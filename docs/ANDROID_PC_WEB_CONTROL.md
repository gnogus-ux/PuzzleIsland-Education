# 안드로이드에서 PC 웹 편집기 조작하기

2026-11-09 공식 문서·지정 소스 학습 기록과 별도 담당의 제한된 도구 확인 보고를 구분한 재사용 매뉴얼이다. 문서 학습이나 실행 도움말 확인을 서버 공개·안드로이드 실기 성공으로 취급하지 않는다. [출처·실제 열람 범위](../reports/ExternalLearning/20261109_ANDROID_PC_WEB_CONTROL_STUDY.json)를 함께 확인한다.

## 목적과 적용 범위

PC가 사진·프로젝트·측정 결과를 저장하고 계산하며, 안드로이드 Chrome에서 같은 웹 편집기를 조작하는 구조를 다룬다. 사진/도면 위 점·선 편집, 화면 확대·이동, 입력·저장·내보내기와 보호된 외부 접속이 대상이다. 휴대폰 단독 계산 앱, PC 전체 원격제어, 생산 모델 자동 수정은 별도 작업이다.

기존 공용 [Chili3D 접속 매뉴얼](https://github.com/gnogus-ux/PuzzleIsland-Education/blob/main/docs/CHILI3D_LOCAL_CAD.md#외부-휴대폰-접속의-준비와-승인-경계)은 PC/휴대폰의 다른 localhost, 사설 HTTPS 접속, 정확한 Host 허용, 실제 이동통신 검증을 설명한다. 그러나 다중 터치 편집 상태와 VPN 없이 외부 접속하는 절차는 충분하지 않아 아래 공식 자료를 보강했다. 기존 앱의 저장 방식이 IndexedDB인지 PC 서버 파일인지 먼저 확인하며 Chili3D의 브라우저별 저장 특성을 모든 앱에 복제하지 않는다.

## 1. 터치 입력에서 확인한 원리

[MDN Pointer events](https://developer.mozilla.org/en-US/docs/Web/API/Pointer_events)는 마우스·펜·터치의 공통 입력 모델, pointerId, 취소·캡처와 touch-action을 설명한다. [Pinch zoom gestures](https://developer.mozilla.org/en-US/docs/Web/API/Pointer_events/Pinch_zoom_gestures)는 각 포인터의 상태를 보관하고 두 포인터 사이 거리 변화를 구분하는 예다. 예제의 배경색 변화는 개념 시연이며 완성된 사진 편집 변환기가 아니다.

적용 제안:

1. 활성 접촉을 pointerId별로 관리한다. 전역 drag 하나에 마지막 접촉을 덮어쓰지 않는다. 마우스의 보조 버튼은 기존 동작과 구별한다.
2. 이동/점 편집/새 점 배치 모드를 명시한다. 첫 손가락을 누른 즉시 새 점을 확정하면 뒤이어 들어오는 둘째 손가락이 잘못된 점을 남길 수 있다. 터치 탭의 확정 시점과 이동 문턱을 구분하고 두 손가락 진입 시 편집 후보를 취소하거나 복구한다.
3. 두 포인터가 활성일 때는 점 수정·새 점 배치를 정지하고 화면 변환만 수행한다. 거리 비율로 확대하고 두 점의 중심으로 이동한다. 화면 CSS 좌표를 사진 원본 좌표로 변환하며 확대·회전·레이아웃 변화 후 같은 사진 위치를 가리키는지 확인한다.
4. 한 손가락을 먼저 떼었을 때 남은 접촉을 즉시 새 점 편집으로 재해석하지 않는다. 이전 제스처를 종료하고 명시적인 새 접촉부터 편집을 재개하는 것이 단순한 안전 정책이다.
5. pointerup 외에도 pointercancel, lostpointercapture, 창 비활성화/페이지 숨김 등 중단 경로를 정리한다. 캡처된 포인터가 영역 밖으로 움직이는 것과 브라우저의 취소를 구별한다. 캡처는 특정 pointerId에 연결한다.
6. 캔버스의 touch-action 설정은 제스처가 시작되기 전에 지정한다. 직접 확대·이동을 구현하는 편집 영역에만 브라우저 기본 동작 제한을 적용하고, 문서 전체의 스크롤·확대·입력을 일괄 막지 않는다. 자동 스크롤과 화면 확대 버튼도 제공한다.

이는 구현 정책 제안이다. 취소 시 좌표를 원복할지, 편집을 미확인 초안으로 남길지는 앱의 명시 정책과 실행 취소 체계에 맞춰 정한다. 어떤 정책이든 취소로 확정·저장·이전 검수 승인이 뜻하지 않게 승계되면 안 된다.

## 2. 작은 화면과 정밀 조작

[W3C 2.5.8](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html)의 AA 기준은 원칙적으로 24×24 CSS px의 포인터 대상 또는 명시된 예외/간격이다. 이 숫자는 모든 모바일 버튼에 충분하다는 사용성 보증이 아니다. 같은 설명은 Enhanced 기준 44×44 CSS px도 구별한다. 모바일의 주요 저장·취소·선택·확대 버튼에는 44 CSS px 이상을 프로젝트 목표로 삼고 실제 손가락으로 검증하는 것이 적합하다. SVG 내부 좌표의 반지름을 고정하는 것만으로 화면상의 터치 크기가 일정해지지 않는다.

[W3C 2.5.7](https://www.w3.org/WAI/WCAG22/Understanding/dragging-movements.html)은 드래그 기능의 단일 포인터 비드래그 대안을 설명한다. 키보드 단축키만 추가하는 것으로 이를 대신하지 않는다. 점 목록에서 선택한 뒤 좌표 입력·상하좌우 미세 이동·확정/취소 버튼을 제공하면 손가락에 가려진 점을 정밀하게 조작할 수 있다. 밀집된 점은 후보 목록이나 선택 순환으로 모호성을 드러낸다.

세로/가로 화면, 작은 폭, 소프트 키보드가 열린 상태, 스크롤 후 고정 버튼 위치를 확인한다. 저장 버튼이 편집면을 가리거나 페이지 밖으로 나가면 배치를 조정한다. 화면 폭 에뮬레이션 통과와 실제 Android 입력·성능 통과를 따로 기록한다.

## 3. PC 연동의 저장·충돌 원칙

휴대폰에서 PC 서버에 접속하는 경우에도 저장 완료 여부를 응답으로 확인해야 한다. 화면만 바뀐 로컬 초안과 PC 저장본을 구별한다. 사진 SHA, 제품/부품 ID, 원본 픽셀 좌표, 단위·배율, 편집 revision과 확인 근거를 함께 유지한다. 두 기기가 같은 프로젝트를 열면 revision 충돌을 확인하고 오래된 화면이 최신 저장본을 덮어쓰지 않게 한다.

사진·기준선·점·분류·단위가 바뀌면 연결된 측정·모델 결과와 검수 확인을 재검토한다. 화면 확대·이동만으로 측정 좌표나 확인 상태가 바뀌면 안 된다. 네트워크 실패 후 저장 재시도에서 중복 작업이 생기지 않는지도 확인한다.

## 4. VPN 없이 외부에서 PC 웹 서비스에 접속하는 후보

현재 적용 목표는 VPN 없이 이동통신/외부 인터넷에서 휴대폰 브라우저로 PC의 특정 웹 앱에 접속하는 것이다. 기존 Tailscale 설치·접속 이력은 보존하고 사용하지 않는다는 범위다. [Tailscale Serve](https://tailscale.com/docs/features/tailscale-serve)는 tailnet 내부 서비스이며 공개 브라우저 접속과 같은 구성이 아니다. 따라서 기존 설치 이력만으로 이 목표를 달성했다고 하지 않는다.

[Cloudflare Quick Tunnels](https://developers.cloudflare.com/tunnel/get-started/quick-tunnels/)는 계정·도메인 없이 임시 trycloudflare URL을 만들 수 있다고 설명한다. PC에는 cloudflared가 필요하다. URL만 아는 사람이 접근할 수 있는 일반 Quick Tunnel과 이메일 인증을 요구하는 보호된 Quick Tunnel을 구분한다.

### 1차 검증 후보: 이메일로 제한한 Quick Tunnel

공식 문서의 명령 형태는 다음과 같다. 이는 예시이며 이 문서 학습에서는 실행하지 않았다. 사용자 이메일·실제 포트·호스트는 비공개 실행 기록에만 둔다.

```text
cloudflared tunnel --url http://localhost:PORT --allowed-mail USER_EMAIL
```

허용 이메일은 사용자가 지정한다. 방문자는 브라우저에서 이메일과 받은 일회용 PIN으로 인증하며 Cloudflare 계정은 필요하지 않다고 문서가 설명한다. PIN 입력·계정 인증은 사용자가 직접 한다. 실제 로그인 화면은 이번 학습에서 열거나 조작하지 않았다.

공식 제약은 임시 호스트명, 프로세스 종료 시 접속 종료, 재생성 시 호스트명 변경, uptime 보장 없음, 최대 동시 처리 200요청과 초과 시 429, SSE 미지원, 이메일 인증은 대화형 브라우저용이라는 점이다. 범용 API 클라이언트 인증이나 안정적인 상시 운영 주소로 확대하지 않는다. URL 변경 시 앱의 정확한 외부 원점도 갱신해야 한다.

### 구현 소스로 확인한 보호 범위

공식 [cloudflared 2026.10.7](https://github.com/cloudflare/cloudflared/releases/tag/2026.10.7)의 지정 파일을 읽었다. cmd/cloudflared/tunnel/cmd.go의 allowed-mail은 Quick Tunnel 전용이며 named tunnel과 함께 쓰면 거부된다. 인접한 2026.9.1과 2026.9.2의 같은 파일을 비교했을 때 2026.9.2에 해당 플래그가 나타나고 2026.9.1에는 없다. 공식 RELEASE_NOTES의 2026.9.2 구간도 이 기능 도입을 기록한다. 이는 문서/소스 버전 근거이며 현재 Windows EXE의 실행 확인은 아니다.

[proxy/proxy.go](https://github.com/cloudflare/cloudflared/blob/2026.10.7/proxy/proxy.go)는 보호된 HTTP 요청을 ingress 선택 전에 인증한다. [handler.go](https://github.com/cloudflare/cloudflared/blob/2026.10.7/quicktunnelauth/handler.go)는 유효 세션이 없는 GET/HEAD를 로그인으로 보내고 다른 메서드는 401로 처리하며, 유효 세션만 원본으로 진행시킨다. 따라서 사진 GET·다운로드와 POST API·업로드도 이 공통 HTTP 경로에서 보호하는 설계임을 확인했다. 모든 실제 앱 경로가 이 ingress를 통과하는지는 별도 실기로 확인한다.

[session.go](https://github.com/cloudflare/cloudflared/blob/2026.10.7/quicktunnelauth/session.go)의 브라우저 세션 쿠키는 host에 묶이고 Secure·HttpOnly·SameSite=Lax·Path=/를 사용한다. 서명된 세션은 broker 만료와 최대 4시간 중 짧은 시점에 끝나며 cloudflared 재시작 시 무효가 된다. [isolation.go](https://github.com/cloudflare/cloudflared/blob/2026.10.7/quicktunnelauth/isolation.go)는 인증 쿠키를 원본 요청에서 제거하고 비공개 캐시 정책을 유지한다. 이는 앱의 CSRF 토큰이나 작업별 사용자 확인과 다른 계층이다. 앱이 이 쿠키를 읽거나 자체 로그에 복사하도록 구현하지 않는다.

### 설치·계정·비용·상시 운영의 구분

[공식 Downloads](https://developers.cloudflare.com/cloudflare-one/networks/connectors/cloudflare-tunnel/downloads/)는 Windows 32/64비트 EXE/MSI를 제공한다. Windows 자동 업데이트가 없으므로 실제 설치 버전과 필요한 플래그의 help를 확인한다. 검토 시 최신 릴리스는 2026.10.7이며 [LICENSE](https://github.com/cloudflare/cloudflared/blob/2026.10.7/LICENSE)는 Apache-2.0이다. 소프트웨어 라이선스와 Cloudflare 서비스 약관·플랜은 별개다. 이 문서 학습 담당은 다운로드·설치·실행·결제·서비스 가입을 하지 않았다.

별도 실행 담당의 2026-11-09 초기 설치 보고를 대조했다. 사용자 개별 허용 후 공식 Windows amd64 2026.10.7 EXE를 프로젝트 전용 폴더에 포터블로 추가했고, 릴리스 SHA256 일치·Authenticode Valid 발행자 Cloudflare, Inc.·실제 version 및 tunnel help의 allowed-mail 옵션을 확인했다고 기록한다. 전역 PATH·Windows 서비스·방화벽 설정은 바꾸지 않았다. 초기 설치·도움말 확인과 아래 후속 연결 검증, PIN 인증·실제 휴대폰 사용을 각각 구분한다.

### 후속 제한 실기: 실제 앱의 익명 접근 차단

문서 학습 후 별도 Codex 검수 담당이 Windows의 실제 MAY 모바일 실행기와 지정 버전 cloudflared의 이메일 제한 옵션으로 외부 연결을 실행했다. 이 문서 게시 담당은 저장된 요청 결과를 읽고 대조했으며 앱·터널·브라우저를 새로 실행하지 않았다. [익명화한 도구 검증 기록](../reports/ToolInventory/20261109_CLOUDFLARED_PROTECTED_MAY_REVIEW.json)에 확인 범위를 남겼다.

선정한 HTML·상태 API·실제 사진·JSON/SVG 내보내기 5개 GET은 미인증 상태에서 정확한 공식 로그인 호스트로 302를 반환했다. 일부 GET에 앱 내부 토큰만 첨부해도 인증을 통과하지 못했다. 앱 토큰만 있는 외부 POST는 401이었다. 이는 Hello World만의 시험이 아니라 실제 앱의 선정 리소스 차단 확인이며, 전체 앱 경로·인증 후 사용·사진 업로드 성공을 보장하지 않는다.

앱의 공개 Host/Origin 연결은 별도 loopback 요청 7개로 확인했다. 일치하는 외부 조합은 허용하고, API의 top-navigation 예외 사용·null 원점·외부 Host와 로컬 원점 혼합·다른 원점은 거부했다. 앱 토큰 누락의 기존 계약은 401이므로 이 경우를 403으로 예상했던 검수 기대값만 바로잡아 한 사례를 재확인했으며 최초 결과는 보존했다. 프록시 인증과 앱 토큰·원점 검사는 서로 대체하지 않는다.

검수 담당은 시험을 콘솔로 중단한 뒤 소유 앱/중계 프로세스가 없고 서비스 리스너가 해제된 것을 확인했다고 보고했다. 그러나 저장된 실행 기록은 여전히 running으로 남았고 finally 완료 기록을 확인하지 못했다. 따라서 프로세스·리스너 해제와 종료 finalizer/상태 기록 성공을 구별하며, 정상 종료 기록까지 검증했다고 주장하지 않는다. 실제 PIN 인증, 안드로이드 이동통신 접속, 인증 후 앱 사용·편집·업로드·다운로드는 계속 미확인이다.

보통의 상시 hostname으로 게시하는 [정식 Tunnel 시작 문서](https://developers.cloudflare.com/tunnel/get-started/)는 Cloudflare 계정·Cloudflare에 연결한 도메인·cloudflared 실행 PC를 요구한다. [Access](https://developers.cloudflare.com/cloudflare-one/access-controls/applications/http-apps/)는 각 요청에 접근 정책을 적용하는 별도 계층이며 public-hostname 앱은 Cloudflare DNS 구성을 요구한다. Quick의 allowed-mail과 named+Access 설정을 혼동하지 않는다. 도메인 보유 여부, 새 계정/비용과 유지보수 조건을 확인한 뒤 정식 운영으로 전환한다. 서비스 가격·최신 플랜 조건은 실행 결정 시 공식 가격에서 다시 확인한다.

## 5. 원점·사진·업로드를 보호하는 앱 측 조건

[OWASP CSRF 설명](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html#using-standard-headers-to-verify-origin)은 브라우저 요청의 출처와 서버가 알고 있는 대상 원점을 비교하라고 설명한다. HTTPS나 인증 프록시를 붙였다는 이유로 앱의 기존 Host/Origin·CSRF 검사를 모두 해제하지 않는다.

- PC 웹 서버는 loopback을 유지한다. 기존 앱을 수정한다면 별도 후보에서 정확히 발급된 외부 HTTPS 원점만 설정한다. 예시 도메인 전체, 임의 하위 도메인, Origin:null을 허용하지 않는다.
- proxy의 전달 헤더는 신뢰할 연결/재작성 정책을 확인해야 한다. 헤더 존재만으로 사용자가 인증됐다고 판단하지 않는다. 프록시 앞·직접 loopback 등 각 진입 경로에서 허용/거부를 확인한다.
- 읽기 전용 GET으로 파일 삭제·확정·생성을 수행하지 않는다. 변경 API의 기존 CSRF 토큰·Origin 검사와 파일 경로 제한을 유지한다. 앱 내부 리소스 URL은 외부와 같은 원점의 상대 경로를 사용한다.
- 사진과 프로젝트가 앱과 외부 중계 사업자를 거쳐 전송되는 구조임을 사용자에게 알린다. 공개 문서·링크·로그에는 제품 사진, 인증 쿠키, PIN, 실사용 이메일·호스트명을 싣지 않는다. 제품별 경로/ID 접근 검증을 유지한다.
- [Cloudflare 413 문서](https://developers.cloudflare.com/support/troubleshooting/http-status-codes/4xx-client-error/error-413/)는 proxied-domain 요청 한도를 플랜별로 설명한다(검토 시 Free/Pro 100MB, Business 200MB). 이는 Quick Tunnel 전용 보장 수치가 아니다. 앱 자체 제한·multipart 여유·원본 사진 크기·중계 한도 중 작은 조건이 적용될 수 있다. 대표 사진으로 실제 업로드를 확인하고 413/시간 초과에서 원본을 보존한다. 자동 압축으로 원본을 덮어쓰지 않는다.

## 6. 구현 후 검사 순서

1. 설치 승인을 받은 뒤 공식 파일 버전·해시·실행 help와 allowed-mail 지원을 확인한다. 사용자 직접 PIN 인증 전에는 실제 세션 성공으로 기록하지 않는다.
2. 분리된 시험 서비스에서 미인증 화면/사진/API/다운로드가 거부되는지, 인증 후 같은 경로가 열리는지 대조한다. 임의 Host·다른 Origin·없거나 잘못된 앱 토큰도 거부되어야 한다.
3. 실제 휴대폰을 PC Wi-Fi에서 분리해 이동통신으로 접속한다. 첫 화면뿐 아니라 사진 표시·업로드·터치 편집·저장·재열기·다운로드를 확인한다.
4. 화면 확대/이동은 데이터 불변, 점/기준선 편집은 확인 해제, 두 손가락 진입·한 손가락 해제·취소는 오편집 없음, 취소 뒤 새 동작 재개가 정상인지 확인한다. 드래그 대안 버튼도 확인한다.
5. PC와 휴대폰에서 같은 revision을 열어 충돌 방지, 네트워크 끊김·복귀·저장 실패 표시, 브라우저 재열기 보존을 확인한다.
6. cloudflared/시험 서버의 소유 프로세스만 정상 종료하고 임시 URL과 세션 종료를 확인한다. 사용 중인 다른 서비스·기존 VPN·원본·전역 설정을 건드리지 않는다.

문서 학습, 소스 검토, PC 화면 에뮬레이션, 외부 HTTPS 응답, 실제 Android 실기와 제품 최종 승인은 각각 구분해 보고한다.
