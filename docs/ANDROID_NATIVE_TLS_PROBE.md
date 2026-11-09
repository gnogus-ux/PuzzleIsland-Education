# 앱을 보존하는 Android 네이티브 TLS 격리 검수

2026-11-09 공식 문서·AOSP 소스의 선택 범위를 대조한 **검수 절차 제안**이다. 작성자는 DEX/시험 코드를 만들거나 폰·서버를 실행하지 않았다. [직접 TLS 파일 교환 설계](DIRECT_TLS_FILE_EXCHANGE.md)의 인증서 검증기를 Android 런타임에서 좁게 확인하기 위한 경로이며, 설치 앱 전체·공개 서버·이동통신 성공 판정이 아니다.

## 지원 근거와 한계

[AOSP Android16 app_process 구현](https://android.googlesource.com/platform/frameworks/base/+/99b01a65cc4c104933788b3143285ab6bae65827/cmds/app_process/app_main.cpp)은 31행의 CLI 구문, 56–72행의 CLASSPATH 클래스 검색, 86행의 main 호출을 제공한다. 190–211행은 VM 인수·현재 미사용인 cmd-dir·실행 클래스/인수를 설명하며, 285–299행과 336–339행은 non-zygote 클래스 실행을 RuntimeInit으로 연결한다. 이는 **플랫폼 내부 CLI 구현 근거**이며 장기 호환을 보장하는 일반 앱 SDK API가 아니다. OEM·빌드·정책에 따른 현재 기기 실행 가능성은 실제 확인 전 미검증이다.

[같은 릴리스의 shell 정책](https://android.googlesource.com/platform/system/sepolicy/+/d4a7f392598cee96d9479a8ac0f84259c19b043a/private/shell.te)은 24–26행에서 app_process 실행 용도를 명시하고, 291행에서 shell의 네트워크 속성을 부여하며, 309–312행에서 shell 임시 파일 접근, 349행에서 해당 실행 파일 타입 접근을 허용한다. [public/shell.te](https://android.googlesource.com/platform/system/sepolicy/+/d4a7f392598cee96d9479a8ac0f84259c19b043a/public/shell.te) 1–3행은 ADB/console shell 도메인이다. [file_contexts](https://android.googlesource.com/platform/system/sepolicy/+/d4a7f392598cee96d9479a8ac0f84259c19b043a/private/file_contexts) 274–275·626행의 app_process/임시 영역 타입과 교차 확인했다. [매크로](https://android.googlesource.com/platform/system/sepolicy/+/d4a7f392598cee96d9479a8ac0f84259c19b043a/public/te_macros) 242행과 279행은 정책 속성을 부여하며 앱의 패키지 UID로 전환하는 명령이 아니다.

[Android SELinux 지침](https://source.android.com/docs/security/features/selinux)은 기본 거부와 강제 적용을 설명한다. 위 AOSP 정책만으로 OEM의 전체 허용 규칙·실제 uid/context·실행 파일/DEX 접근·네트워크 가능을 보장하지 않는다. 일반 허용된 ADB shell에서 거부되면 그 항목을 미검증으로 남기고 중단한다. root·run-as·SELinux 완화·정책/소유권 변경·hidden API 제한 해제를 해결책으로 쓰지 않는다.

## 원앱과 분리할 시험 범위

기존 앱을 실행·종료·업데이트하거나 pairing/CA/권한/보안 설정·초안·사용자 파일에 접근하지 않는다. 원앱의 사설 data 경로를 읽는 방식도 사용하지 않는다. 이 경로는 보통의 ADB shell에서 별도 Java main을 시작하는 것이다. `--application`이라는 옵션명도 설치 앱의 UID·Manifest·Context를 얻는다는 의미가 아니다. zygote/system-server 모드는 사용하지 않는다.

후보의 **동일한 순수 Java TLS 클래스**와 작은 시험 main만 기존 JDK/SDK로 컴파일할 수 있는지 확인한다. 소스/입력·클래스/DEX 해시와 컴파일 설정을 보존하고, 시험을 통과시키려고 후보의 핀·호스트·유효기간 검사에 예외를 추가하지 않는다. 숨겨진 Android API·원앱 Context·Keystore가 필요한 코드이면 순수 클래스 프로브 범위를 벗어나므로 멈추고 대안을 검토한다.

[D8 공식 문서](https://developer.android.com/tools/d8)에 따라 호환되는 Java 바이트코드와 android.jar, 필요한 classpath, min-api를 명시하고 최종 DEX를 만든다. D8의 JAR/ZIP 출력은 classes.dex를 담을 수 있다. 일반 `.class` JAR와 혼동하지 않고 최종 실행용에는 `--intermediate`를 쓰지 않는다. 앱 설치·서명·새 AndroidX/Gradle 다운로드를 이 절차의 조건으로 삼지 않는다. 실제 컴파일·ART 로드는 별도 검증이다.

## 보존·실행·정리 순서

1. 기존 USB/RSA 허용 상태와 현재 대상 기기를 [ADB 문서](https://developer.android.com/tools/adb)의 명시 대상 선택 방식으로 확인한다. 기기 확인·일반 shell uid/SELinux 상태·실행 파일 존재·현재 forward/reverse 목록을 최소 조회한다. 새 인증 창은 사용자가 처리하며 자동 설정 변경을 하지 않는다. 기존 매핑을 대체하지 않는다.
2. PC의 별도 로컬 fixture 서버에 시험 전용 인증서/개인키·일회성 credential을 둔다. 기기에는 공개 시험 인증서·임시 credential 파일·DEX/config만 새 전용 하위 디렉터리에 넣는다. 실제 서버 키·실사용 token·제품 사진·사용자 pairing 파일은 사용하지 않는다. `/data/local/tmp` 전체가 아닌 이번에 만든 디렉터리와 명시 파일 목록만 점유한다. credential은 argv·환경값·일반 로그로 전달하지 않고 제한한 시험 파일로 읽는다.
3. [공식 ADB CLI 구현](https://android.googlesource.com/platform/packages/modules/adb/+/ce023afef190b0cea7f8939e9dd5ee3ee79b137b/client/commandline.cpp) 131–139행은 reverse 목록·`--no-rebind`·개별 제거를 제공한다. 충돌하지 않는 기기 시험 포트 하나만 PC의 loopback fixture로 reverse하고 기존 포트 점유가 있으면 실패시킨다. `--remove-all`이나 기존 ADB 서버 종료를 정리 수단으로 쓰지 않는다. 이 연결은 USB 경로이며 공유기/방화벽/셀룰러 시험이 아니다.
4. DEX를 바꾸지 않을 시험 자산으로 확인한 뒤 일반 shell에서 일회성 CLASSPATH와 non-zygote main을 사용한다. 개념 구문은 `CLASSPATH=<전용 DEX JAR> app_process /system/bin <시험 main> <시험 config 경로>`다. 명령 문자열/경로 quoting은 PC와 기기 shell 두 단계에서 검토한다. 기기마다 존재하는 app_process 변형과 정책을 먼저 확인하며 시스템 바이너리·전역 환경·ART 설정은 바꾸지 않는다. 이 문서는 해당 명령을 실행한 기록이 아니다.
5. 시작 시 probe의 소유 PID·uid/context·Android/API·Java 런타임·SSLContext provider와 socket 구현·후보/입력 해시를 민감값 없이 기록한다. 실제 provider가 원하는 기기 TLS 제공자인지 확인하기 전 Conscrypt 검수라고 단정하지 않는다. PC JDK에서 같은 클래스가 통과한 결과와 별도 기록한다.
6. 전체 실행에 독립적인 host 마감 시간을 두고 connect/read/write·TLS 실패·서버 응답을 개별 측정한다. main 반환만으로 남은 스레드·프로세스가 없다고 추정하지 않는다. 마감 초과 시 확인한 **소유 probe PID만** 종료하고 결과를 실패/미완료로 남긴다. 앱·adbd·다른 app_process·사용자 서버를 종료하지 않는다.
7. 민감값 없는 결과를 회수한 뒤 소유 probe/fixture의 정상 종료·리스너 해제를 확인한다. 이번 reverse 하나만 제거하고 이전 forward/reverse 목록 보존을 대조한다. 시험 디렉터리와 목록을 다시 확인한 뒤 이번 파일만 정리한다. 루트 임시 영역 일괄 삭제·와일드카드 전역 정리·기존 앱 데이터 삭제는 하지 않는다. 정리 실패도 미확인으로 기록한다.

## TLS와 인증 미전송을 검수할 항목

정상 exact leaf/SAN/유효기간·시험 credential로 허용한 요청 한 건을 먼저 확인한다. 이어 다른 인증서, **같은 키로 발급한 다른 DER 인증서**, 만료/미래 인증서, exact pin은 맞지만 SAN은 다른 인증서, redirect와 평문, 잘못된/폐기 시험 credential을 구분해 시험한다. 실제 기기 시간을 바꾸어 만료를 만들지 않는다.

TLS 거부 케이스에서는 서버가 TLS 접속을 관찰할 수 있다. 이것을 인증 유출로 혼동하지 않고 **HTTP 요청 수·Authorization 존재 여부·본문 바이트 수**를 별도 안전한 계수로 확인한다. TLS 신뢰·핀·SAN·기간 실패 전에 credential/본문이 전송되지 않았는지 검수한다. 헤더/토큰 원문·개인키·인증서 비밀 데이터를 로그로 남기지 않는다. 잘못된 credential의 HTTP 거부와 TLS 거부는 서로 다른 시험이다.

fixture URL의 호스트/IP와 SAN은 실제 검수 조건에 맞춰야 한다. 후보의 endpoint 허용 정책이 로컬 fixture와 충돌하면 어느 계층까지 시험했는지 나누고, 실제 후보에 임시 trust-all/호스트 예외를 넣어 통과시키지 않는다. native 클래스 통과는 앱의 INTERNET 권한·Manifest/NetworkSecurityConfig·Keystore/백업·SAF pairing·UI·취소/초안 보존·실제 외부 IP 인증서를 검증한 결과가 아니다. 이 앱 통합과 이동통신 연결은 후속 별도 시험으로 남긴다.

## 경로가 막히면

[공식 instrumentation 안내](https://developer.android.com/studio/test/command-line)는 main/test APK의 빌드·설치와 선언된 runner를 전제로 `am instrument`를 사용한다. 별도 시험 패키지·runner/의존성·호환 API·서명·설치 승인·대상 앱과 데이터 보존 계획이 필요하다. AndroidX runner나 Gradle 캐시가 이미 있다고 가정하지 않는다. 지금 허용된 설치 없는 probe가 거부됐다는 이유로 원앱을 대상으로 instrumentation을 시작하거나 새 APK를 설치하지 않는다. 필요한 항목만 보고하고 현재 검수 범위를 미완료로 남긴다.

공식 근거는 이 제한된 경로를 **제안할 근거**이며 실제 폰 실행 성공을 뜻하지 않는다. [문서/소스별 실제 열람 범위](../reports/ExternalLearning/20261109_ANDROID_NATIVE_TLS_PROBE_STUDY.json)와 함께 사용한다.
