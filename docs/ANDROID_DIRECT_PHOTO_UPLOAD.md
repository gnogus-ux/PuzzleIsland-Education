# Android 선택 사진을 직접 TLS 서버에 올리기

2026-11-09 공식 문서의 필요한 절을 직접 읽고 교차 검토한 구현·검수 매뉴얼이다. **문서 학습 완료이며 앱·기기·서버의 실기 완료가 아니다.** 기존 사진·초안·서버 인증서와 기기 페어링을 보존한다. 선택하지 않은 갤러리 사진이나 다른 프로젝트를 탐색·업로드하지 않는다.

## 1. 적용 환경과 기존 매뉴얼의 부족한 부분

기존 Android 파일 교환 매뉴얼은 작업 컨테이너 가져오기와 수정 JSON 내보내기를, 직접 TLS 매뉴얼은 인증된 작업 다운로드·수정 업로드를 설명한다. 새 사진의 content URI 읽기, 이미지 크기·포맷 검증, 서버 사진함 등록 및 중복 재시도는 별도 근거가 필요해 이번 학습으로 보강했다.

대상은 기존 Java/Android SDK 환경이며 새 AndroidX·Gradle·스토리지 라이브러리 설치를 전제하지 않는다. 검토 환경의 최소 API26/컴파일 API35에서는 프레임워크 `ACTION_OPEN_DOCUMENT`와 `ContentResolver` 경로를 사용할 수 있다. 공식 Android 문서는 현행판이며 API별 추가 시점은 Intent/API reference에서 직접 확인했다. Pillow 현행 문서는13.0.0으로 표시됐다. 검수 담당은 기존 실행환경을11.3.0으로 확인했다고 보고했다. 문서 담당은11.3.0 태그의 공식 Image/ImageOps 소스 해당 절을 추가로 직접 읽어 open(formats)·lazy load·verify/재열기·픽셀폭탄 제한·exif_transpose의 비파괴 사본 경로가 같은 원리임을 대조했다. 이는 실제 이미지 업로드/디코딩 성공을 뜻하지 않는다. 버전별 문서 URL은 제공되지 않아 공식 태그 소스를 근거로 사용했다.

## 2. 사진 선택과 URI 읽기

1. 사진 올리기 버튼은 Android 시스템 선택기를 연다. 기존 프레임워크만 사용하는 첫 경로는 `ACTION_OPEN_DOCUMENT`, MIME `image/*`, `CATEGORY_OPENABLE`이다. 사용자 선택 파일만 읽고 광범위한 저장소 권한이나 갤러리 전수 목록을 요구하지 않는다. 카메라 촬영은 별도 기능이며 이번 경로가 자동 제공하지 않는다.
2. API19부터 이 액션을 지원한다. 단일 파일은 결과 `getData()`의 content URI를 사용한다. 복수 선택을 지원하려면 `EXTRA_ALLOW_MULTIPLE`을 명시하고 `ClipData`의 실제 반환 항목 수에 제한을 둔다. 단일 선택만 구현했다면 여러 장 일괄 업로드 완료로 보고하지 않는다.
3. `getType()`은 null일 수 있고 공급자의 MIME·표시 파일명·선언 크기는 신뢰 경계 바깥이다. URI를 실제 경로로 역변환하거나 filename을 서버 경로로 쓰지 않는다. `ContentResolver.openInputStream()` 결과의 null, `FileNotFoundException`, `SecurityException`, 중간 읽기 오류를 처리한다. 자원을 확실히 닫고 UI 스레드에서 대용량 읽기·업로드하지 않는다.
4. `CATEGORY_OPENABLE`은 스트림으로 열 수 있는 문서를 요구하는 선택이다. SAF 가상 문서는 별도 typed asset 경로가 필요하므로 이 첫 범위에서는 명확히 제외한다. cloud provider는 시스템 선택기에 보일 수 있다. 다운로드 지연/실패를 로컬 성공으로 표시하지 않는다.
5. 선택 취소는 업로드0·현재 작업/초안 보존이다. URI 크기가 알려지지 않아도 실제 읽은 바이트에서 상한을 검사한다. 파일을 메모리 무제한으로 읽지 말고 앱 전용의 제한된 staging 파일에 모은 뒤 크기·해시를 확인한다. 서버가 Content-Length를 요구하면 이 확정 크기로 보낸다.
6. 즉시 읽고 사본을 staging하는 흐름에는 장기 URI 권한을 불필요하게 취하지 않는다. 재부팅 뒤 같은 URI를 재사용하는 큐를 구현했다면 반환 플래그 범위에서 persistable read 권한을 취하고, 이동/삭제/권한해제로 다시 열리지 않는 경우 재선택을 요구한다. 권한을 취한 사실이 영구 접근 보장은 아니다.

## 3. 전송·등록 계약

- 선택한 사진명·개수/크기와 도착할 사진함을 짧게 보여 주고 전송을 시작한다. 현재 편집 작업을 업로드 목적지로 자동 간주하지 않는다. 처음에는 기기 전용 사진함이나 명시 선택한 새 프로젝트로 분리하는 편이 기존 작업 보존을 검증하기 쉽다.
- 이미 검수된 정확한 인증서 고정·기간/SAN 검증과 기기별 credential을 재사용한다. 전송 전 TLS 검증, redirect 거부, 제한된 헤더 인증을 유지하고 WebView로 임의 URL을 열거나 인증서 검증을 끄지 않는다. 신규 경로에도 요청마다 인증·권한·폐기를 적용한다. 기존 기기 credential이 임의 프로젝트 쓰기 권한까지 갖는다고 가정하지 않는다.
- 모바일 원본 사진 전송은 JPEG/PNG/WebP 같은 **서버가 실제 지원하는 allowlist**로 좁힌다. `image/*`는 HEIC/AVIF/GIF 등도 선택하게 할 수 있으므로 미지원 형식은 분명히 안내한다. HEIC를 JPEG라고 이름만 바꿔 보내지 않는다. 자동 변환을 추가하려면 원본·변환본의 포맷·픽셀·해시·EXIF 차이와 실제 디코더 지원을 별도로 검증한다.
- 헤더와 실제 수신 바이트·SHA256을 대조한다. 생성한 업로드 ID를 재시도 동안 고정하고 같은 ID/같은 바이트는 같은 접수를 돌려주며 다른 바이트는 충돌로 거부한다. 연결 끊김 뒤 서버 등록 여부가 모호하면 새 ID로 무조건 재전송하지 않는다. idempotency의 영속성·동시성·보존기간도 문서화한다.
- 기기당/전체 수신 개수·총바이트·동시 업로드·읽기/쓰기 및 전체 마감시간을 둔다. 클라이언트와 서버 한도를 일치시키고 서버가 재검사한다. 기존 시스템의 실제 제한은 1장8MiB,24M픽셀,한변8192,프로젝트100장·전체50프로젝트였다. 이 값은 현재 제품 정책의 근거이며 일반 보안 표준의 보편 수치가 아니다. 새 경로에서 몰래 늘리지 않는다.
- 업로드 결과에는 실제 저장 바이트·원본 SHA·지원 포맷·사진/프로젝트 식별자와 상태를 돌려준다. **전송 성공·서버 접수·사진 등록·현재 작업에 사용·측정/계산 확정은 각각 다른 상태**다. 사진 등록이 끝나지 않았는데 'PC에 사진 등록 완료'를 표시하지 않는다.

## 4. 서버 이미지 검증과 원본 보존

1. 원격 전용 endpoint만 연다. 임의 파일 경로·일반 PC 관리 API·HTML 실행·디렉터리 쓰기를 제공하지 않는다. TLS·기기 인증을 통과한 뒤에도 크기/한도/대상 권한을 재검사한다. 외부 파일명은 표시용 메타데이터로만 제한하고 서버가 만든 이름과 지정 루트 아래에 저장한다. 경로순회·제어문자·HTML 이름을 실행/해석하지 않는다.
2. 업로드 파일은 webroot 밖의 비공개 임시 영역에 저장한다. 빈 파일·초과 바이트·Content-Length 불일치·중단된 수신은 등록하지 않는다. 임시파일 성공이 정식 사진 등록 성공은 아니다. 서버가 받지 못한 원본을 기존 프로젝트에 빈 항목으로 남기지 않는다.
3. MIME와 magic bytes만으로 정상 이미지라고 판정하지 않는다. Pillow의 `Image.open()`은 lazy 식별이므로 `formats` allowlist, 실제 폭·높이·픽셀수·프레임수, `verify()`와 재열기 후 제한된 `load()`를 함께 검토한다. `verify()`만으로 전체 디코딩 완료를 주장하지 않는다.
4. `DecompressionBombWarning`을 오류로 처리하거나 더 좁은 제품 픽셀 한도를 명시하고, `MAX_IMAGE_PIXELS=None`으로 제한을 끄지 않는다. 큰 픽셀 할당 전 치수/정수/상한을 검사한다. 경고의 기본 임계값은 라이브러리 버전별 값이며 제품 한도를 대신하지 않는다. 멀티프레임·미지원 파일은 별도 검증 전 거부한다. 기존 격리 Pillow 도구·마감시간을 활용하고 새 이미지 라이브러리를 설치하지 않는다.
5. 원본 바이트와 원본 SHA를 불변으로 저장한다. 표시용 정규화 사본은 별도 이름/해시로 만든다. `ImageOps.exif_transpose()`는 Orientation에 따라 픽셀을 변환하고 orientation 정보를 제거하므로 원본파일에 덮어쓰지 않는다. 원본 해상도/EXIF 방향과 표시 사본 좌표 기준을 함께 기록한다. metadata 제거는 표시/배포 사본에 적용하고 원본까지 손실시키지 않는다.
6. 기존 PC 사진 저장 파이프라인의 해상도·ICC·EXIF·불변 원본 정책을 재사용한다. 현재 선택 PC 프로젝트나 진행 중 job을 전환·덮어써야만 새 사진을 등록할 수 있는 메서드를 원격 요청에서 그대로 호출하지 않는다. 원격 업로드 전용 목적지/잠금/원자적 등록을 명시하고, PC에서 보이는 프로젝트 목록과 사진 수까지 확인한다. 기존 사진 교체는 별도 명시 요청 없으면 금지한다.
7. OWASP의 재인코딩 권고는 공격면을 줄이는 계층 중 하나이며 안전 보증이 아니다. 이 프로젝트의 원본 보존 요구와 함께 적용할 때 원본은 비공개 불변 보관, 제한적으로 디코딩한 표시 사본만 UI에 사용한다. 실제 원본을 공개 파일 서버로 그대로 배포하는 기능으로 확대하지 않는다.

## 5. 최소 독립 검수

| 구분 | 확인할 결과 |
|---|---|
| 실제 폰 정상 흐름 | 사진 올리기→시스템 선택→정상 이미지 선택→인증 업로드→PC 사진함의 원본 SHA/크기·정규화 사본 확인 |
| 기존 상태 보존 | 선택/업로드 전후 현재 작업·초안·페어링·PC 현재 프로젝트·기존 사진이 보존됨 |
| 취소·실패 | 선택 취소·provider null/권한실패·지원외 포맷·초과 파일·손상 이미지·오프라인/마감 실패에서 성공 표시·부분 등록이 없음 |
| 인증·권한 | 누락/폐기/타기기 credential·사진함 권한 혼용·다른 인증서·redirect를 거부함 |
| 한도·재시도 | 실제 스트림 초과, 픽셀폭탄, 동시 한도 경계, 같은 업로드 ID 재시도에서 중복/한도 초과가 없음 |
| 등록 원자성 | 정규화/디스크/메타데이터 실패 시 정식 빈 항목·기존자료 손실이 없고 다음 정상 등록이 가능함 |
| 좌표·방향 | EXIF 회전/미러 예제의 원본 SHA 유지와 표시 방향·정규화 좌표 기준이 맞음 |
| 경로 구분 | USB는 선택/설치에 쓸 수 있으나 전송은 실제 앱 TLS여야 함. 같은 Wi-Fi와 독립 CELLULAR 경로를 분리해 기록 |
| 앱 업데이트 | 기존 서명키로 versionCode 증가 빌드·업데이트 설치 후 초안/페어링 보존. 단순 APK 생성과 실제 설치/전송을 구별 |

정상/실패 fixture와 실제 원본 대신 명시된 시험 사진을 사용한다. 자동 전체 갤러리 업로드·사용자 사진 수집·기존 원본 적용을 검수 편의로 추가하지 않는다. 작성자 자체검사·독립 파일 검수·실기·통신사망·전체 제품 승인은 별도로 판정한다.

## 6. 실제 읽은 원출처와 학습 범위

1. [Android SAF](https://developer.android.com/training/data-storage/shared/documents-files): 문서 열기·MIME·URI 권한·메타데이터·가상문서/stream 제한 절.
2. [Android Intent reference](https://developer.android.com/reference/android/content/Intent): ACTION_OPEN_DOCUMENT(API19), CATEGORY_OPENABLE, EXTRA_ALLOW_MULTIPLE, URI grant 설명 절. 모든 Intent API를 학습한 것은 아니다.
3. [Android ContentResolver reference](https://developer.android.com/reference/android/content/ContentResolver): getType, openInputStream, null/예외/URI scheme 절. 문서 전체 API 전수 실습은 하지 않았다.
4. [OWASP File Upload](https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html): type/signature/filename/content/storage/user permissions/limits와 이미지 재인코딩의 제한. 현재 서버의 공격 안전성 실기 증거는 아니다.
5. [Pillow Image](https://pillow.readthedocs.io/en/stable/reference/Image.html): Image.open의 lazy 식별·formats, DecompressionBombWarning/Error, verify와 재열기·load 절. 현행 문서13.0.0과 실제 설치 버전은 별도 대조 대상이다.
6. [Pillow ImageOps](https://pillow.readthedocs.io/en/stable/reference/ImageOps.html): exif_transpose의 방향변환/Orientation 제거·in_place 설명 절.

학습일은2026-11-09다. 웹본문의 해당 절만 실제 읽었고 영상·자막·기기·서버 실기는 실행하지 않았다. 공식 권고와 현재 제품 적용 제안을 구별했으며 원문 전문·외부 코드·제품 사진·개인 경로·기기고유ID·주소·인증정보는 포함하지 않았다.

[공식 자료 학습 범위](../reports/ExternalLearning/20261109_ANDROID_DIRECT_PHOTO_UPLOAD_STUDY.json) · [기존 직접 TLS 전송](DIRECT_TLS_FILE_EXCHANGE.md) · [기존 Android 파일 교환](ANDROID_OFFLINE_FILE_WORKFLOW.md)

버전 적용 대조: [Pillow11.3.0 Image 공식 태그](https://github.com/python-pillow/Pillow/blob/11.3.0/src/PIL/Image.py) · [Pillow11.3.0 ImageOps 공식 태그](https://github.com/python-pillow/Pillow/blob/11.3.0/src/PIL/ImageOps.py). 태그의 해당 함수·docstring만 읽었으며 라이브러리 전체 소스 학습/실기와 구별한다.
