# PC 직접 TLS 파일 교환과 Android 페어링 설계

2026-11-09 공식 문서 선택 범위 학습에 따른 **r17 설계와 제한된 로컬 실기 기록**이다. 문서 작성자는 서버·인증서 생성·앱 연결·포트 전달·외부 이동통신 실기를 실행하지 않았다. 후속 독립 native fixture 실행은 아래 별도로 기록한다. 기존 [r16 오프라인 파일 교환](ANDROID_OFFLINE_FILE_WORKFLOW.md)의 APK·초안·결과 파일·PC 원본을 보존한다. Cloudflare·VPN·새 계정/도메인·설치·비용·보안 설정 변경을 수행하지 않는다.

## 후속 확인 — Windows 로컬 TLS와 업데이트 설치

검수 담당이 저장한 결과를 작성자가 대조했다. 검수된 코드 69파일의 배포·해시 대조, 기존 데이터 189파일 및 보호 원본 475파일 불변이 확인됐다. 코드·데이터·캐시는 별도 영역에 두었으며 실제 서비스는 loopback에서만 실행했다. 개인 경로·제품 파일/사진 해시·키/credential 원문은 게시하지 않는다.

실제 전용 TLS 키 생성·PEM 로드 후, loopback 전송에서 인증서 IP SAN을 참조 identity로 사용하는 표준 TLS 검사·정확한 인증서 일치·TLS1.3 협상이 통과했고 무인증 작업 목록 요청은 HTTP401이었다. IP SAN 참조값과 TCP 연결 목적지를 구분한다. 이는 LAN·공유기/방화벽 수신·공인 IP·이동통신 도달 성공이 아니다.

기존 서명키를 보존한 실제 Windows APK 빌드의 v2/v3와 같은 서명 업데이트 설치를 확인했다. 설치 완료 후 확인한 앱은 versionCode2 / r17-1이고 INTERNET 권한을 선언한다. 기존 작업/저장 버전·초안 없음 상태와 PC 연결 메뉴·미페어링 안내 표시만 확인했다. 설치 도중 이전 버전을 보여 준 조기 캡처는 증거에서 제외했다. 실제 앱 페어링·네이티브 송수신은 아직 하지 않았다.

Windows에서는 제작자 시나리오를 검수 담당이 재실행해 서버 124/124·PC e2e 54/54가 통과했다. symlink 생성/정리의 OSError 시 건너뛰는 항목 1건은 이 Windows 실행에서 미실행이다. 별도 제작자 sandbox의 125건과 합산하지 않는다. 검수 담당이 직접 작성한 작은 한도·잠금 유지/만료 회복 재현 통과는 이 시나리오 재실행과 별도 근거다.

이전 shell native 11건은 빌드/native 입력 21파일 불변 대조를 근거로 재사용하며 새 native 실행으로 세지 않는다. [로컬 배포·설치 검수 범위](../reports/ToolInventory/20261109_R17_LOCAL_DEPLOYMENT_APK_REVIEW.json)에 확인과 미확인을 구분했다. 전체 r17/공개 준비 완료 판정은 하지 않는다.

## 구성과 공개 범위

외부 휴대폰의 새 r17 네이티브 전송 기능이 **별도 파일 교환 TLS 서비스**에만 연결하는 구성을 제안한다. 기존 PC 편집기·관리 화면은 loopback에 유지하며 이 포트로 프록시하지 않는다. 서버는 허용한 작업 패키지 다운로드와 수정 결과 업로드/접수 확인만 제공한다. 원격 편집기·임의 파일 탐색·자동 프로젝트 덮어쓰기·명령 실행을 제공하지 않는다.

휴대폰이 받은 파일은 기존 오프라인 편집 흐름으로 연다. 업로드 완료는 PC 접수 성공이고, PC의 검사·차이 미리보기·명시 적용과는 별개다. r16 앱은 INTERNET 권한이 없으므로 이 설계로 곧바로 통신할 수 없다. 새 권한은 r17 후보에만 필요하며 WebView의 외부 탐색·리소스 차단을 유지하고 전송은 네이티브의 제한된 경로로 둔다.

## 1. 먼저 확인할 외부 도달 조건

[공유기 제조사 안내](https://www.tp-link.com/us/support/faq/1379/)는 인터넷 포트 전달에 공인 WAN 주소와 안정적인 내부 대상 주소가 필요하다고 설명한다. 이는 일반 NAT 원리 참고이며 다른 제조사/펌웨어의 버튼이나 동작을 보증하는 자료가 아니다. 공유기에 메뉴가 있다는 관찰만으로 외부 도달 성공을 판정하지 않는다.

- WAN과 외부에서 관찰한 출구 주소가 같고 공인 형식인지 확인한다. 사설 WAN·이중 NAT·통신사 CGNAT·ISP 수신 차단이면 단일 공유기 규칙만으로 도달하지 못할 수 있다. [RFC 6598](https://datatracker.ietf.org/doc/html/rfc6598)의 shared address space는 공인 직접 접속 주소로 취급하지 않는다.
- PC 내부 주소가 바뀌면 전달 대상도 어긋난다. 고정/예약이 필요한지 확인하되 이 학습에서 공유기나 Windows 설정을 바꾸지 않는다. 공인 주소가 현재 같아도 수신 허용·지속 고정·내부 NAT loopback 지원을 뜻하지 않는다.
- 별도 승인을 받은 실제 연결 단계에서만, 검증한 TLS 파일 서비스의 TCP 포트 하나와 대상 PC만 좁혀 연다. DMZ·SuperDMZ·UPnP 자동 개방·편집기/관리 포트 공개·라우터 원격 관리 공개는 사용하지 않는다. 방화벽 전체 해제는 하지 않는다.
- 외부 시험은 휴대폰 이동통신에서 실시하고 USB reverse·같은 Wi-Fi의 NAT loopback 성공과 구별한다. 접속 실패를 인증서 검증 해제·평문 전환·추가 중계 가입으로 해결하지 않는다.

총괄의 기존 읽기 보고에서는 포트 전달 메뉴·규칙 없음·DMZ 꺼짐·공인형 WAN과 출구 주소 일치가 관찰됐다. 작성자는 공유기에 접속하지 않았다. 이 보고는 설정 적용·서버 수신·실제 이동통신 연결 근거가 아니다. 실제 IP·MAC·SSID·계정·사진은 공용 기록에서 제외한다.

## 2. IPv4 주소와 인증서의 대응

새 계정 없는 첫 후보는 현재 IPv4의 `https` 주소와 **같은 IP의 SAN**이 있는 전용 자체 서명 서버 인증서다. URL의 호스트를 실제 IP로 고정하고 IP SAN의 일치를 정상 HTTPS 검증으로 확인한다. CN만 쓰거나 DNS SAN에 IP 문자열을 넣는 방식으로 대체하지 않는다. 구체 발급값은 비공개 페어링 데이터에만 둔다.

유동 공인 IP가 바뀌면 주소만 바꾸어 접속하지 않는다. 현재 IP SAN으로 인증서를 재발급하고 PC에서 확인한 새 인증서/주소를 USB·SAF의 명시 재페어링으로 배포한다. 기존 인증서 핀과 새 인증서는 달라야 하며 이전 자격증명을 폐기/회전할 수 있어야 한다. 재접속을 위해 hostname 검사를 끄거나 앱이 인터넷에서 새 핀을 자동 수락하지 않는다. DDNS 가입·새 도메인·고정 IP 구매는 전제하지 않는다.

## 3. 기존 JDK → Python SSL의 인증서 형식 경계

[JDK 17 keytool](https://docs.oracle.com/en/java/javase/17/docs/specs/man/keytool.html)은 키쌍·자체 서명 인증서와 SAN의 IP/DNS, serverAuth 등 확장을 다룬다. APK 서명키를 재사용하지 않고 TLS 전용 키/별칭/유효기간을 정한다. 명령행·채팅에 암호를 넣지 않고 지원되는 안전한 입력/비공개 암호 파일을 사용한다. 초기 학습 때는 생성 전이었으며, 후속 독립 검수에서 전용 TLS 키 생성·PEM 로드를 확인했다. 문서 작성자는 실행하지 않았다.

[Python 3.10 SSL](https://docs.python.org/3.10/library/ssl.html#ssl.SSLContext.load_cert_chain)의 `load_cert_chain`은 PEM 인증서와 대응 개인키를 읽는다. keytool의 PKCS12 파일을 그대로 넘기는 방식은 지원 경로가 아니다. OpenSSL 명령이 PATH에 없어도 Python의 ssl 모듈과 동일한 의미가 아니며, 별도 OpenSSL 설치를 자동 요청하지 않는다.

새 외부 의존성을 전제하지 않는 변환 후보:

1. 기존 JDK의 [KeyStore](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/security/KeyStore.html)로 명시한 PKCS12·별칭을 암호로 로드하고 해당 개인키·인증서만 읽는다. null·잘못된 암호·예상 외 키 타입이면 중단한다.
2. [Key.getFormat/getEncoded](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/security/Key.html)에서 인코딩 가능 여부와 `PKCS#8`을 확인한다. [Certificate.getEncoded](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/security/cert/Certificate.html)의 X.509 DER도 확인해 표준 PEM 블록으로 기록한다. keytool의 인증서 export는 개인키 export가 아니다.
3. 이 변환을 제작자가 구현한다면 기존 JDK/표준 API만 사용하는 작은 제품 빌드 단계로 검수한다. 작성자는 변환 도구를 만들거나 실행하지 않았다. 개인키 PEM은 공개 자료·APK·페어링/작업 파일·일반 다운로드/로그에 넣지 않는다. 인코딩이 평문 개인키라면 비공개 저장 보호가 필수이며 암호화 PEM 호환도 실제 검증 전 가정하지 않는다.
4. 기존 Python으로 PEM을 읽고 키/인증서 일치·유효기간·SAN·용도를 다시 확인한다. 별도 서버 컨텍스트의 TLS 설정·버전·협상도 시험해야 한다. 공식 API 지원과 이 PC의 실제 변환/SSL 성공은 별개다.

## 4. Android에서 정확한 인증서 고정

[Android 네트워크 보안 구성](https://developer.android.com/privacy-and-security/security-config)의 `<pin-set>`은 **SPKI 공개키 해시**다. 전체 DER 인증서 해시와 다르며 같은 키로 재발급한 인증서는 SPKI가 같을 수 있다. 또한 pin expiration 이후에는 고정이 해제되므로 이 설계의 fail-closed 정확한 인증서 고정을 대신하지 않는다. USB에서 가져온 인증서를 정적 XML에 자동 적용할 수 있다고 가정하지 않는다.

후보 검증 순서는 다음과 같다. 이는 공식 구성 요소를 조합한 적용 제안이며 구현 실기 전이다.

1. 페어링은 PC에서 확인한 IPv4·TLS 포트·공개 인증서 DER/PEM과 그 SHA256·서버/기기 식별·제한된 자격증명만 가진 버전 있는 파일을 사용자 확인 후 SAF로 연다. 서버 개인키는 포함하지 않는다. 크기·형식·알고리즘·인증서·endpoint를 엄격히 검사하고 임의 URL/파일 경로를 실행하지 않는다.
2. 그 페어링 하나의 인증서만 담은 앱 전용 신뢰 저장소로 검증기를 구성한다. TLS handshake의 서버 인증서 검증 단계에서 leaf DER의 SHA256을 로컬 핀과 정확히 대조하고, [유효기간 검사](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/security/cert/X509Certificate.html#checkValidity())·서버 용도·제한한 신뢰 경로 검증도 수행한다. 핀 불일치/만료/형식 오류는 예외로 중단한다. 단순히 해시만 저장하고 실제 연결에서 검사하지 않는 구현은 불가다.
3. [HttpsURLConnection의 인스턴스별 socket factory](https://developer.android.com/reference/javax/net/ssl/HttpsURLConnection)로 범위를 제한하고 표준 hostname/IP SAN 검증은 유지한다. 전역 trust store/factory 변경·아무 일도 하지 않는 TrustManager·항상 true인 HostnameVerifier를 사용하지 않는다. [Android TLS 지침](https://developer.android.com/privacy-and-security/security-ssl)은 trust-all을 임시 해결로도 쓰지 말라고 명시한다.
4. 자격증명/본문을 보내기 전에 handshake 검증이 끝나야 한다. 전송 후 인증서를 확인하는 방식은 늦다. [자동 redirect](https://developer.android.com/reference/java/net/HttpURLConnection#setInstanceFollowRedirects(boolean))는 인스턴스에서 끄고 모든 3xx를 실패로 처리한다. 다른 호스트·포트·평문으로 토큰을 전달하지 않는다.
5. 앱이 다른 PC/새 핀을 연결하려면 명시 로컬 재페어링을 요구한다. 앱의 인증서/토큰 교체가 기존 편집 초안을 지우지 않아야 한다. Android 시스템 CA 설치·사용자 인증서 전체 신뢰·보안 설정 변경은 필요 조건으로 삼지 않는다.

## 5. 기기별 자격증명과 파일 권한

[Python secrets](https://docs.python.org/3.10/library/secrets.html)의 안전한 난수로 충분한 길이(후보: 32바이트)의 기기별 opaque credential을 발급한다. 서버가 기기별 허용 작업·만료·폐기를 관리하고 비교는 `compare_digest` 같은 상수시간 API로 한다. 짧은 공용 PIN·HTML 안의 공용 토큰·IP 주소 자체를 인증으로 쓰지 않는다. 서버에는 가능하면 원문 대신 검증용 해시를 두고 원문·페어링 파일·클라이언트 저장·백업 정책을 별도로 보호한다. USB 페어링 파일에 든 credential도 비밀이므로 공개/공용 폴더에 남기지 않는다.

[OWASP REST 지침](https://cheatsheetseries.owasp.org/cheatsheets/REST_Security_Cheat_Sheet.html)에 따라 모든 파일 endpoint에서 인증과 대상 권한을 검사하고, 토큰은 URL/query/로그 대신 검증된 TLS의 요청 헤더로만 보낸다. 한 기기의 토큰으로 다른 기기의 작업/접수 파일을 읽지 못하게 한다. 탈취된 bearer는 폐기 전 사용될 수 있으므로 기기 폐기·재페어링·유출 시 즉시 revoke하는 PC 로컬 관리 경로가 필요하다. API key 하나가 민감한 자원의 모든 보호를 대신한다고 주장하지 않는다.

파일 서비스는 지정 ID와 서버가 만든 경로만 사용한다. 임의 디렉터리 목록·사진 전체 폴더·PC 경로·편집/관리 API·페어링/개인키 파일을 노출하지 않는다. 업로드 크기/멤버/해제·이미지 디코딩/연결 수/요청 시간/빈도·디스크 사용량을 제한한다. 잘못된 파일·중단된 수신은 비공개 임시 후보로 격리하고 기존 자료를 덮어쓰지 않는다. 업로드 접수 ID·실제 바이트 SHA·중복 처리 결과를 돌려주고, PC에서 기존 SHA/사진ID/baseRevision/미리보기·최종 재검사/락·원자적 적용을 유지한다.

## 6. 공개 전 구현 검수 조건

[OWASP TLS](https://cheatsheetseries.owasp.org/cheatsheets/Transport_Layer_Security_Cheat_Sheet.html)에 맞춰 TLS 1.3을 우선하고 필요 시 1.2 호환만 두며 구형 SSL/TLS는 거부한다. Python의 실제 SSL 빌드·암호군·버전·timeout·동시 요청 제한을 확인한다. [Python http.server](https://docs.python.org/3.10/library/http.server.html)는 production 권장을 하지 않으며 기본 보안 검사만 제공한다고 명시한다. 단순 정적 파일 서버에 인증서를 덧씌우는 것을 인터넷용 완성 서버로 간주하지 않는다. 구현 검수 전 공개 수신을 시작하지 않는다.

최소 시험은 정상 exact-cert/SAN/credential 다운로드·업로드와 함께 다음 실패를 포함한다: 다른 인증서·같은 키의 다른 DER 인증서·만료/미래 인증서·SAN 불일치·HTTP·redirect·누락/오류/폐기 토큰·타 기기 작업ID·허용 외 route/path·과대/손상/중복 파일·중간 연결 종료·느린 요청/동시 폭주·PC 수정 충돌. 실패 후 토큰/사진 미노출과 기존 초안/원본 불변을 확인한다. 이후에만 승인된 좁은 네트워크 설정을 적용하고 실제 이동통신 왕복을 별도 시험한다.

초기 학습 당시 인증서 생성·변환·pin handshake·credential 폐기·전송·외부 경로는 미검증이었다. 후속 shell fixture에서 제한한 native 전송·인증 거부가 확인됐다. 후속 Windows 로컬 키 생성/PEM 로드·표준 IP SAN/TLS1.3와 제한된 APK 설치는 위 실기 범위로 확인됐다. 설치 앱의 실제 pairing/송수신·라우터/방화벽·외부 이동통신·공개 서버 준비는 여전히 별도 미검증이다. [자료별 학습 범위](../reports/ExternalLearning/20261109_DIRECT_TLS_FILE_EXCHANGE_STUDY.json)를 참고한다.

## Android 런타임의 별도 격리 검수

[앱을 보존하는 네이티브 TLS 프로브](ANDROID_NATIVE_TLS_PROBE.md)는 기존 ADB/JDK/D8와 AOSP app_process 소스에 근거한 조건부 검수 경로다. 후속 독립 검수에서 S24 Android16 일반 shell의 AndroidOpenSSL/Conscrypt socket으로 fixture 11건이 통과했다. 정상 왕복·pin/기간 거부·pairing 사전 SAN 거부·인증/redirect 거부와 write 마감·소유 자산 정리가 확인됐다. 앱 패키지 환경·SAF/UI·실제 TLS SAN handshake 거부·이동통신·r17 전체 통과를 대신하지 않는다. [범위별 실기 기록](../reports/ToolInventory/20261109_ANDROID_NATIVE_TLS_PROBE_RUNTIME.json)에 검증 계층과 미검증을 나눴다.
