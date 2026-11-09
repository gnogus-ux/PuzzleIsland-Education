# 기존 SDK/JDK로 Android 오프라인 편집기 APK 준비

2026-11-09 공식 도구 문서 학습과 독립 검수 담당의 제한된 도구 확인 보고를 정리했다. 이 문서는 **빌드 절차 제안**이다. 문서 작성자는 빌드·서명·설치·기기 조작을 실행하지 않았으며 APK 성공을 주장하지 않는다. [오프라인 파일 교환 설계](ANDROID_OFFLINE_FILE_WORKFLOW.md)와 함께 적용한다.

## 확인 범위와 의존성

검수 담당은 기존 Android API 35 / Build Tools 35.0.1에서 aapt2 실행 버전 `2.19-12874835`, 기존 Temurin java/javac 실행 버전 `17.0.20.1+1`을 확인했다. 후속 기존 JAR 실행에서 D8 `8.6.2-dev`, apksigner `0.9` 버전을 확인했고 API 35 플랫폼 revision 2 / Build Tools 35.0.1 메타데이터도 대조했다. android.jar·zipalign은 파일 존재 확인이다. DEX 생성·APK 서명·정렬 실행 성공은 아직 확인하지 않았다. Gradle은 PATH에서 발견되지 않았으며 캐시나 전체 시스템의 부재까지 판정한 것은 아니다.

프레임워크 Java의 Activity·WebView·Storage Access Framework(SAF)를 사용하는 작은 앱은 아래 도구 체인으로 검토할 수 있다. AndroidX WebKit/Gradle/외부 라이브러리가 이미 있다는 가정을 두지 않는다. AssetLoader가 없으면 외부 접근을 차단한 자체 포함 HTML과 `loadDataWithBaseURL` 경로를 검토한다. 새 의존성 설치·다운로드·보안 설정 변경은 이 문서가 승인하지 않는다.

## 제안 빌드 순서

1. 별도 작업 영역에서 Manifest, Java 소스, 필요한 res, 고정한 HTML/JS/CSS assets를 준비한다. 실제 API 사용에 맞춘 minSdk/targetSdk와 package/version을 정한다. 서버 API를 호출하던 편집기는 먼저 로컬 파일·초안 어댑터를 갖춰야 한다. 온라인 URL을 포장하는 것만으로 오프라인 앱이 되지 않는다.
2. [AAPT2 공식 문서](https://developer.android.com/tools/aapt2)의 `compile`로 리소스 중간 파일을 만들고 `link`에서 `--manifest`, 플랫폼 `-I android.jar`, `--java`, `-A` assets, 별도 `-o` 출력을 지정한다. 이 단계의 APK에는 DEX와 서명이 없어 설치 결과물이 아니다.
3. 기존 javac로 앱 Java와 생성된 R.java를 플랫폼 android.jar에 대해 컴파일한다. JDK 17 실행 가능과 Android에서 사용 가능한 Java/API는 별개다. 선택한 언어 수준·플랫폼 API에 맞추고, 존재를 확인하지 않은 Java API desugaring 라이브러리를 전제하지 않는다.
4. [D8 공식 문서](https://developer.android.com/tools/d8)에 따라 컴파일된 클래스 전체를 DEX로 변환한다. `--lib android.jar`, 일관된 `--min-api`, 필요한 `--classpath`, 별도 출력 위치를 지정한다. 최종 기기용 DEX에는 `--intermediate`를 사용하지 않는다. `--debug` 또는 `--release`는 DEX 정보 설정이며 서명·배포 승인이 아니다.
5. 리소스 APK의 Manifest·리소스·assets를 보존하면서 classes.dex(필요하면 전체 DEX 집합)를 루트에 넣어 별도의 미서명 APK를 만든다. 기존 JDK의 ZIP/JAR 기능 등으로 가능한 패키징을 검토하되 실행 가능한 도구 여부와 엔트리 중복/누락을 검증한다. 이 조립 방법은 문서 작성자의 적용 제안이며 아직 재현하지 않았다.
6. [zipalign 공식 문서](https://developer.android.com/tools/zipalign)에 따라 **서명 전에** 다른 이름으로 정렬한다. 일반 비압축 파일은 4바이트 정렬이며, 비압축 native .so가 들어가면 `-P 16` 조건도 확인한다. 프레임워크 전용 앱에 native 라이브러리를 임의 추가하지 않는다. `-c`로 정렬 검사를 별도로 수행한다.
7. [apksigner 공식 문서](https://developer.android.com/tools/apksigner)에 따라 정렬된 APK를 별도 출력 파일로 서명하고 `verify --verbose --print-certs`로 확인한다. 서명 후 APK 바이트를 수정하면 다시 서명해야 한다. APK SHA256·서명 인증서 지문·앱 버전·소스/빌드 근거를 비공개 인수 기록에 남겨 설치할 파일을 식별한다.

각 단계 종료 코드와 산출물 존재를 확인하고 실패하면 다음 단계로 진행하지 않는다. 기존 APK·서명키·제품 사진·PC 기준 파일을 덮어쓰지 않는다. 서명/정렬 통과와 앱 기능 검수는 별개다.

## 서명키와 설치 경계

서명키와 암호는 공개 Git·문서·채팅·명령행 인자·일반 로그에 넣지 않는다. 작업 전용 비공개 영역에서 생성/보존하며 apksigner가 지원하는 표준입력 또는 접근을 제한한 암호 파일을 사용한다. 키 생성 도구도 기존 사용 가능 여부를 먼저 확인한다. 앱 업데이트에는 서명 정체성 유지가 필요하므로 키를 임의 재생성하거나 기존 배포키를 덮어쓰지 않는다.

[Android 앱 서명 안내](https://developer.android.com/studio/publish/app-signing)의 개발용 인증서와 Play 배포 절차는 구분한다. 자체 개발 시험용으로 서명한 APK는 Play 출시·심사·스토어 배포를 완료한 앱이 아니다. 기존 Android Studio가 자동 생성한 debug key를 썼다고 가정하지 않는다.

APK 생성 → 정렬/서명 검사 → 사용자가 허용한 설치 → 네트워크 없이 실제 편집/초안 복구/SAF 파일 저장 → PC 명시 가져오기·재열기 검증을 각각 기록한다. 앱 설치 확인·보안 경고·권한/인증은 사용자 직접 단계이며 자동 변경하지 않는다. 현재 이 순서의 APK 빌드 이후 단계는 **미검증**이다.

학습 범위와 도구 확인 근거는 별도 JSON으로 보존하며, 공개 기록에는 개인 PC 경로·기기 식별자·서명키·사진을 포함하지 않는다.
