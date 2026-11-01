# Scenario 엔진 자료 · Unity·Roblox 학습 매뉴얼

2026-11-01 · 한국어 문서 학습본. [고정 원문](https://github.com/scenario-labs/skills/tree/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines)의 **Unity 14개와 Roblox 14개 SKILL 본문 전체, 6,126행·545,746바이트**를 읽고 재구성했다. Godot 14개·Unreal 10개는 다른 담당의 범위이며 이 작성자가 읽었다고 합산하지 않는다.

`SCENARIO_UNITY_ROBLOX_TOPIC_INDEX.md`에 28개 각각의 고정 출처·절차 핵심·검수·한계가 있다. [학습 기록](../reports/ExternalLearning/20261101_SCENARIO_UNITY_ROBLOX_STUDY.json)에는 파일별 SHA-256·실제 읽은 행·보충자료·미검토 파일과 다른 담당 범위가 있다. 선택 보충문서는 8개 전체와 루트 README 1~100행이다. 연결된 영상·스크린숏·시험 결과 파일·모든 소스코드를 전수 검토하지 않았다.

이번 작업은 문서 독해와 비교다. **외부 스크립트·검사기·CI·엔진·앱 조회·설치·설정·API·결제·출시는 모두 미실행**이다. 원문 SKILL에 적힌 명령을 작업 지시로 실행하지 않았다. 모델 가중치를 학습하거나 제품 기능을 추가한 것이 아니다.

## 1. 출처가 증명하는 범위를 먼저 구분한다

원문은 개념 설명뿐 아니라 원작자의 toolkit, 시험 결과, 영상의 타임스탬프, 검수 기준을 함께 제공한다. 이 자료를 재사용할 때 다음 다섯 층을 섞지 않는다.

| 층 | 사용할 수 있는 근거 | 이번 상태 |
|---|---|---|
| 문서 관찰 | 실제 읽은 주장·예제·내부 모순 | 28개 본문과 지정 보충자료 독해 완료 |
| 정적 추론 | 상태·예외·단위·실패 경로를 읽고 예상한 위험 | 색인과 교정표에 명시 |
| 원작자 시험 보고 | 원작자 기기·버전·fixture에서 관찰했다고 기록한 수치 | 작성자 보고로만 인용, 직접 재현 아님 |
| 현재 공식 지원 | 해당 버전의 공식 API·정책·설치 가능성 | 이번 신규 공식 웹 재대조는 NOT_RUN |
| 우리 제품 검증 | 실제 후보·엔진·빌드·기기·운영 시험 | 전부 NOT_RUN |

[Unity 계열 README](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unity/README.md)는 Unity `6000.3.21f1`·URP17.3·macOS Apple Silicon을 시험 환경으로 쓴다. 전화기 설치·상점 업로드·실결제/광고·Safari·실제 Actions runner·Accelerator 등은 미실행으로 명시한다. 본문 일부의 ‘모든 절차 실행’ 문장은 개별 NOT_RUN 예외와 함께 읽는다.

[Roblox 계열 README](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/roblox/README.md)는 Studio0.743·macOS의 미게시 로컬 place를 기준으로 한다. 실제 DataStore·공개 서버·다중 클라이언트·Team Create·폰/콘솔/VR·Windows·실결제는 미실행이다. 일부 최신 수정은 live 시험 뒤 **offline만 재검사**했다고 따로 적었다. 파일 수·그린 배지·‘97%’의 계획문 평가 점수를 완성 게임 품질 보증으로 바꾸지 않는다.

계열 README가 설명하듯 `tests/code/...`, `archive/tests/...` 등 일부 시험 경로는 원작자의 별도 build project에 있는 출처 표기이며 가져온 저장소에 포함되지 않을 수 있다. 파일이 없으면 결과를 직접 검증한 것처럼 쓰지 않는다. macOS 프로세스·GPU·창 제어 스크립트를 현재 Windows에서 검증된 도구로 취급하지 않는다.

## 2. 적용을 준비하는 공통 순서

1. 기존 프로젝트의 승인 원본·가이드·엔진/패키지·화면 방향·디자인·담당 시스템과 정본을 고정한다. 원문의 새 프로젝트 기본값을 기존 제품에 덮지 않는다.
2. 현재 허용된 공용 프로그램 목록과 문서를 먼저 사용한다. toolkit을 읽었다고 설치된 것이 아니다. 없는 프로그램이나 부족한 버전 근거는 주제·목적·부족한 점을 밝혀 요청한다. 이미 승인된 문서 학습은 계속한다.
3. 문제를 최소 재현, 기대 결과, 바꿀 수 있는 범위와 보존 경계로 적는다. 메시·형태를 바꾸려면 실제 Guide를 먼저 만들고 원본을 보존한다.
4. 본문·보충자료에서 관찰한 원리와 프로젝트 적용 제안을 구분한다. 예시 상수·기본 UI·경제·이동 방식은 승인된 설계가 아니다.
5. 구현이 별도 승인되면 정적 검수→규칙 fixture→엔진→실제 대상 빌드/기기 순으로 확인한다. 빈 시험·결과 없는 종료·정지한 카운터·잘못된 창의 캡처는 성공 근거가 아니다.
6. 변경 전후를 같은 장면·카메라·기기·부하·시점으로 비교한다. 수치와 실제 화면/조작을 함께 읽고 실패·미실행을 남긴다.
7. 저장 상태·후보 경로·버전·열린 문제·증거를 인계하고 실제 인수를 구분한다. 게시 담당만 공용 자료실을 변경한다.

원문의 doctor·preflight·앱 목록·라이선스 검사·자동 설치·새 bridge·창 생성/종료·키/권한 변경·업로드·결제는 이번 학습에 실행하지 않았다. 설치/설정 보류 및 금지 앱 조회 제한을 유지한다.

## 3. Unity: 상태·입력·저장부터 제작까지

### 수명·입력·저장

SO는 콘텐츠 정의, 순수 C#은 세션 상태, 버전 파일은 영속 상태를 맡게 설계할 수 있다. 파일 해시가 같아도 Play 중 SO 메모리가 바뀔 수 있으므로 디스크 불변과 메모리 불변을 구분한다. domain reload를 끈 두 번째 Play, static 이벤트 중복, 씬 재입장, prefab 단독 배치를 경계 사례로 둔다.

await에는 객체/서비스/앱 수명의 소유자를 정한다. 토큰을 얻기만 해서는 임의 Task·IO가 취소되지 않는다. 실제 기다리는 작업에 전달하고 취소 뒤 늦은 callback이 상태를 다시 쓰지 못하게 한다. Awaitable 재사용, Unity fake-null, 메인 스레드 접근을 별도로 검수한다. Development에서 탐지된 오류가 Release에서 안 보인다고 안전해진 것이 아니다.

재매핑은 Action 비활성→대기→완료/취소→원래 활성 상태 복원→저장의 흐름이다. Escape 취소, 복합 바인딩의 각 part, effectivePath 충돌, modifier 단축키, JSON override의 덮기/레이어링과 Reset All의 저장 삭제 정책을 정한다. 여러 generated input asset을 만들면 한 화면의 변경이 다른 소비자에게 안 보일 수 있다.

저장은 schema·ID·revision·백업·복구와 실제 Player 재시작으로 확인한다. 원문의 예제 SaveService가 있다는 것과 현재 프로젝트 저장에 적합하다는 것은 다르다. 기존 저장 파일·키·경제 계약을 임의 변경하지 않는다.

### 2D·애니메이션·카메라

픽셀아트는 PPU·필터·압축·pivot·카메라·움직임이 하나의 계약이다. 정지 화면만 보지 말고 subpixel pan과 실제 조작 중 흔들림을 확인한다. 아틀라스는 텍스처 전환·메모리·배치 중 어떤 비용을 줄였는지 측정한다. 원문 fixture에서 Batches가 같았다는 이유로 모든 아틀라스가 draw call을 줄이지 못한다고 일반화하지 않는다.

2D 광원은 sorting layer별 light batch·fill·normal/shadow 비용을 함께 본다. 플랫폼 controller는 입력 래치·고정 스텝·버퍼/코요테 소비를 나누고 점프 방법·공중 마찰을 실제 레벨에 맞춰 선택한다. 원문 16PPU·무압축·전이0·피해 판정 축소는 특정 스타일/게임의 선택이다.

3D 애니메이션은 avatar·clip 역할·축별 root motion·mask·additive 기준 pose·transition/constraint 순서를 계약으로 정한다. 이동 속도와 clip 평균 속도를 대조해 foot slide를 확인한다. 카메라 Brain·CM rig·Timeline 중 현재 소유자를 정하고 cutscene 종료 뒤 조작/카메라 handback을 시험한다. import 규칙은 지정 폴더에만 적용하고 기존 rig/가이드/동작 범위를 확대하지 않는다.

### 게임플레이·월드

상태마다 writer는 하나다. NavMeshAgent와 물리 바디, root motion이 같은 위치를 동시에 쓰지 않게 한다. 경로는 bake 결과의 존재뿐 아니라 실제 문·계단·층간 이동·닫힌 장애물·왕복 통과로 확인한다. pathStatus·목표 유효성·실패/도착을 구분한다.

물리는 정상 고정 스텝과 과도한 catch-up을 구분한다. timestep 상한을 줄여 프레임을 안정시킬 때 게임 시간이 느려지는 교환 조건을 기록한다. CCD는 실제 속도·벽 두께·상대 운동으로 시험하고 필요할 때 형상 sweep과 시작 overlap를 사용한다. NonAlloc은 count만 순회하며 버퍼 포화를 누락 없는 결과로 오인하지 않는다.

월드는 배우와 카메라 치수의 gym→접합 규격→블록아웃→조립→경로/시야→디테일 순으로 다룬다. grid 정렬이 맞아도 같은 slot 중복·누락 벽·잘못된 prefab override는 남을 수 있다. TerrainData 저장·생성 recipe·순서·seed·규칙 버전을 보존하고 실제 재개/재생성을 확인한다. stream은 메모리 필요로 결정하며 unload·중복 load·활성화 대기·proxy·빛/경로 소유권을 함께 설계한다.

### 렌더링·셰이더·VFX

실제로 활성화된 Quality의 URP asset과 renderer·volume 계층부터 확인한다. 동일 카메라에서 노출/카드→광원→bake→reflection/leak→최종 grading을 비교한다. 회색 카드·clipping 수치만으로 예술적 목표를 확정하지 않는다. 주야간·실내의 색을 원문 고정 recipe로 교체하지 않는다.

셰이더는 실제 설치된 URP의 keyword·pass·인코딩을 기준으로 한다. forward/depth/normal/shadow/meta에서 clip·displacement가 일치하는지 확인한다. 빌드에 남은 variant, API별 PSO, cold/warm 실행과 GPU 시간은 각각의 증거다. shader_feature는 런타임 변경이 문법적으로 불가능한 것이 아니라 필요한 variant의 보존/stripping이 핵심이다.

VFX는 게임 반경·판정 시간·중요도·최악 동시 수와 연결한다. 같은 효과의 시작/정점/종료를 보고 N개 겹침·fill/overdraw·pool/잔여 인스턴스를 검사한다. Custom Data와 vertex stream 순서, 선형 데이터 텍스처, VFX Graph의 capacity/bounds/지연된 readback을 확인한다. 모든 빈 프레임이 오류는 아니며 의도된 시작 전/종료 후는 기대 결과와 대조한다.

### UI·성능·파이프라인·대상 플랫폼

기존 uGUI/UITK를 우선하고 혼용 시 레이어 표·focus 왕복·EventSystem 소유자를 정한다. 표시를 꺼도 숨은 버튼이 선택되는지 확인한다. TMP와 UITK의 폰트 체인은 별개이며 한국어/긴 번역·확대 텍스트를 각각 검사한다. 카메라에 Overlay UI가 안 잡히면 실제 표현 경로로 캡처해야 한다. 모든 화면에서 같은 composition이나 1 batch가 필수인 것은 아니다.

성능은 병목 thread·GPU·GC/메모리·로딩을 구분하고 동일 경로 A/B를 반복한다. Editor 계측은 반복 개선의 자료, 실제 대상 Player는 판정의 근거다. GRD·SRP Batcher·MaterialPropertyBlock·render path의 조건을 현재 버전으로 확인한다. 신규 ECS 전환이나 아트 품질/AI 주기 변경은 별도 설계 결정이다.

import 규칙은 범위를 좁히고 의존성을 선언한다. Undo는 실제 변경 component에 기록하고 prefab override·dirty·save를 각각 다룬다. Addressables는 동시에 로드할 조건과 shared dependency로 구성하고 hard reference·bundle 중복·release 후 실제 unload를 검수한다. clean tree 요구를 기존 사용자 dirty 삭제로 해결하지 않는다.

모바일은 실효 GPU 압축·active Quality·실제 Safe Area/멀티터치·중단 복귀·지속 열/메모리·서명된 최종 산출물을 본다. synthetic thermal은 조정 정책의 논리 시험이며 실기 soak가 아니다. IAP·광고는 중복 transaction·pending 복구·실패 confirm·정상 영수증·저장된 지급을 나누며 새 결제 기능을 승인한 것으로 취급하지 않는다.

Web은 실제 host의 MIME/encoding·HTTPS/iframe·첫 playable까지 bytes·실 graphics API·heap·오디오 첫 입력·page/game 키보드·폰트를 확인한다. 로컬 headless Chrome 성공이 Safari·실폰·portal 배포 성공은 아니다. cold-start와 warm-cache 성능을 따로 남긴다. 정책·상점 제한·목표 API·SDK/패키지 버전은 최신 공식 대조 후 채택해야 한다.

## 4. Roblox: 서버 정본과 교체되는 수명

### 아키텍처·Luau·네트워크

Script 배치와 RunContext를 함께 확인한다. Init에서 자신의 상태/구독을 준비하고 Start에서 의존 시스템을 사용하도록 나눌 수 있지만 one-entry·새 loader·코드 생성 remote는 특정 설계 선택이다. 기존 구조를 먼저 찾고 중복 부팅·순환 require·같은 기능 두 번 실행을 피한다.

Player·Character·GUI·round/map·tool의 수명을 각각 정한다. 태그는 템플릿도 찾을 수 있으므로 허용 ancestor와 이동/제거를 함께 본다. Deferred 이벤트에서 제거된 Parent를 읽지 않게 필요한 상태를 보존하고 handler/connection을 생성 시점부터 소유자에게 묶는다. task.spawn은 OS 병렬이 아니지만 yield 이후 논리적 동시 진행은 가능하다. yield 사이의 불변식을 보호한다.

클라이언트는 ID/행동 의도를 보내고 서버가 가격·피해·자격을 결정한다. rate→값/유한수/크기/Instance 경로→상태/거리/권한 순으로 좁혀 확인할 수 있다. prompts·touch·click도 신뢰 경계다. 물리 network owner가 판정 권한을 얻는 것은 아니다. 실제 정상 입력이 작동하는 대조군과 악의 입력에서 상태가 바뀌지 않는 사례를 함께 시험한다.

server authority 도입은 fixed simulation·입력·streaming·예측/롤백까지 영향을 미치는 별도 전환이다. 원문의 honeypot·제재 점수·무작위 지연을 그대로 제품 정책으로 채택하지 않는다. lag rewind는 문/움직이는 cover의 상태 이력도 요구할 수 있다. unreliable transport는 손실을 허용하므로 모든 발송 수와 수신 수가 같아야 한다는 범용 완료 기준과 맞지 않는다.

### 저장·결제·거래의 실패 대응

GameDev의 단순 UpdateAsync 예제가 부족했던 세션 충돌을 Scenario 자료는 명시적으로 다룬다. old 데이터·세션 잠금·작업 ID·키별 순서·저장 확인을 따로 둔다. 실패 응답 뒤에도 쓰기가 실제 반영됐을 수 있으므로 같은 지급을 반복하기 전에 결과를 확인한다.

schema migration은 Reconcile이 버전 필드를 채우기 전에 실행한다. 미래 schema는 읽자마자 낮은 버전으로 저장하지 않는다. 원작자의 mock은 ghost write·conflict·crash·시계 차이를 주입하지만 실제 DataStore 가용성·한도·두 공개 서버의 인수 성공은 별도다.

receipt는 하나의 서버 담당이 수신하고 PurchaseId/transaction의 처리 중·현재 데이터·확정 저장 상태를 구분한다. UI의 구매 완료 안내가 지급 근거는 아니다. 제한된 100개 receipt·50개 operation 기록은 오래된 재전송까지 영구적으로 중복 제거한다고 주장할 수 없다. 보존 기간·미정산 건·추가 원장 정책이 필요하다.

두 profile을 연속 저장해도 원자 거래가 아니다. escrow와 단일 trade-log 결정으로 회복하는 방식을 배웠으나 소유권·저장 확정·중단 단계·재접속·동시 복구를 실제로 검수해야 한다. 정책 API 실패·저장 불가를 조용히 live 메모리 저장으로 전환하지 않는다. 특히 procedures의 일반 `403` 문자열→mock 분기는 미게시/테스트 환경을 명시적으로 제한하지 않으면 권한 오류를 잘못 분류할 여지가 있다.

원문 restore 예시는 잠금 여부를 읽고 나중에 SetAsync하는 구조다. 두 시점 사이에 새 세션이 시작되는 경합까지 원자적으로 막았다는 증거는 없으므로 운영 복구를 바로 실행하지 않는다. 우리 저장/계정/거래/삭제·상점은 이번에 변경하지 않았다.

### 자산·애니메이션·환경·UI·VFX

AI GLB는 결함을 측정할 원자료다. 실치수·앞방향·pivot·형상/노멀·boundary/nonmanifold·재질 채널·형식/업로드 규격을 분리한다. 두 생성 예시의 +Z·단위 크기·metal1 관찰을 모든 생성물의 특성으로 취급하지 않는다. 무조건 yaw180이나 metalness 이진화로 고치지 말고 실제 source/destination 변환과 원본 재질 의도를 확인한다.

session EditableMesh 미리보기·저장 파일·play 복사본·실제 게시 자산은 서로 다르다. UGC 로컬 규격 검사와 업로드 소유권/심사까지 구분한다. 지금은 실제 preview·import·upload·메시 수정 모두 미실행이다.

리그는 실제 joint class·Animator 생성/재생 주체·priority와 keyed joint·marker·IK/face·publish owner를 확인한다. marker는 표현 타이밍이며 서버의 합법성 검증을 대신하지 않는다. 원문 24fps·IK0.999·동적 head 처방은 해당 시험 사례다.

환경은 spawn view와 실제 통로에서 graybox·충돌·지형 높이·material name/override·태양 방향·주야간 가독성을 검수한다. bounding-box overlap가 열린 문을 막혔다고 볼 수 있음을 구분하고 실제 형상/통과/플레이를 확인한다. 원문 Default/Hull/Precise 명칭만으로 모든 구멍의 충돌을 판정하지 않는다.

UI는 한 source tree를 화면·장치에 맞춰 적응시키고 safe inset·core touch controls·입력 context·persistent HUD·스타일 소유·번역·focus 복원을 본다. 9개 device simulator와 Scriptable gamepad는 실폰/실패드 시험이 아니다. 44px/11px/58px·원문 Sensor 방향을 현재 제품의 가로 UI 기준으로 복사하지 않는다.

VFX는 서버 결과를 필요한 client가 표시하고 거리 cull·반복/종료 정리를 소유한다. Audio는 Wire/graph·출력 경로·재생 시계·analyzer와 실제 청취를 분리한다. RMS가 0보다 크다는 사실이 실제 스피커 출력이나 좋은 믹스를 증명하지 않는다. cubic Bezier의 midpoint/apex가 맞아도 정확한 원형 반원이라는 증명은 아니다.

### 성능·도구·배포 경계

실제로 느린 Server/Client의 동일 부하·시점·장면에서 ms/frame과 상승하는 메모리 바닥을 본다. 외부 signal이 closure로 파괴된 객체를 붙잡는지 확인한다. Studio 메모리·정지된 render counter·18코어 Mac의 속도를 실폰 성능으로 옮기지 않는다. 500 draw·1.3GB·폰4배 등의 예산은 출처의 기기/목표 예시다.

Rojo/Script Sync의 정본 범위를 정하고 둘이 같은 폴더를 쓰지 않게 한다. builder base map과 code build를 합칠 때 누락·덮어쓰기·오래된 baseVersion을 검수한다. Saved/Published·restart·rollback은 별도 상태다. 모든 place를 차례로 promote해도 전역 원자 배포가 아니므로 구/신 서버 공존과 부분 실패 복구를 설계해야 한다. 키 생성·권한·공개·재시작은 이번 문서 학습에서 실행하지 않았다.

## 5. 내부 불일치와 적용 한계

아래는 원문 독해에 근거한 교정/검증 질문이며 이번 실행 재현 결과가 아니다.

| 항목 | 관찰/추론 | 적용 기준 |
|---|---|---|
| Roblox 창 종료 | expert의 never-close와 close-as-soon 문장 상충 | 사용자·공통 점유/인계 규칙 우선, 이번 창 작업 없음 |
| 검증 경로 | README와 세부 본문의 live 수·후속 offline 범위가 다름 | 가장 구체적인 범위/날짜를 유지, 합계로 과장하지 않기 |
| Unity dissolve | workflow는 threshold1 shadow gone, quality gate는 restored | 효과의 승인된 의미·정확한 threshold 정의를 먼저 고정 |
| Unity physics | 성능 gate <=1step은 50Hz 물리/30fps의 정상 다중 step과 맞지 않음 | 설정된 simulation/render 주기의 정상 분포로 판정 |
| shader_feature | runtime toggle ‘절대 금지’ 표현 과도 | 필요한 variant의 빌드 보존·엄격 matching·실행 확인 |
| VFX 난수 | ‘shader에서 난수를 못 만든다’ 인용 부정확 | hash/seed 의사난수 가능, 결정성·변동 단위를 계약 |
| Unity UI | pre-cut 미니맵 frame만으로 지도 clipping 보장 불가 | 내부 지도 마스크/셰이더·실제 화면을 확인 |
| 이벤트 채널 | 역순 List만으로 임의 리스너 변경/재진입 보장 불가 | 발송 중 변경·snapshot·지연 변경 등 명시 계약 |
| Roblox mock 선택 | general403을 미게시로 분류할 위험 | 테스트 환경 명시, 운영 오류에서 memory fallback 금지 |
| restore | 잠금 조회와 강제 덮어쓰기 사이 경합 가능성 | 세션 차단/원자적 권한 확인·운영 복구 절차 검토 |
| 네트워크 제재 | 두 독립 사유 원칙과 honeypot1회 enforcement 예시 상충 | 정책·오탐·검토 권한을 별도 결정, 자동 채택 안 함 |
| 성능 | first launch 폐기는 cold-start 문제를 숨길 수 있음 | cold/warm 별도 기록, 반복 성능과 첫 사용자 경험 분리 |
| 시각 수치 | clipping·uniform·difference 검사가 미학/실제 조작 대체 불가 | 동일 조건 화면·행동·기기와 함께 판정 |
| 계정/규격 | 상점·API한도·폐기 버전·키/정책은 시간에 민감 | 최신 공식 근거 재확인 전 원문 당시 주장으로 표시 |

## 6. 기존 공용 교육과의 대조

GameDev78 학습 때 실제 본문을 읽은 기존 Match3 5개·모듈러 3개와 이번 내용을 이어 비교했다. 해당 문서가 학습한 영상을 이번 담당이 다시 보았다고 합산하지 않는다.

| 기존 자료 | 보강점 | 유지할 경계 |
|---|---|---|
| MATCH3_WORKFLOW / BOARD_INPUT | 입력 asset·rebind·수명·second Play·focus | 기존 명령/좌표/PRNG 불변·해결 소유자 유지 |
| MATCH3_RESOLUTION_SPECIALS | 늦은 await/애니 완료·pool·VFX 종료의 소유권 | 특수 생성·장애물·구간 중력은 기존 문서가 더 상세 |
| MATCH3_LEVEL_SAVE_QA | ghost write·revision/세션·migration 순서·저장 확정 | 고유 거래·안정 스냅샷·손상 복구 원칙, 새 유료 기능 없음 |
| MATCH3_UNITY6_COMPATIBILITY | 실제 package 조건·엔진/Player 차이 확인 질문 | 6000.3.27f1 대상과 원문6000.3.21f1 구분, 공식 웹 대기/실기미실행을 PASS로 바꾸지 않음 |
| MODULAR_MAP_GRID_KIT | gym·slot/perimeter·prefab override·recipe | 승인 치수·원점·접합·Guide 보존, 2.5m 등 예시 혼합 금지 |
| MODULAR_MAP_PLAYABILITY_QA | whole-floor/왕복·카메라 통과·불완전 경로·stream | 문 leaf bake 제외만으로 동적 문/다리 상태가 해결되지 않음 |
| MODULAR_MAP_BLENDER_UNITY | import 결정성·재수출·PBR/variant·Player 부하 | GUID/Prefab·실크기·색 공간·실루엣 유지, 실제 왕복 시험 미실행 |

GameDev는 여러 엔진의 기본 계약을 짧게 안내하고 Scenario는 toolkit·fixture·수치·검수표를 깊게 제공한다. 더 상세한 자료라도 예제 숫자를 제품 규칙으로 만드는 것은 별도 판단이다. 기존 Match3의 run/그룹·특수 연쇄·실패 복구 내용을 외부 일반 장르 예제로 대체하지 않는다.

## 7. 후속 적용과 완료 보고

후속 제작 인계는 `승인 범위 · 정본/후보 · 버전/패키지 · 설정/규칙/schema · 재현 · 기대 · 실제 관찰 · 증거 · PASS/FAIL/NOT_RUN · 남은 문제 · 다음 담당`을 포함한다. 도구가 없거나 막히면 새 도구를 임의 제작/설치하지 않고 부족한 프로그램·용도·계정/비용 필요를 요청한다.

현재 완료 범위는 **Unity·Roblox 28개 본문 독해, 선택 보충자료 검토, 한국어 매뉴얼·색인·행/해시 기록 작성**이다. Godot·Unreal 24개는 다른 담당 범위로 남기며 아직 실제 완료됐다고 이 문서가 주장하지 않는다. 원문 코드를 실행하거나 우리 엔진·게임·기기·서비스를 검증하지 않았다. 공용 게시·커밋·푸시는 단일 게시 담당에게 인계한다.

## 출처와 이용 조건

Scenario Inc.의 MIT 자료를 요약·비평했다. 아래 원문 LICENSE를 보존한다. 연결된 강좌·타사 에셋·음원·SDK의 권리는 각각 다르며 문서 라이선스를 그 원자료의 재배포 허가로 확대하지 않는다.

```text
MIT License

Copyright (c) 2026 Scenario Inc.

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
