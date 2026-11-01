# Scenario 엔진 자료 · Unity·Roblox 28개 색인

2026-11-01 · Unity14 + Roblox14 본문 6126행 전체 읽음. Godot14 + Unreal10은 다른 담당 범위이며 이 작성자의 읽음 수에 포함하지 않는다. 원작자의 macOS 시험/영상 분석 기록을 본인의 실행·시청 결과로 사용하지 않았다. 선택 references와 미검토 범위는 [학습 기록](../reports/ExternalLearning/20261101_SCENARIO_UNITY_ROBLOX_STUDY.json)에 있다.

Scenario Inc. MIT 자료를 한국어 요약·비평했다. 원 라이선스 본문은 `SCENARIO_UNITY_ROBLOX_WORKFLOW.md`에 보존했다.

## 01. scenario-roblox-animation

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/roblox/scenario-roblox-animation/SKILL.md) · 본문 1–212행 전체 읽음 · SHA-256 `42d7e234ac5730402dc58ebc8cc0fa580ce6257597dd1132c0cc74849bc8a367`

- 핵심·절차: 리그 종류·조인트 소유·Animator 우선순위/키 점유·마커·클립·IK·얼굴·임시ID를 분리한다.
- 검수: 자세표와 수치·양쪽 복제·원본 본 좌표·취소/루프·저장 전 Edit 자세 초기화를 확인한다.
- 한계·교정: Studio0.743/macOS의 원작자 시험값이다. 24fps/IK0.999/모든 R15 AnimationConstraint 단정은 전 리그 보편규칙이 아니며 마커는 서버 권한 검증을 대신하지 않는다.

## 02. scenario-roblox-architecture

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/roblox/scenario-roblox-architecture/SKILL.md) · 본문 1–244행 전체 읽음 · SHA-256 `da6700178645bb0fc0e52a6bad382a6fd4e94afbb7b1bb2b6a69d5a7b46c395c`

- 핵심·절차: 배치/RunContext·2단계 Init/Start·서버 정본/속성 미러·태그 Binder·연결 수명을 하나의 소유계약으로 구성한다.
- 검수: 중복 boot·yield Init·순환 require·태그 템플릿/재부모화·Deferred 제거·respawn GUI·속성과 remote 순서 경계를 확인한다.
- 한계·교정: one-entry와 코드생성 remote는 설계 선택이며 기존 Explorer 편집 방식을 금지하는 보편규칙이 아니다. 개별 Init 실패 후 의존 Start 진행·AutoUpdate 권장은 프로젝트 실패/버전정책과 대조해야 한다. 원문14live/8offline PASS는 본인 실행 결과가 아니다.

## 03. scenario-roblox-assets

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/roblox/scenario-roblox-assets/SKILL.md) · 본문 1–221행 전체 읽음 · SHA-256 `f6ca36ca2978d96eb8742964a3ea7b18f26083705b7989ecbf79241076c9ec7a`

- 핵심·절차: 생성 GLB를 원자료로 분류하고 크기/앞방향/원점/삼각형/구멍/PBR 분리·미리보기·착용·검증·정식 import를 나눈다.
- 검수: 원본/후보 실루엣·boundary/nonmanifold·실제 studs·부착점·타입별규격·저장/복제되는 미리보기 차이를 확인한다.
- 한계·교정: 두 생성 결과의 0.95단위/+Z/metal1 관찰을 모든 생성물로 일반화하지 않는다. 무조건 yaw180·metalness 이진화·1unit=1stud는 실제 변환/재질계약 확인이 우선이며 우리 메시 수정은 Guide 필수다.

## 04. scenario-roblox-data

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/roblox/scenario-roblox-data/SKILL.md) · 본문 1–212행 전체 읽음 · SHA-256 `6c9582bdc883522b516e493d1c15f8e6c99e6ccfb7e46c83a91886257d05f938`

- 핵심·절차: 세션 잠금·old기반 UpdateAsync·작업ID·키별 순서·저장 확인 receipt·migration 전 reconcile·미래버전거부·거래escrow를 분리한다.
- 검수: 실패 후 실제 저장 여부·중복 receipt·다중 서버/크래시 단계·과거 schema·live키 격리·teleport 재예약을 확인한다.
- 한계·교정: mock 성공은 실제 API/정책/다중서버 성공이 아니다.100개 receipt log의 보존범위·2프로필+trade-log 복구와 비용은 추가 설계대상이며 ProfileStore 교체/설치 승인이 아니다.

## 05. scenario-roblox-environment

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/roblox/scenario-roblox-environment/SKILL.md) · 본문 1–241행 전체 읽음 · SHA-256 `52154f2b8d3acc3088e8762b79d8b371fdbbbc010efef95389de561c022db69e`

- 핵심·절차: 스폰 카메라 기준 graybox·문통과·voxel 지형·MaterialVariant 링크/terrain override·태양방향·명암·실기 계측을 연결한다.
- 검수: 부피/실제 통과 질의·기준높이·풀침투·재질명·동일카메라 주야간·서버/클라이언트 streaming을 확인한다.
- 한계·교정: 10stud문/500draw/조명처방/픽셀 crushed 수치는 예시다. 후속viewport정지·scatter/streaming offline-only 경계를 보존하고 숫자만으로 좋은 조명/통행을 PASS하지 않는다.

## 06. scenario-roblox-expert

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/roblox/scenario-roblox-expert/SKILL.md) · 본문 1–241행 전체 읽음 · SHA-256 `6020cd6bf5be2c5ed258f558c00ccf5db9fb2cbad327cbe20c971f6cf9c11fae`

- 핵심·절차: 명시 대상 place·Edit/Play/Offline/Files 채널·파싱된 결과·고정카메라 전후·프레임예산·실제 저장/휘발을 구분한다.
- 검수: Spec총수>0·오류페이로드·원본/후보·창점유·실제저장·단일client와multiclient 경계·인계펜스를 확인한다.
- 한계·교정: macOS Studio0.743 전용 toolkit의36live/16offline은 원작자 결과다. 본문 never-close와close-as-soon 지시가 상충하므로 사용자/공통정책·점유계약 우선. 외부코드/신규창/앱조회/설치/유료API는 실행하지 않는다.

## 07. scenario-roblox-gameplay

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/roblox/scenario-roblox-gameplay/SKILL.md) · 본문 1–221행 전체 읽음 · SHA-256 `c88ecb31032aa66f49301ea1bca81e870c7f5435aac89a17ab46f425938fd457`

- 핵심·절차: 서버 intent·시작 overlap+이동 sweep·중복 캐릭터 hit 방지·NPC 단일스케줄/경로예산·hysteresis·차량 제약/소유권을 결합한다.
- 검수: pcall+pathStatus·막힌 다음 waypoint·stun때예약타격취소·빠른벽·실제입력·차량하차정지를 확인한다.
- 한계·교정: 실패 move를 waypoint로 snap해도 벽 관통/높이오류 가능성이 있으므로 재경로/안전검사 없이 일반화하지 않는다. trapezoid의 완전 프레임독립은 상수가속도 등 가정이 필요하고 two-player/touch/link 원문도 NOT_RUN이다.

## 08. scenario-roblox-luau

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/roblox/scenario-roblox-luau/SKILL.md) · 본문 1–224행 전체 읽음 · SHA-256 `a0a2f3b9f2fff0b6ecce25fe0e71b9f19d2afca6910a4cb832d6c13628afbb76`

- 핵심·절차: task scheduler·Deferred 이벤트·비양보 경계·명시 self 타입·Actor 병렬계산/직렬쓰기·정리·측정후 native/buffer를 구분한다.
- 검수: 양쪽 타입검사·누수 retained/slope·동일계산 A/B·SharedTable 원자갱신·주입 chunk의 별도 module cache를 확인한다.
- 한계·교정: task.spawn은 OS 병렬실행을 뜻하지 않지만 yield 뒤 논리적 동시진행은 가능하다. Actor마다 항상 고유VM/모든쓰기금지 같은 단정은 안전태그/API별 대조대상이며 원작자18core 속도를 본기기 성능으로 쓰지 않는다.

## 09. scenario-roblox-monetization

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/roblox/scenario-roblox-monetization/SKILL.md) · 본문 1–241행 전체 읽음 · SHA-256 `a1288661c447858984c70655091e2c8e58a38406e6de0ba81f3fbb6ab7fd5888`

- 핵심·절차: 서버 catalog/receipt·저장확인 지급·사용자별 엔진가격·공통확률표·권한·분석/실험 config를 나눈다.
- 검수: 중복/유실결제·저장실패·가격미로드·제한대상·기본config·실험가드레일·대시보드/출시경계를 확인한다.
- 한계·교정: 원문 수익화25~99Robux/기능유료화/광고제안은 사용자제품방침이 아니며 이번 학습에서 채택하지 않는다.100receipt 보존과 grant-before/after-save 표현은 데이터와 정산계약으로 해석, 최신정책/BindReceiptHandler·실결제미검증이다.

## 10. scenario-roblox-networking

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/roblox/scenario-roblox-networking/SKILL.md) · 본문 1–225행 전체 읽음 · SHA-256 `c54005b63056f209b2d4224768f327204b3e264e313fd8a0d26ca286d05e2ceb`

- 핵심·절차: rate→값/유한수/Instance경로→문맥검사·서버히트/이동검증·권한·복제/대역폭·탐지와제재를 분리한다.
- 검수: 악의/정상 대조군·벽/거리/시간·서버teleport grace·hostile Client·실제 honest 이동·지연/손실을 확인한다.
- 한계·교정: 지연rewind를 사용해도 움직이는문/커버의 이력정책이 필요하다. unreliable sent=accepted를 보편게이트로 삼지 않는다. honeypot하나로enforce 예시는 두독립사유정책과상충하며 자동제재/서버권위이관승인없음이다.

## 11. scenario-roblox-performance

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/roblox/scenario-roblox-performance/SKILL.md) · 본문 1–219행 전체 읽음 · SHA-256 `b88ad572c529fabcfa5493c12806af18fe3aff8e85d1fb5211d64488c6551ffc`

- 핵심·절차: 실제 아픈 Server/Client를 고정부하·동일시점·프레임별 프로파일로 찾고 장식복제·누수·streaming·출시복구를 나눈다.
- 검수: view별계측·움직이는카운터·반복수명뒤 rising floor·외부signal연결·실기폰·변경전후노이즈를 확인한다.
- 한계·교정: 폰CPU4배/500draw/1.3GB/5%노이즈/20초soak는 모든기기 보증이 아니다. 서버Tween 전면금지 대신권위/장식분리·실제트레이드오프를 판단하며 Studio와 device·출시상태는 별개다.

## 12. scenario-roblox-tooling

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/roblox/scenario-roblox-tooling/SKILL.md) · 본문 1–253행 전체 읽음 · SHA-256 `93b8cc4e965053e5b304f02672d5d382dd312e79d5ee4b9b73c9137ca8ad4c6f`

- 핵심·절차: 정본repo와builder map을 합치고 sync하나·핀도구·실패대조군·정적/엔진spec·Saved/Published·신선도/키권한·승인release를 구분한다.
- 검수: 빈 테스트/못읽은spec·sourcemap·dev코드유출·맵누락·이전baseVersion·secret로그·동시publish·실제복구를 확인한다.
- 한계·교정: 전체place 연속promote는 전역원자배포가 아니므로 구/신버전 공존schema호환과 부분실패 복구가 필요하다. macOSheadless pending·OpenCloud 무물리·live데이터접근 경계유지, 도구설치/allowlist/키변경/CI실행하지 않는다.

## 13. scenario-roblox-ui

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/roblox/scenario-roblox-ui/SKILL.md) · 본문 1–236행 전체 읽음 · SHA-256 `89b2ad748e9b243857affbbebe2bc60ee5a4d666cb047ce37eef0031bd106681`

- 핵심·절차: 한 UI트리·Scale/Offset/제약·Core safe area·StyleSheet 소유·입력context·persistentHUD·실측layout/번역을 연결한다.
- 검수: respawn·입력sink/복원·스타일실값·태블릿/phone회전·장치전환·focus/스크롤·긴번역·클릭한번한행동을 확인한다.
- 한계·교정: 9개 simulator와 Scriptable gamepad 테스트는 실폰/실패드동작 보장이 아니다.44px/11px·58px·우선순위숫자·globalUIScale 금지는 보편기준이 아니며 프로젝트가로방향/기존스타일 유지가 우선이다.

## 14. scenario-roblox-vfx-audio

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/roblox/scenario-roblox-vfx-audio/SKILL.md) · 본문 1–205행 전체 읽음 · SHA-256 `a76e44eee568fdc3cac008a97a4b864fe01ad18bf982eb3eb97716df20352a93`

- 핵심·절차: 권위게임결과와 client VFX·시간별잔상/정리·beam/trail·Audio graph/Wire/분석값·청취를 분리한다.
- 검수: 시작/정점/종료프레임·입자수명·중복/거리cull·서버장식0·wires/output/재생시계·발소리marker/fallback을 확인한다.
- 한계·교정: chord×2/3 cubic Bezier의 apex 일치는 정확한 원형반원 증명이 아니다.5개레이어/0.05초/LUFS값은예시. analyzer>0은 실제출력/믹스좋음의증거아니며 원문도사람청취미실행이다.

## 15. scenario-unity-2d

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unity/scenario-unity-2d/SKILL.md) · 본문 1–209행 전체 읽음 · SHA-256 `156a8dfb39552b57fa508e4becd0e8ce0f690f60feb3f18edd13ad01e260ba3c`

- 핵심·절차: PPU/import/픽셀카메라·atlas실제절약·RuleTile/충돌·2D광원batch·입력래치/고정스텝·낙하카메라·hitstop을 결합한다.
- 검수: 정지뿐아닌 subpixel pan·실제 light batch/fill·임계전후점프·airdrift·폭넓은화면·표현완료를 확인한다.
- 한계·교정: onePPU/무압축/스프라이트전이0/피해hitbox축소는 특정 pixel art/게임의선택이다. atlas가항상batch불변은아니고 예제결과로범위한정, URP17.3/CM3핀은 설치지시로실행하지 않는다.

## 16. scenario-unity-animation

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unity/scenario-unity-animation/SKILL.md) · 본문 1–205행 전체 읽음 · SHA-256 `da787e21b5b63cfc1a7fcc51b2fac43ab866230f66471f696cb48c12c7df3439`

- 핵심·절차: Humanoid import·clip역할/축별rootmotion·실속도 blendtree·mask/additive기준pose·constraint순서·CM/Timeline소유를 측정한다.
- 검수: 같은reference범위·idle drift/발미끄럼·중단전이·카메라장애/flip·cutscenemarker/handback·oneMove를 확인한다.
- 한계·교정: jump Y bake·rootmotion기본·idle별도state는 controller/clip에따른선택이며 모든리그규칙이아니다. lower layer는UI순서/인덱스명확화·가중/mask따라판정, 실제이관/패키지/아바타변경없음이다.

## 17. scenario-unity-architecture

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unity/scenario-unity-architecture/SKILL.md) · 본문 1–221행 전체 읽음 · SHA-256 `9d28a133b80b082b8c0782d485bea55585ecf188eded7b5e5ad995109a22d97c`

- 핵심·절차: SO정의/런타임state/file·domainreload/static·await소유토큰·event·rebind상태기계·asmdef·직렬화이름/merge를 경계에서 검증한다.
- 검수: secondPlay·Destroy/exit뒤작업·실player재시작저장·미래schema·binding취소/reset/복합충돌·클래스이동·merge역직렬화를 확인한다.
- 한계·교정: 토큰을 얻는 것만으로 임의Task/IO가 취소되는 것은 아니다. 역순리스너순회는임의중첩변경안전보장아님. SO파일불변은메모리불변아님, source6000.3.21/Input1.20실기와우리버전구분이다.

## 18. scenario-unity-expert

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unity/scenario-unity-expert/SKILL.md) · 본문 1–228행 전체 읽음 · SHA-256 `78078f24b8e56efdeba6a5b16e920755162f88ca6b7ceb71b4a3284ad65caf32`

- 핵심·절차: 프로젝트단일점유·batch/live/CLI/pipeline/test채널·결과envelope·직렬화/명시저장·target고정·수치+화면을 연결한다.
- 검수: compile오류/빈test·캡처white/pink/UI누락·build실산출물·같은camera/device·GUI미검증·낮은권한실패를 확인한다.
- 한계·교정: 원문macOS/AppleSilicon·CLIbeta/pipelineexperimental 설치검증은여기서실행하지 않았다. GUI경로 원문도NOT_RUN이며 설치/프로세스종료/라이선스조회/채널우회/새bridge제작의근거로쓰지않는다.

## 19. scenario-unity-gameplay

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unity/scenario-unity-gameplay/SKILL.md) · 본문 1–207행 전체 읽음 · SHA-256 `94fbd8c16b67fe9c21d609de1c64cfc1ab38bb9ef74414179b58c5d9be18b076`

- 핵심·절차: 고정스텝누적·실속도CCD/sweep·단일상태writer·저장된NavMesh/문질의·AI주기·측정후Jobs/DOTS·NGO범위·오디오믹서/voice를 나눈다.
- 검수: settings재시작readback·querybuffer포화·경로완전/계단·agent-animation일방향·대상수량p95/worst·실청취/넷코드원격동작을 확인한다.
- 한계·교정: CCD사다리/경로폭/2000개Jobs분기점은시험장치의예시다. ECS선택만으로결정성생기지않고 EditorNetSim은 NGO다중기기증거아님, feel은정지frames만으로확정불가다.

## 20. scenario-unity-mobile

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unity/scenario-unity-mobile/SKILL.md) · 본문 1–212행 전체 읽음 · SHA-256 `cda84d293fe8486b1aa742a58d639a084ba4abfd6ddc113682a1351c6a2d8f6a`

- 핵심·절차: 지속기기예산·실효압축·모바일URP tier·startup/pause·touchSafeArea·서명산출물·IAP/광고멱등처리를 분리한다.
- 검수: 실importformat·activeQuality·열정책복원·실기20분soak·멀티터치·중단·AAB/Xcode내부·중복/실패/pending구매를 확인한다.
- 한계·교정: 65%/ASTC전부/22kHz/수익낮은기기제외·광고간격은예시/상품정책이며채택승인아니다. syntheticthermal은정책검사일뿐실제열검증대체불가, API/store규정·SDK핀최신성·기기/결제미검증이다.

## 21. scenario-unity-performance

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unity/scenario-unity-performance/SKILL.md) · 본문 1–208행 전체 읽음 · SHA-256 `c08d102d29e0af1d9eba95f1812cec8dfbb4fb48d69a71f326f57f0662803f11`

- 핵심·절차: 병목thread/CPU-GPU·실developmentplayer·GCbytes/collection·GRD조건·원인marker·PSO/JIT·residentmemory·실출하크기를 분리한다.
- 검수: 같은time기반경로/기기·실draw>0·반복AB·GPUtrace·셰이더coverage·언로드/번들중복·p95/worst를 확인한다.
- 한계·교정: 1.5배예측/Editor메모리5배/0B/물리<=1step는보편보증아니다.50Hz물리+30fps는정상2step가능, firstlaunch폐기는cold-start문제별도기록필수·측정노이즈속정확counts단정도조건명시가필요하다.

## 22. scenario-unity-pipeline-automation

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unity/scenario-unity-pipeline-automation/SKILL.md) · 본문 1–213행 전체 읽음 · SHA-256 `272dfd61dc5382ac8ce58b563bea3011c8e085356c87b807594e7bf8e6eb42dd`

- 핵심·절차: import결정성/의존선언·정확대상Undo/저장·batchfinally·로딩조건별Addressables·refcount·target동일·컨텐츠검수/실player·cleanrelease출처를 연결한다.
- 검수: 2회실행불변·거부집계·UV/scale/재질화면·implicit중복·hardref·archive상태파일·총test수·bundle실언로드를 확인한다.
- 한계·교정: FBX All+ApplyTransform/512px/5000vertex는기본예시로모든자산정답아니다. clean tree는기존dirty삭제승인아님, 캐시purge/CI/라이선스/패키지설치·새자동화실행안했다.

## 23. scenario-unity-rendering-lighting

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unity/scenario-unity-rendering-lighting/SKILL.md) · 본문 1–197행 전체 읽음 · SHA-256 `60f08706141287db1ad0ad784ec89e1fc5f78b39399a028ec2a38843a4dd4edf`

- 핵심·절차: activeQuality의URP/volume계층·고정노출카드·광원/그림자거리·bake/UV·probes/reflection·등급별post/nativepass를 연결한다.
- 검수: 새process설정readback·동일camera단계·mixed4채널·leak/shadowmask·실gpu/device·최종tonemapper에서자료를 확인한다.
- 한계·교정: 회색후contrast증가/실내blue-red<=0/일괄각tier자산·고정bias·5%clipping은스타일/fixture한정이다. APV/lightmap비용을장치별상수로쓰지않고 M5Max실기를Windows/모바일검증으로옮기지 않는다.

## 24. scenario-unity-shaders

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unity/scenario-unity-shaders/SKILL.md) · 본문 1–223행 전체 읽음 · SHA-256 `c244c57e6d0ece9cd7c2b6b4c075f6112e69cfb573bb5244c82593bc31c5ec57`

- 핵심·절차: 실제URP소스/API·모든pass의clip/displace일치·lightloop·strip후variant·API별PSO·GPUms·RenderGraph의존을 검증한다.
- 검수: Forward/Depth/Normal/Shadow/Meta·추가방향광·역치끝값·엄격variant·cold/warm·물depth전제·투명/화면효과차이를 확인한다.
- 한계·교정: 원문workflow는dissolve1그림자gone, Qualitygate는restored라상충한다. shader_feature런타임toggle절대금지는과도하며보존variant/strip정책이핵심, rawDepthNormal도실제pipeline인코딩조건확인필요. GPU비용/73live는원작자결과다.

## 25. scenario-unity-ui

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unity/scenario-unity-ui/SKILL.md) · 본문 1–203행 전체 읽음 · SHA-256 `27ec1e8c5f84be7839e364101e6b9ed240d9d949a02456e1108fde8181570fbc`

- 핵심·절차: 기존uGUI/UITK선택·scaler실공식·canvas재생성/입력·양쪽layer/focus·font별glyph·binding숨김비용·실표현방식캡처를 나눈다.
- 검수: 긴언어/CJK·reference/safearea·숨겨진button포커스·양쪽시스템복귀·같은프레임layout·하위canvasdraw비용을 확인한다.
- 한계·교정: 모든화면same-shape/1batch/0panelchange·ContentFitter최상단만은목표/구조별조건이다. 미니맵frame이미지만자르면내부지도까지clip되지않으며 별도마스크/셰이더가필요하다.

## 26. scenario-unity-vfx

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unity/scenario-unity-vfx/SKILL.md) · 본문 1–209행 전체 읽음 · SHA-256 `de2edd8d77942b39c4d78ff21dd1c69bf108279730eefb1ef3ce9adf88d6bbab`

- 핵심·절차: 게임반경/수명과시각읽힘·mobile mesh-first·CustomData/stream계약·VFXGraph기능/읽기지연·시퀀스/FSE·최대동시수검수를 결합한다.
- 검수: clear+pool재생·다른seed·색공간·원근거리·게임종료뒤tail·Ncopycrowd·cull/capacity·실GPU/API를 확인한다.
- 한계·교정: 셰이더에서난수를못만든다는인용은부정확하며hash/seed기반의사난수는가능하다.100입자/512px/선형곡선금지·0.5초tail은디자인예시, always0blank자동검사는효과시작/끝빈화면을의도와대조해야 한다.

## 27. scenario-unity-web

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unity/scenario-unity-web/SKILL.md) · 본문 1–193행 전체 읽음 · SHA-256 `9a7797a68ec3171eca0cecea5ff0c3b53a30df0af93a08c3ce9b1b7254e64958`

- 핵심·절차: 실host압축/headers·첫playable까지bytes·wasm/heap·실graphicsAPI·JSbridge/keyboard·glyph·stripping·browserrelease를 분리한다.
- 검수: HTTPS/iframe·실network순서·audio첫탭·cold/warmcache·host별MIME/encoding·폰메모리·page입력·실로딩/UI를 확인한다.
- 한계·교정: Task.Run.Result hang관찰로모든ThreadPool API가항상동일hang이라일반화하지않는다. HTTP+Brotli는서버설정/브라우저조건별이며 SafariiframeIndexedDB전면불가/portal제한·최신WebGPU주장은미재확인이다.

## 28. scenario-unity-world-building

[고정 원문](https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unity/scenario-unity-world-building/SKILL.md) · 본문 1–203행 전체 읽음 · SHA-256 `5216908ef622930366c6c5f0b47b378a3a4304b2bc5e2016706d8fb8d66dd27e`

- 핵심·절차: 배우+카메라gym·grid접합·TerrainData선저장·결정적recipe·prefaboverride·전체바닥경로·가이드랜드마크·필요시stream·worstview를 연결한다.
- 검수: controller변경뒤gym갱신·slot/perimeter·문열림/닫힘·upperlink/roof·왕복도달·LODpop·Player통합/언로드·camera가림을 확인한다.
- 한계·교정: 문leaf bake제외는동적차단해결아니며 기존모듈러주의유지. noise항상erosion·해안항상콘텐츠/벽금지·2.5m는디자인예시, skip-worktree가원본보존/정상Git검수를대신하지않고 APV모든씬bake 원문NOT_RUN유지다.
