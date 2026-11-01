# Unreal 10주제 · 문서 기반 제작·인계·검수 매뉴얼

2026-11-01. Scenario Labs [고정 원본](https://github.com/scenario-labs/skills/tree/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unreal)의 SKILL 본문 10개를 전부 읽고 정리했다. 총 **2,172행·212,243바이트**, MIT. [10주제 색인](SCENARIO_UNREAL_SKILLS_INDEX.md) · [파일별 읽기·해시 기록](../reports/ExternalLearning/20261101_SCENARIO_UNREAL_SKILLS_STUDY.json)

**원문 자체가 2026-09-24 상태에서 Unreal 미설치와 엔진 호출 미실행을 명시한다.** 오프라인 synthetic capture·fake `unreal`·순수 Python 테스트 통과는 엔진 실행 증거가 아니다. 여기서도 Unreal·앱·MCP·API·제공 코드·테스트·설치·빌드를 실행하지 않았다. 원문의 UE 5.8/macOS Apple Silicon 대상 예시를 현행 공식 문서 재검증이나 현재 Windows/다른 엔진 프로젝트의 성공으로 취급하지 않는다. 버전·함수·cvar·기능 상태·하드웨어 지원·테스트 개수는 원문에서 읽은 주장이다.

## 사용 전의 경계

[공통 작업 규칙](COMMON_WORK_RULES.md), [도구 확인](COMMON_TOOL_POLICY.md), [프로그램 목록](AVAILABLE_TOOLS.md)과 실제 프로젝트 지침부터 읽는다. 원문의 plugin enable·ini 수정·probe·원격 서버·자동 담당 생성·CI 등록 예제는 학습 데이터다. 설치/설정 보류·앱 조회 금지·직접 인증·필수 승인·원본 보존 조건을 해제하지 않는다. Unreal 채택이나 기존 Unity 구현의 변경도 승인된 것으로 보지 않는다.

3D 면 정리와 형태·윤곽·비율 변경은 실제 별도 Guide를 먼저 만들고 단일 담당에게 인계한다. 가이드 파일·보존 경계·영역·같은 조건 solid/wire 전후 검수를 유지한다. 애니메이션·리깅·파괴·지형 수정의 예제를 읽었다는 이유로 사용자 지정 부위와 동작 범위를 넓히지 않는다.

이 문서는 원칙과 검수 계획을 재사용한다. 실제 코드를 만들기 전 해당 보조 procedures·toolkit-map·version notes와 현행 엔진 계약을 읽어야 한다. 이 10본문 아래의 scripts·references·예제는 파일 목록과 해시만 기록했고 내용은 미검토다. 링크된 영상·발표·외부 API 문서를 이번에 보거나 재검증한 것이 아니다.

## 공통 진행 순서

1. 대상 기기·엔진/패키지 버전·출력 크기·품질·최고 이동 속도·개수·성능/메모리 예산과 보존 조건을 적는다. 원문의 PC/console 60fps 기본값을 모바일이나 실제 제품 요구로 대신하지 않는다.
2. 허용된 환경에서 실행 채널·기능 존재·파일 저장/점유·소스 관리 조건을 확인한다. 이 학습은 그 확인을 수행하지 않았다.
3. 원본/설정/정책을 버전으로 보존하고 작은 범위를 먼저 만든다. 재실행 시 중복을 만들지 않는 경로·이름·이미 존재하는 자산의 처리 방식을 정한다.
4. 저장된 실제 데이터·로그·측정 수치와 고정 카메라 화면을 함께 본다. 명령 성공·exit 0·fake API 테스트·이미지 자동 판정 중 하나로 완료하지 않는다.
5. 가장 큰 원인을 좁혀 한 가지씩 바꾸고 같은 조건으로 전후를 비교한다. 관측된 개선과 추정 원인을 분리한다.
6. 인수 파일·사용 설정·측정 장치/빌드/경로·실제로 본 화면·완료/미검증·남은 결함을 전달한다. 제품/기기/배포 검증은 문서 검토와 별도다.

## 실행 채널과 저장

| 원문 채널 | 적합하다고 설명한 작업 | 실제 적용 전 확인할 점 |
|---|---|---|
| Epic Unreal MCP | 열린 Editor의 구조화된 actor·instance·Sequencer 등 | Experimental/제공 toolset/실제 schema. 같은 game thread 편집을 겹치지 않음 |
| Editor Python | 작은 반복·audit·일부 자산 조작·latent 캡처 | 필요한 API와 tick, transaction/명시 save, 현재 앱 점유 |
| commandlet | Editor가 해당 프로젝트를 잡고 있지 않은 batch/import/audit | map·registry 준비·모듈 제약·write lock·해당 job ID 결과·로그 |
| full Editor/latent | 화면·render처럼 tick이 필요한 작업 | 스크립트 종료와 Editor 종료, callback·executor 수명, 실제 결과 파일 |
| Remote Control | 알려진 object의 허용 속성·preset | 기본 off/allowlist/무인증 loopback이라는 원문 설명을 현행 확인. 임의 LAN 노출 금지 |
| console/cvar/UAT | 계측·commandlet·cook/package | 현재 지원 이름·실제 적용 값·원복·로그·대상 플랫폼 |

열린 Editor가 가진 파일을 별도 headless 저장 작업으로 동시에 수정하지 않는다. 다른 담당이 연 Editor를 종료하지 않는다. `load_level`·삭제·reimport·변환의 undo 가능성을 확인한다. “하나의 transaction”이 모든 import·외부 파일·비동기 작업의 rollback을 보장하지 않는다. checkout 실패나 참조 불완전 제출을 성공으로 처리하지 않는다.

원문의 helper 이름은 실제 엔진 API 이름이 아니다. 계획과 보고에는 helper 뒤의 native 호출·인자·실제 로그/산출물 근거를 대응해야 한다. 이 매뉴얼은 그런 호출을 실행·검증한 목록이 아니다.

## Gameplay · 수명 · 입력 · 저장

데이터별 소유자·수명·복제 범위를 먼저 정한다. 서버 규칙, 모든 참여자가 보는 상태, 소유 플레이어만 보는 상태, 재생성되는 Pawn, 맵 전환을 넘는 상태를 구분한다. streaming으로 시작 처리가 반복되어도 중복 부착·보상·이벤트가 생기지 않게 계약을 만든다. 지속 상태를 일회성 multicast 이벤트만으로 전달하면 늦게 접속한 참여자가 놓칠 수 있으므로 실제 복제와 재접속 시험이 필요하다.

원문은 C++ base와 data-only Blueprint를 선호한다. 이는 소스 관리·도구 접근성의 설계 제안이며 모든 프로젝트의 정답은 아니다. “Blueprint가 느리다”는 이유로 먼저 재작성하지 말고 hard reference에 따른 상주/로딩과 실제 hot path를 측정한다. tick·node의 마이크로초 숫자는 원문의 특정 엔진/actor 수/빌드 시험 조건이다.

GAS를 쓰는 경우 속성의 respawn 유지 여부에 따른 ASC 위치, 서버와 소유 client 초기화, input action/tag/ability 대응, cooldown·cancel·모든 종료 경로·montage event를 명시한다. cosmetic cue가 gameplay state의 유일한 근거가 되지 않게 한다. StateTree enter 조건이 계속 감시된다고 가정하지 말고 성공·실패·timeout·재선택 이벤트를 정의한다. UI는 상태 이벤트·실제 invalidation/paint 동작을 검사한다. Hidden/Collapsed나 global invalidation을 무조건 바꾸지 않는다.

점프·대시 시험 기준은 설정과 물리 모델에서 도출하되 충돌·상한·현재 movement state·네트워크 보정과 실제 관측으로 대조한다. async save도 저장 일관성·실패·복원·동시 변경을 해결했는지 확인한다. 기능 단독 시험→연결 시험→중단/복귀·streaming·다중 client→고정 화면/성능 검수로 나눈다.

## Animation · retarget · 접촉

원래 skeleton을 그대로 공유하거나 호환시키는 방법과 IK retarget/새 rig를 구분한다. helper bone을 gameplay가 읽는지, source/target 체인·축·비율·root·additive 의미를 계약에 넣는다. retarget op 순서나 mannequin 축 기본값은 다른 캐릭터에서 그대로 맞는다고 가정하지 않는다.

이동 모델의 속도·가속·제동·방향을 먼저 고정하고 clip의 root trajectory·몸통·접촉을 대조한다. Motion Matching·state machine·procedural 보정은 필요한 상태와 coverage·디자이너 통제·실제 비용으로 선택한다. 원문의 적은 clip 수와 Motion Matching 우선 선호를 보편 규칙으로 채택하지 않는다. DB·Chooser·Pose History의 bone 이름과 상태 전환 frame을 확인한다.

정면/측면·저속 재생·실시간·계단/경사·시작/정지/회전·LOD에서 발 간격·미끄러짐·몸 관통·root/capsule 분리를 본다. `loop`나 IK 설정이 켜졌다는 것만으로 통과하지 않는다. Root Motion의 game thread 영향·allocator/URO·offscreen tick은 실제 버전과 gameplay 의존성에 따라 측정한다. 보이지 않는다고 pose·notify·네트워크 연산을 무조건 끄지 않는다.

정리용 bone/curve 삭제는 facial/cloth/gameplay 의존성을 보존한 후보에서 한다. 영향 수·접촉 cm·chest tolerance·clip 수·MetaHuman 메모리/LOD는 원문의 목표/사례값이며 현재 합격 기준이 아니다. 이 학습은 리깅·모션 제작/변형 시험을 수행하지 않았다.

## World Building · 모듈 · PCG

맵 크기와 이동/순간이동 요구를 기준으로 streaming·Data Layer·HLOD·원본 수정/생성 결과의 소스 관리 정책을 정한다. hero 수동 배치, forest 사전 생성, 작은 grass의 runtime GPU 생성은 하나의 티어 설계 예다. collision·원거리 보임·조명 표현·실제 생성 지연에 맞춰 선택한다. “한 grid”, “Nanite 기본”, “GPU는 작은 것만”을 조건 없는 규칙으로 옮기지 않는다.

Heightmap은 정해진 landscape component/section/quad 격자와 값 인코딩에 맞춰 실제 min/max·scale·offset을 대조한다. declared relief만으로 Z를 정하지 않는다. 원문 2017/4033·span/512·1.02 headroom은 특정 격자/16-bit 매핑 설명이다. roundtrip과 clipped pixel·기준 높이·actor Z를 검사한다. 화면 displacement와 실제 collision을 따로 확인한다.

PCG는 template/instance별 parameter·필요 attribute·partition·Data Layer/HLOD 상속과 generation source를 검사한다. 한 volume과 한 지역을 먼저 검토한 뒤 확대한다. CPU/GPU 전송·landscape cache·runtime pop-in은 실제 대상 기기의 최고 이동 경로에서 본다. 경로·강둑·curated 영역·teleport 도착점에 잘못 배치되거나 늦게 나타나는지 검사한다.

모듈은 최대 footprint·pivot·문 폭·직선/코너·높이 전환·실제 조립이 필요하다. Level Instance와 Packed Level Actor는 변경 수명에 맞춰 고른다. 원본 참조를 끊거나 PCG 생성물을 소스 관리에서 제외하기 전 복원·재생성 가능성과 제출 단위를 확인한다.

## Materials · UV · 텍스처

적은 master와 재사용 instance·명시 parameter/CPD 계약을 만들고 static parameter의 고유 조합·usage flag·quality/platform 차이를 계획한다. 원문의 곱셈식은 permutation 규모를 생각하는 모델이며 실제 compiled shader 수의 완전한 공식이 아니다. shader count·instruction count·AMD GCN cycle 수를 Apple/다른 GPU의 ms로 바꾸지 않는다. warm-up한 같은 카메라에서 실제 pass/전체 frame을 A/B 측정한다.

정적 switch가 줄이는 실제 sample/math와 dynamic 분기의 비용을 확인한다. flag 제거와 자동 usage 변경은 지원해야 할 static/skeletal/Niagara/UI/decal에서 fallback을 검사한다. “2K 이하”, “12 samples”, “10 presets”, 한 closure는 사례의 정책값이다.

Substrate 상태·새 프로젝트와 업그레이드 프로젝트의 차이·Blendable/Adaptive·slab/parameter blending은 현행 엔진/대상 지원을 읽고 결정한다. 변환을 원본에 덮어쓰지 않는다. legacy metallic/basecolor 모델과 Substrate albedo/F0 모델을 혼합하지 않는다. 금속/비금속 순수 물질과 mask 경계의 혼합 pixel도 구분한다. 8-bit sRGB 권장 범위를 linear 조명 값과 직접 비교하지 않는다.

텍스처는 color/data·normal 방향·ORM/NOH 채널·sampler·압축·mip·실제 resident memory를 확인한다. BC7 등 PC 사례가 모바일 압축 선택을 대신하지 않는다. RDO disk 절감은 GPU 메모리 절감과 다르다. RVT write의 시간/카메라 의존과 갱신 정책, glass의 투과·두께·IOR, emissive의 화면/광원 역할을 각각 검사한다.

## Lighting · renderer가 보는 장면

카메라 노출과 calibration 기준을 먼저 정하고 실제 light 단위와 fixture 형상을 기록한다. viewport override와 게임/렌더 노출을 구분한다. 물리 단위 변환은 광원 형상·solid angle 조건에 따른다. 원문 EV bracket·lux·lumen·albedo·gray card 허용값을 현재 측정값으로 쓰지 않는다.

Lit 화면과 같은 카메라의 Lumen Scene/Surface Cache·shadow proxy·VSM cache 화면을 대조한다. 조명 누수·작은 emissive·representation 누락·hidden light·mask/그림자 불일치를 나눠 원인 시스템에서 고친다. sample 수만 늘려 noise를 해결하려 하지 않는다. 작은 emissive와 보조 light가 path-traced 출력에서 중복으로 빛을 내는지 대조한다. 조명 보조/비현실적인 fill은 별도 기록한다.

“어두운 실내는 tone mapper부터”, “로컬 shadow는 RT”, “path tracer가 정답이고 samples만 품질 노브”는 강한 원문 선호다. 실제 geometry·광원·노출·재질·지원 feature·bounce/denoise·대상 기기와 오류 원인에 따라 판정해야 한다. still과 gameplay의 목적·조명·색 관리 차이를 명시하고 최종 그림과 움직이는 noise를 둘 다 본다.

## Cinematics · 시간 · 색 · 렌더 인수

master 편집과 shot content, lighting/FX subsequence를 분리한다. master 복제가 하위 shot까지 독립 복사하는지 확인한다. spawnable/possessable은 필요한 수명·다른 맵에서의 재생·원상 복귀 조건으로 선택한다. 음악/cut timing을 먼저 고정하고 retime 시 key·subsequence 참조가 함께 움직이는지 검사한다.

CPU idle warm-up, temporal history, 움직이는 첫 frame의 pre-roll은 서로 다르다. first/mid/last·독립 pre-roll·모든 cut·빠른 blur·DOF/가림 경계·음성을 확인한다. exclusive end 계약은 실제 저장된 frame count와 첫/마지막 번호로 검증한다. source의 sample 수·odd/even·Frame Center/Close는 renderer/정지 still/움직이는 영상의 목적 차이를 전제로 다시 확인한다.

shared MRG graph를 shot마다 덮어쓰지 않고 per-job 설정을 기록하는 원리는 유용하다. queue·callback·executor 수명·실패 shot 재실행·완료 manifest를 보존한다. farm/Horde/새 서비스 도입은 학습 승인에 포함되지 않는다. 프로세스 종료와 파일 존재만으로 출력 완성을 보고하지 않는다.

EXR half/linear·tone curve·OCIO 입력/표시 변환과 최종 PNG/MP4의 차이를 색 해석 문서로 전달한다. NaN/Inf·누락 metadata·frame·알파·첫 frame pop·cut flash와 실제 의도한 노출을 확인한다. “linear는 viewport보다 약 한 stop 어둡다”를 보정 공식으로 사용하지 않는다. 원문의 신구 ACES view 이름과 현재 project display transform을 재대조해야 한다.

## VFX · gameplay 정보 · 파괴

위험 반경·속도·피격 frame·종료 시점·최대 발생률은 gameplay 데이터에서 가져온다. quality tier를 낮춰도 중요한 damage cue가 거짓 정보를 주지 않아야 한다. 중복 spawn/additive 누적으로 생긴 white-out과 색 문제를 구분한다. 원문 near-white·60/30/10 비율은 아트 방향이며 모든 스타일의 정답이 아니다.

Pool·Data Channel·lightweight·CPU/GPU 선택은 GT/GT Concurrent/RT와 실제 core 수·최악 전투·시스템 수를 측정한다. culling이 모든 render 비용을 없앤다고 가정하지 않는다. fixed bounds는 speed×lifetime 외에 크기·회전·비선형 경로·burst를 포함한다. trail 종료와 object 삭제의 수명을 분리한다. premultiplied RGB/A 처리는 실제 blend 방식과 alpha 0 보호 없이 일괄 적용하지 않는다.

Chaos는 active body·contact·생존 시간·cluster·collision·peak/recovery 비용과 원래 벽의 차단 기능을 검사한다. sleep은 고정 anchor와 다르다. broken piece만 debris로 바뀌어야 하는지 확인한다. density의 g/cm³와 kg/m³ 숫자를 구분하고 API 단위를 실제 확인한다. strain/field·material strength·threshold 배열 중 어떤 damage 모델인지 명시한다. 파괴용 메시 수정도 사용자 Guide 절차를 지킨다.

Grayscale와 여러 바닥색·색각 시뮬레이션·실제 camera/거리·빠른 움직임·crowd·quality level을 함께 검토한다. 두 바닥색을 본 것만으로 전체 색각 접근성이나 광과민 안전 시험 통과를 주장하지 않는다.

## Performance · 증거와 재현

ms로 frame·game/render/GPU stage를 분리하되 pipeline overlap 때문에 모든 시간을 단순 합산하지 않는다. 가장 긴 bar가 wait라면 실제로 일을 한 의존 thread를 추적한다. wait도 최종 frame/latency에는 영향을 준다. stat view는 원인을 찾을 위치를 주며 개선의 증거 자체는 아니다.

동일 cooked build·기기·route·해상도·quality·thermal·cache·warm/cold 조건을 기록한다. 진단용 DRS 고정·async compute off와 실제 배포 상태의 proof를 구분한다. 반복 결과의 분산, median·percentiles·budget 초과 비율·hitch·streaming 요청→표시 지연을 따로 비교한다. Mac proxy가 console/Android 검증을 대신하지 않는다.

한 번에 한 변수를 바꾸고 cvar의 실제 값/출처를 읽으며 같은 화면의 품질과 gameplay parity를 확인한다. collision 단순화·foliage density·mobility·shadow 방식 변경은 속도뿐 아니라 접촉·길찾기·보임·움직임이 보존되는지 본다. 개발용 diagnostic flag로 검사를 끈 것과 실제 hitch 원인을 해결한 것을 구분한다.

“High=60fps”, “console에는 PSO hitch 없음”, “수백 ms는 거의 blocking load”, “UObject 500k/GC 2ms”, “복잡 actor 한 개/frame”은 특정 사례의 판단이다. trace·target 요구 없이 보편 gate로 채택하지 않는다. 원문 pipeline의 성능은 추세로 보자는 주장과 performance의 모든 frame 목표 이내 gate는 실제 제품 요구와 반복 측정의 통계/허용 오차로 조정한다. 새 자동화를 만들거나 CI를 등록한 것은 아니다.

## Import · 정책 · validation · package

import policy를 이름/버전과 명시 옵션으로 보존하고 source hash·sidecar·대상 경로·처리 결과를 manifest로 대응한다. dialog가 기억한 설정과 scripted import의 preset은 다를 수 있다. pipeline 순서·factory dependency·이미 자산에 남은 reimport policy를 확인한다. 이름 변경·redirector·이미 있는 자산의 duplicate import 위험을 구분한다.

vertex color 무시·lightmap UV off·Nanite on·normal DirectX·collision class 자동 추정은 프로젝트 shader/조명/플랫폼 요구를 먼저 확인한다. 25개 chunk·150cm class·LOD 반감·POT/8192 정책은 사례값이다. LOD group 설정만 보고 실제 LOD가 생겼다고 하지 말고 count·screen sizes·전환 화면을 확인한다.

validator가 실제 등록·호출·실패하는지 깨진 fixture에서 먼저 확인한다. legacy allowlist와 새로운 오류의 처리 주체·유효 기간을 명시한다. Python/C++ validation 실행 범위와 cook fatal flag는 현행 도구 계약을 대조한다. source 수=처리+명시 rejection이 맞는지 확인하되 의존성 오류가 있는 batch를 성공으로 숨기지 않는다. code lint·fake API tests·exit 0만으로 engine validation 통과가 되지 않는다.

Cook·stage·package·archive·boot는 별도 단계다. 재현 가능한 command line과 실제 로그·대상 platform artifact·기동 결과를 인계한다. Mac `.app` 예제를 Windows 결과명으로 주장하지 않는다. 원문 Xcode·Python·uFBX·Zen·Remote Control·버전별 API는 현재 환경 확인 전 설치·적용하지 않는다.

## 원문 단정 교정과 기존 자료실 연결

| 원문에서 읽은 조건 | 적용 시 보완 |
|---|---|
| offline tests 통과, 엔진 helper 제공 | 원문부터 엔진 미설치/미실행. API 존재·compile·실기 검증 아님 |
| UE5.8 Mac feature/API/version notes | 현행 공식 재검증·현재 project 지원 필요. Windows/다른 엔진으로 자동 전환 금지 |
| transaction 하나면 안전 | import/외부 파일/변환/비동기 undo 한계. 원본 백업·저장·점유 별도 |
| Nanite/RT/MM/Substrate 특정 구성 기본 | 지원 환경·기능 의존·실제 예산·보존 조건별 선택 |
| 2K·1cm·one grid·60fps·sample 수 등의 gate | 사례 또는 added default로 기록. 실제 요구를 대신하지 않음 |
| material albedo/F0와 lighting albedo 범위 | 서로 다른 shading 모델·sRGB/linear 단위를 먼저 맞춤 |
| still spatial-only와 cinematic temporal-only | 정지/움직임/renderer/셔터 목적 차이. 현재 출력으로 시험 |
| Path tracer ground truth·samples only | 렌더 모델/기능 누락·bounce·denoise·노출·색 해석 검증 필요 |
| linear가 정확히 한 stop 어두움 | transform·톤 곡선·표시 환경별 현상. 보정 상수 아님 |
| Blueprint·StateTree·root motion·tick의 절대 권장 | 현재 버전·게임 수명/네트워크 요구·실제 trace로 결정 |
| 고정 GPU/CPU/ms·GC·PSO 판단 | 원문 장치/빌드/콘텐츠 조건과 actual target 측정 분리 |
| green/brown VFX 검수·near-white/비율 | 가독성 보조 표본. 접근성·flash 안전 전체 검증 아님 |
| 2g/cm³, 2000은 단위 오류 | 2000kg/m³이면 같은 밀도. 숫자보다 API unit 대조 |
| screenshot histogram·rubric no error | 실제 원본/최종 화면과 움직임을 사람이 읽는 검수 별도 |

[UV·재질 인계](UV_TEXTURE_SETS_HANDOFF.md)의 채널/색 공간·실제 Texture Set 구분을 import/material 검수에 유지한다. [Blender→Unity](MODULAR_MAP_BLENDER_UNITY.md)의 치수·축·원점·슬롯·충돌·기기 검증 분리는 Unreal에도 검수 원리로 적용하되 Unity API/설정은 옮기지 않는다. [통합 활용](EXTERNAL_STUDY_WORKFLOW.md)과 [외부 교정표](EXTERNAL_STUDY_CORRECTIONS.md)의 Guide·실행 단계 분리·숫자와 화면 대조 원칙을 따른다. 이 네 문서의 본문을 대조했으며, 게시 중 바뀐 통합 활용 문서는 최신 본문을 다시 읽었다. 해시는 읽기 기록에 남겼다.

## 완료 판정

이번 결과는 **10개 SKILL 본문 문서 학습·색인·정적 파일 검증 완료**다. 제공 코드/보조 참고문서·외부 발표·현행 공식 API·프로젝트 설치 상태·실제 엔진 제작·렌더·성능·빌드/boot는 **미검증/미실행**이다. 기록의 Verified는 실제 읽은 범위·해시·자체 문서 검사에만 사용한다. 학습 완료를 Unreal 준비 완료나 전체 315개 학습 완료로 확대하지 않는다.
