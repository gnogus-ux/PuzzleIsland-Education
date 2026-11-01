# Unreal 10주제 탐색표

2026-11-01. [제작·인계·검수 매뉴얼](SCENARIO_UNREAL_SKILLS_WORKFLOW.md) · [읽기 범위·해시](../reports/ExternalLearning/20261101_SCENARIO_UNREAL_SKILLS_STUDY.json)

원본 Scenario Labs skills, MIT, 고정 커밋 `7f4b801c7248d51b093ec365aceb114bd06139e6`. `skills/game-engines/unreal/**/SKILL.md` 10개 **2,172행·212,243바이트 전부 읽음**. 아래 링크는 모두 고정 본문이다. 보조 scripts·references·외부 링크의 내용을 읽거나 실행한 것은 아니다.

원문은 **UE 5.8/macOS Apple Silicon**을 대상으로 작성했으며 **Unreal 미설치, 엔진 호출 미실행, 오프라인/fake API 검사만 수행**했다고 명시한다. 아래 작업/도구/수치는 원문의 설명이다. 현재 환경·현행 버전의 검증 결과가 아니다. 실제 작업에는 공통 규칙·원본 Guide·단일 점유·설정 보류·앱 조회 금지가 먼저 적용된다.

| 전체 읽은 본문·행수 | 주제·찾을 상황 | 선행 입력 | 원문의 작업 흐름 | 검수·실패/인계 |
|---|---|---|---|---|
| [scenario-unreal-expert] · 210 | 실행 채널, Editor Python/MCP/commandlet, 공통 TD 절차 | target engine/device·예산·권한·저장/점유 | 채널 선택→작은 stage→수치+같은 camera→원인 수정 | native API와 helper 대응·job ID/log·실제 screenshot·Verified/Assumed. offline 통과를 엔진 성공으로 쓰지 않음 |
| [scenario-unreal-animation] · 225 | FBX skeleton, retarget, locomotion, contact, AnimBP 비용 | rig/clip/축·root·movement model·target budget | 가장 단순한 transfer→필요 IK→retarget→접촉→locomotion→LOD/계측 | 발/손 helper bone·root/capsule·전환 frame·계단/경사·실시간·trace. 원본 rig 보존과 리깅 보류 |
| [scenario-unreal-gameplay] · 214 | 데이터 수명, Blueprint/C++, GAS, input, AI, UI, save | single/network·생존/복제 계약·동작 수치·기존 구조 | owner 결정→구현 경로→단독 기능→연결/다중 client→계측 | late join/respawn/streaming·cancel/cooldown·AI 출구·UI/입력·save복원. C++ 원문 미컴파일 |
| [scenario-unreal-world-building] · 221 | WP, Data Layers/HLOD, heightmap, PCG, kit/streaming | world/grid/heights·최고 속도/teleport·수동/생성 범위 | map spec→terrain→조직/kit→단일 PCG volume→지역 builder→이동 경로 | 실제 Z/clip·layer·footprint/pivot·collision·지연/pop-in·curation 경계. 생성물 제출 정책 명시 |
| [scenario-unreal-materials] · 209 | master/instance, Substrate, maps, shader/permutation, RVT | shading 모델·platform·역할별 texture·예산 | family/presets→texture policy→graph/instance→flags→fixed-camera A/B→cook | 색 단위·normal/packed sampler·fallback·resident memory·actual pass ms. fake unreal tests만 |
| [scenario-unreal-lighting-rendering] · 214 | 노출·physical light, Lumen/MegaLights/VSM, still | camera/exposure·fixture·target renderer·Substrate·기준 장면 | calibration→lighting→representation views→noise원인→look→still→manifest | source/보조 light 중복·proxy 누락·leak/flicker·actual EXR/색·같은 camera. PT/샘플 보편단정 교정 |
| [scenario-unreal-cinematics] · 217 | Sequencer cut/shot, camera, preroll, MRG/EXR | timing/music·fps/start·bindings·lighting master·색 계약 | offline plan→shot/subsequence→board lock→polish→draft→shot render→인계 | 첫/끝 번호·exclusive end·preroll·모든 cut/blur/DOF·음성·EXR/metadata·실제 색 해석 |
| [scenario-unreal-performance] · 213 | CPU/GPU bound, hitch, PSO/GC/streaming, proof | 같은 cookedbuild/device/route·quality·DRS/cache/열 조건 | 반복 baseline→bound/의존성→한 변경→parity→hitch→배포상태 proof | ms+percentiles/분산·실제 cvar·wait 원인·cold/warm·품질. synthetic 50 tests가 target proof 아님 |
| [scenario-unreal-vfx] · 225 | Niagara cue/비용, pooling/NDC, Chaos 파괴 | gameplay radius/window/rate·camera·min cores·아트 기준 | timing/critical class→template params→재질→pool/caps→gameplay→captures→계측 | damage cue 일치·duplicate/whiteout·bounds·quality tier·activebody/contact/recovery. 밀도 단위와 alpha0 처리 |
| [scenario-unreal-pipeline-automation] · 224 | batch import/reimport, policy, validators, LOD, cook/package | source hash/sidecar·경로/이름·policy·권한·target | plan/stage→explicit pipeline→fixture trial→accounted import→validate/look→cook/stage/package/boot | registry/write lock·원본·중복·reimport policy·실제 LOD·validator 호출·job/log·targetartifact/boot. 원문 호출 전부 미실행 |

## 전체 읽기와 다음 구현의 차이

10본문은 기능을 분류하고 검사 목적을 정하는 자료다. 실제 구현 전에는 해당 폴더의 `references/procedures.md`, `references/critique.md`, version/API 근거와 필요한 코드·toolkit-map을 읽고 현행 프로젝트 환경에서 좁게 검증해야 한다. 본문이 요구한 probe나 설치·ini 변경을 이 학습에서 수행한 것으로 취급하지 않는다.

원문의 샘플 예산·하드웨어·영상 timestamp는 출처 관찰이다. 해당 영상을 이번에 시청하거나 현행 Epic API와 교차 검증하지 않았다. 자동 테스트 수·기능 이름·source 버전 노트를 “공식 검증 완료”로 바꾸지 않는다. `문서 읽음`, `실제 코드 실행`, `저장 자산 검수`, `기기 성능`, `빌드/기동`은 각각 별도의 완료다.

[scenario-unreal-animation]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unreal/scenario-unreal-animation/SKILL.md
[scenario-unreal-cinematics]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unreal/scenario-unreal-cinematics/SKILL.md
[scenario-unreal-expert]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unreal/scenario-unreal-expert/SKILL.md
[scenario-unreal-gameplay]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unreal/scenario-unreal-gameplay/SKILL.md
[scenario-unreal-lighting-rendering]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unreal/scenario-unreal-lighting-rendering/SKILL.md
[scenario-unreal-materials]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unreal/scenario-unreal-materials/SKILL.md
[scenario-unreal-performance]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unreal/scenario-unreal-performance/SKILL.md
[scenario-unreal-pipeline-automation]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unreal/scenario-unreal-pipeline-automation/SKILL.md
[scenario-unreal-vfx]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unreal/scenario-unreal-vfx/SKILL.md
[scenario-unreal-world-building]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/game-engines/unreal/scenario-unreal-world-building/SKILL.md
