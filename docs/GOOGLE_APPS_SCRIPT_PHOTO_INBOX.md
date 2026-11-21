# 휴대폰 원본 사진을 구글 드라이브 '받기 전용 주소'로 받기

2026-11-21 Claude가 공식 문서의 필요한 절을 직접 읽고 작성한 구현·검수 매뉴얼이다. **문서 학습과 실제 배포·폰 실기는 별개다.** 이 문서를 쓴 시점에 실제 Apps Script 배포·실제 폰 업로드·실제 Gmail 수신은 실행하지 않았다(학습 기록 참고).

## 1. 적용 대상과 기존 매뉴얼과의 차이

- 목적: 다른 사람이 Android 앱으로 찍은 **원본** 사진·짧은 영상을 사용자 구글 드라이브의 한 폴더에 묶음별로 올리고, PC(Google Drive for desktop 동기화 폴더)가 검사·알림한다.
- 기존 [Android 직접 사진 업로드](ANDROID_DIRECT_PHOTO_UPLOAD.md)는 PC 서버로 TLS 직접 전송이다. 이 방식은 **PC 주소를 앱에 넣지 않는다.** 앱은 받기 전용 주소 1곳에만 올릴 수 있어 PC를 조작할 수 없다.
- 공유 폴더 초대 방식과 비교: 보내는 사람은 구글 계정이 필요 없고, 서로의 사진을 볼 수 없다. 대신 소유자가 Apps Script 웹앱을 직접 배포해야 한다.

## 2. Apps Script 웹앱의 공식 동작 (확인한 범위)

1. 웹앱으로 게시하려면 `doGet` 또는 `doPost`가 있어야 하고, HTML 서비스 `HtmlOutput` 또는 콘텐츠 서비스 `TextOutput`을 반환한다. JSON 응답은 `ContentService.createTextOutput(..).setMimeType(ContentService.MimeType.JSON)`.
2. POST 요청이면 `doPost(e)`가 실행된다. 본문은 `e.postData.contents`(텍스트), 형식은 `e.postData.type`, 길이는 `e.contentLength`. **매개변수 이름 `c`, `sid`는 예약어**라 쓰면 405가 날 수 있다 → 본문 JSON 키로 쓰지 않는다.
3. 본문은 텍스트로 받으므로 사진은 **base64 문자열**로 보내고 `Utilities.base64Decode` → `Utilities.newBlob(bytes, mime, name)` → `folder.createFile(blob)`로 저장한다.
4. 배포: 배포 > 새 배포 > 유형 '웹 앱' > 실행 사용자 **나**, 액세스 **모든 사용자** > 배포. '나로 실행'이면 누가 호출해도 소유자 권한으로 실행된다. 처음 배포 때 소유자가 권한 동의 화면을 직접 승인한다(자동화 금지).
5. 테스트 배포 URL은 `/dev`로 끝나며 편집 권한자만 쓴다. 실제 앱에는 `/exec` 배포 URL을 넣는다. 코드를 바꾸면 **배포 관리에서 새 버전**으로 다시 배포해야 `/exec`에 반영된다.
6. 개발자로 실행되는 웹앱은 `ScriptApp.getOAuthToken` 값을 절대 응답에 넣지 않는다.

## 3. 한도 (일반 gmail.com 계정, 공식 표 기준; 예고 없이 바뀔 수 있음)

| 항목 | 값 | 설계 반영 |
|---|---|---|
| 스크립트 실행 시간 | 6분/실행 | 요청 하나에 조각 하나만 저장 |
| 사용자당 동시 실행 | 30 | 앱은 한 번에 1개씩 순서대로 보냄 |
| 메일 수신자 | 100명/일 | 알림은 소유자 1명, 하루 상한을 스크립트에 둠 |
| 메일 본문 | 200KB/메시지 | 알림은 짧은 글 |
| 속성 값/총량 | 9KB/값, 500KB/저장소 | 묶음 토큰만 저장하고 오래된 것 정리 |

**문서에 없는 것(실측 필요):** `doPost` 요청 본문 최대 크기. 조각 크기를 4MiB 원본(base64 약 5.6MB)으로 보수적으로 잡고, 실제 배포 후 큰 사진 1장으로 확인한다. POST 응답은 302로 다른 주소(googleusercontent)로 넘어갈 수 있으므로 앱은 **자동 리다이렉트를 끄고 Location을 GET으로 따라가** JSON을 읽는다(관찰된 일반 동작, 공식 문서에서는 확인 못 함 → 실측 대상).

## 4. 받기 전용 계약 (최소 기능)

- `begin`: 초대 코드 확인 → `이름_YYYYMMDD_HHMM` 폴더 생성(서울 시간, 이름은 글자·숫자·밑줄만) → 임의 묶음 토큰 반환. 하루 묶음 수 상한.
- `put`: 코드+토큰 확인 → 파일 이름 정리(경로 문자 제거, 확장자 허용 목록) → 조각 저장(`이름.part003of007`). 같은 이름이 이미 있으면 다시 저장하지 않고 성공(재시도 안전).
- `finish`: `정보.json`(파일별 SHA-256·크기·장면)과 끝 표시 저장 → 토큰 폐기(더 못 올림).
- `notify`: 별도 PC 키 확인 → **소유자 본인 메일로만** 짧은 알림. 수신자를 요청에서 받지 않는다.
- 없음: 목록 보기, 파일 읽기·내려받기, 지우기, 다른 폴더 접근. 실패 응답은 이유를 자세히 알리지 않는다(코드 추측 방지).
- 비밀값(초대 코드·PC 키)은 스크립트 속성에만 둔다. 코드에·저장소에·보고서에 적지 않는다. 코드를 바꾸면 이전 코드는 즉시 무효.

## 5. Android 쪽 (공식 문서 확인 범위)

1. 촬영: `MediaStore.ACTION_IMAGE_CAPTURE`에 `EXTRA_OUTPUT`을 주면 **원본 크기**가 그 URI에 저장된다. 주지 않으면 작은 Bitmap만 온다. 영상은 `ACTION_VIDEO_CAPTURE` + `EXTRA_DURATION_LIMIT`(초).
2. 앱이 `CAMERA` 권한을 **선언만 하고 허용받지 않으면** `ACTION_IMAGE_CAPTURE`가 SecurityException → 카메라 권한을 선언하지 않는다(시스템 카메라 앱이 찍는다).
3. 고르기: `MediaStore.ACTION_PICK_IMAGES`(API33+, R 확장 2)는 저장소 권한 없이 고른 항목만 읽게 한다. 여러 장은 `EXTRA_PICK_IMAGES_MAX`(1 초과, `getPickImagesMaxLimit()` 이하, 아니면 취소로 돌아옴). 없으면 `ACTION_GET_CONTENT`/`ACTION_OPEN_DOCUMENT`로 대체.
4. 사진 선택기의 읽기 권한은 기본으로 앱 종료·재시작까지다. 오래 걸리는 업로드·재개를 위해 **고른 즉시 원본 바이트를 앱 저장소에 그대로 복사**(재압축 없음)하고 그 사본에서 SHA-256을 계산한다.
5. HDR 영상은 선택기가 SDR로 변환할 수 있다(API33+, 명시 요청 시). 원본이 필요하므로 변환 기능을 요청하지 않는다.
6. 촬영 결과를 넣을 MediaStore 항목은 API29+에서 권한 없이 만들 수 있으므로 최소 API를 29로 둔다(그 아래는 저장소 권한 필요 → 범위 밖).

## 6. PC 감시와 검사

- 동기화 폴더의 받는 폴더만 읽는다. 끝 표시가 있는 묶음만 처리하고, `정보.json`의 모든 파일·조각이 동기화될 때까지 기다린다(동기화 지연).
- 조각을 합쳐 **로컬 작업 폴더**에 사본을 만들고 SHA-256·크기·파일 시작 표식(JPEG/PNG/HEIC/MP4)을 확인한다. 받은 파일을 실행하지 않는다.
- 빠진 장면 목록과 흐림 값(폰이 계산해 보낸 값)을 쉬운 한국어 `검사결과.txt`로 남기고, 알림은 묶음당 한 번(상태 파일로 중복 방지).

## 7. 검수 기준

- 앱 APK 권한이 `INTERNET` 하나뿐인지 `aapt2 dump permissions`로 확인.
- 초대 코드 틀림·토큰 없음·허용 안 된 확장자·`../` 이름·조각 번호 범위 밖은 저장 0.
- 같은 조각 재전송은 파일 1개 유지. `finish` 뒤 `put`은 거부.
- PC: SHA 불일치·조각 누락은 '불완전'으로 표시하고 알림에 적는다. 같은 묶음 알림 1회.
- 실제 배포·폰 업로드·큰 사진 크기 한도·302 동작·Gmail 수신은 배포 후 실기로 별도 기록한다.

## 출처 (2026-11-21 직접 열람, 한국어 번역 페이지)

- Google Apps Script 가이드 '웹 앱': https://developers.google.com/apps-script/guides/web
- Google Apps Script '서비스 할당량': https://developers.google.com/apps-script/guides/services/quotas
- Apps Script 참조 Drive `Folder`(createFile/createFolder/getFoldersByName/getFilesByName): https://developers.google.com/apps-script/reference/drive/folder
- Apps Script 참조 `MailApp`(sendEmail, getRemainingDailyQuota): https://developers.google.com/apps-script/reference/mail/mail-app
- Android `MediaStore` 참조(ACTION_IMAGE_CAPTURE, ACTION_VIDEO_CAPTURE, ACTION_PICK_IMAGES, EXTRA_DURATION_LIMIT, EXTRA_PICK_IMAGES_MAX): https://developer.android.com/reference/android/provider/MediaStore
- Android '사진 선택 도구': https://developer.android.com/training/data-storage/shared/photopicker
