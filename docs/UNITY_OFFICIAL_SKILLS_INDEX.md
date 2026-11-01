# Unity 공식 35개 SKILL · 주제 탐색과 검수표

2026-11-01. [통합 학습 매뉴얼](UNITY_OFFICIAL_SKILLS_WORKFLOW.md). 원본은 Unity-Technologies/skills의 `089bedebab64e9e75943b19a364c7aec2162a7e7` 고정 스냅샷이며, 아래 35개 **본문을 각각 첫 행부터 끝 행까지 읽었다**. 번호는 이 문서의 가나다가 아닌 원본 폴더명 순서다. 실제 설치·실행·API 검증·서비스 이용이 완료됐다는 목록이 아니다.

원본 탐색: [고정 skills 디렉터리](https://github.com/Unity-Technologies/skills/tree/089bedebab64e9e75943b19a364c7aec2162a7e7/skills). 표의 이름과 `/SKILL.md`를 이어 해당 본문을 찾는다. 정확한 파일 SHA256·바이트·읽은 행 범위는 함께 전달하는 검토 JSON에 있다. 아래 숫자/조건은 **고정 원문의 주장·전제**이며 현재 환경의 설치 상태가 아니다.

| # | 원본 폴더명 · 본문 행 | 다루는 일 | 적용 전에 구분할 것 | 재사용 절차·검수와 실패 주의 |
|---|---|---|---|---|
| 1 | `2d-pixel-perfect` · 1–208 | 픽셀 아트의 흐림·떨림·틈 | URP 내장형 / Built-in standalone / HDRP 미지원, 고해상도 아트 제외 | 파이프라인→sprite PPU/pivot/filter→카메라→정수 배율→카메라 이동·UI 검수. AA/압축/PPU를 모든 아트에 일괄 적용하지 않음 |
| 2 | `asset-transformer-toolkit` · 1–39 | 3D/점군 import·RuleSet·LOD | Toolkit4.0+와 entitlement, Studio와 구별 | 해석 버전→Importer/RuleSet/LOD 경로 선택→설정과 실제 재import 분리. 긴 재import·유료 권한을 자동 진행하지 않음 |
| 3 | `audio-setup-mixers` · 1–127 | 기존 그룹으로 AudioSource 라우팅 | 실제 그룹과 source 분류, 공개 API 범위 | clip/객체 이름으로 분류→그룹 존재 확인→할당→누락 mapping·그룹/scene 저장 확인. `.mixer` 손편집·비공개 tree 조작 우회 금지 |
| 4 | `build-gtk` · 1–242 | Graph Toolkit Editor 도구 | Graph API6.6+, State Machine6.7+, Editor 전용 | graph/node/port→validation→선택적 importer/runtime 분리→asset 재열기. graph 작성은 runtime 실행기를 자동 제공하지 않음 |
| 5 | `build-live-game` · 1–255 | UGS 계정·설정·저장·서버 로직 | cloud project/environment·resolved SDK·Editor와 모듈 형식 | Core/Auth→정의와 상태→신뢰 변경 서버 처리→권한/배포/실제 feature 검수. `.ccmu`6.5+와 legacy`.ccmr`·experimental을 분기 |
| 6 | `craft-game-floors` · 1–134 | 아트·조명·카메라·피드백·오디오·shell | 품질 평가 요청 / 실제 변경 요청, 기존 승인 디자인 | 일관된 스타일 기준→요청된 품질 항목→실제 캡처와 동작 검수. 기존 컨트롤러·캐릭터·팔레트를 예제로 교체하지 않음 |
| 7 | `create-2d-physics` · 1–128 | 2D 물리 제작/진단 | 기존 Rigidbody2D / Core script / Core component6.7+ | 실제 컴포넌트·namespace→버전별 API→상태 읽기/동작 증거→임시 로그 제거. 서로 다른 시뮬레이션을 혼합하지 않음 |
| 8 | `create-tile-palette-or-rule-tiles` · 1–12 | Palette·빈 RuleTile·기존sprite RuleTile | 사용자가 준 그림 유무·격자 유형 | 알맞은 reference로 분기하는 진입점. 부속 제작 절차 미검토이며 3D 키트 자동화의 증거가 아님 |
| 9 | `generate-editor-search-query` · 1–117 | Editor 자산·장면 검색 질의 | asset/scene·known name·query-only | type/path/label/ref 질의→필요시 Search 창→결과와 한계. repository 텍스트 검색이나 결과 자동 수정과 분리 |
| 10 | `implement-in-app-purchases` · 1–157 | IAP5·구매 복원·구독·D2C | 기존 3rd-party/native/v4/v5·codeless·플랫폼, D2C5.4+ | 사전 분류→이벤트 선구독→Connect/Fetch→Pending 검증·중복 없는 지급→Confirm. deferred/재전달·캐시·영수증 플랫폼 차이 검수 |
| 11 | `initialize-ai-navigation` · 1–95 | Surface·Agent·Obstacle·Link·Modifier | 기존 이동·agent type/size·수집 layer·동적 문 | 현재 구성→Surface bake→agent→obstacle/link→실제 path/통과 검수. 파란 영역만으로 실제 보행 PASS 아님, 패키지 추가 절차 상충 주의 |
| 12 | `levelplay-unity-integration` · 1–442 | 광고 mediation 통합·업그레이드·오류 | resolved package·native dependencies·target·SDK9.4/9.5 | 초기화 선행→선택 ad형식→이벤트/수명→mock/실기/Test Suite 분리. 동의·ATT·정책·빈도/가격은 원문 예로 확정하지 않음 |
| 13 | `localization` · 1–347 | 로케일·String/Asset Table·CJK | resolved package·글꼴 권리·locale별glyph·Addressables | locale code 매핑→텍스트·코드 양쪽 추출→persistent event→빈 번역 검사→실제 locale/저장 검수. Canvas 파괴·TMP import·fallback/layout 상충 주의 |
| 14 | `manage-sprite-atlas` · 1–351 | Atlas V2·master/variant·전달 | authoring/importer/runtime·Built-in/Addressables | 기존 생성물→packing 모드→의도 packables→save/import→전달/콘텐츠 빌드→실제 load. prebuild/3스크립트는 원문 설계 선호, API 예외 확인 |
| 15 | `migrate-birp-to-urp` · 1–543 | Built-in→URP와 부분 이관 수선 | full/2D/selected/troubleshoot·복구지점·현재pipeline | 0인벤토리→1재질/Graphics/Quality→2PPv2→3GI/probe→4저장·대표 장면 검수. empty profile/가짜저장/잘못된2D shader·효과 누락은 PARTIAL |
| 16 | `new-unity-project` · 1–339 | 기획부터 신규 프로젝트·인계 | 기존 프로젝트 유무·플랫폼·template·계정·비용 | brief→조건 목록→환경/버전관리→패키지→시각기준→meta/저장→인계. latest/cloud/익명 계정 기본을 기존 사용자 승인으로 해석하지 않음 |
| 17 | `optimize-audio` · 1–199 | 오디오 메모리·CPU·로드·품질 | platform/rate·listener·source·load/codec | baseline→원인별 import/공간/스트리밍 후보→재import/실기 측정. 그룹tree/효과 조회는 mixer 문서와 상충, mono/sample값 일괄 강요 금지 |
| 18 | `optimize-text-mesh-pro` · 1–172 | TMP atlas·SDF·fallback·AutoSize | 메모리/품질/CPU/빌드/언어 증상 | glyph/atlas 체계→padding·scale→변경 빈도·Canvas→기기 비교. DynamicOS·폰트명·sampling숫자는 가용/권리/기기별 확인 |
| 19 | `optimize-web` · 1–530 | Web 다운로드·로드·메모리·프레임 | host header·browser baseline·package·dev/release | baseline→압축/strip/예외/메모리→저장→실제browser Network/성능 검수. per-machine설정·품질index/기기수치·과한stripping 주의 |
| 20 | `physics-3d-collision` · 1–442 | 3D 충돌·trigger·raycast | 2D/DOTS/PhysX·callback·body유형 | pair/mask/movement/callback/시간 상태를 나눠 진단. 원문의 단일원인·무검증·보장 fast path는 독립 사실로 채택하지 않음 |
| 21 | `project-auditor-fixes` · 1–64 | 정적 audit→CSV→묶음별 수선 | Auditor/rules·실제 명령·검수 baseline | trigger→terminal status→파일/종류별 작은 수정→시험. unavailable/interrupted를 깨끗한 scan으로 보고하지 않음 |
| 22 | `setup-multiplayer-services` · 1–36 | 세션·발견·호스팅·netcode 경로 | 실시간 네트워크 요구·topology·복구·platform | Sessions API 우선 탐색→요구 적합성→필요시 하위서비스. 전체 reference/API나 실제 연결은 미검증 |
| 23 | `setup-vivox-voice-chat` · 1–118 | 음성/문자·채널·이벤트 | Vivox16.4+·identity·mic·token·platform | Core/Auth/init/login→join 요청과 완료event→participant→unsubscribe/leave. v4 API와 혼합 금지, 실제 한도/정책은 재확인 |
| 24 | `shader-graph-create-custom-node` · 1–25 | HLSL reflected custom node | ShaderGraph17.5+·기존 include | export reflection→hint tags→기존파일 보존→컴파일/Graph 확인. 17.3에 기능을 있다고 가정하지 않으며 부속 hints는 미검토 |
| 25 | `sprite-editor` · 1–66 | sprite rect·pivot·border·outline·slice | live Editor와eval·importer capability | provider init→권한별지원확인→rect수정→Apply/Reimport→실제 readback. meta 손편집/지원검사 우회 금지 |
| 26 | `sprite-segment-3x3grid` · 1–136 | sprite색의3×3패턴 표현 | 실제sprite rect·alpha·색오차·동률/나머지pixel | 중앙최빈색→주변비율→임계값→위에서아래로출력. 75%는원문기본, 구조/기하판정이 아님 |
| 27 | `ui` · 1–142 | UI 체계 선택·라우팅 | explicit file/기존runtime·Editor UI | 기존파일/계층→UITK/uGUI/IMGUI분기→질문/수정/생성 범위. Figma자동import를이환경에서지원한다고약속하지않음 |
| 28 | `ui-imgui` · 1–180 | 기존 EditorWindow/Inspector/Drawer | 기존 IMGUI·Editor assembly·명시요청 | SerializedProperty·Undo·style cache·Begin/End·Apply→Editor/빌드검수. 런타임게임화면을자동OnGUI로만들지않음 |
| 29 | `ui-ugui` · 1–276 | Canvas·RectTransform·Layout·Prefab | 기존계층·레이아웃소유권·logic요청여부 | 현상/부모확인→국소수정→크기/anchor/pivot→이벤트/실제화면. 계층전체재생성·무관script추가를피함 |
| 30 | `ui-uitk` · 1–229 | UXML/USS·binding·Manipulator | runtime/Editor·PanelSettings·현재지원property | 기존styles재사용→완전한파일→import/Console→실제layout·event. CSS동일가정금지, 원문작성정책과API존재를구분 |
| 31 | `unity-cli` · 1–711 | Editor/프로젝트·VCS·build/test·plugin | CLI·인증·Pipeline·정확한target를각각확인 | schema검색→정확target→명령→JSONsuccess/error/partial→실제결과. 자동update/install/EULA·업로드·다른Editor사용금지 |
| 32 | `unity-package-management` · 1–352 | UPM add/remove/search/resolve | 현재해석버전·live 명령·프로젝트점유 | package명령우선→필요시C#async대체→resolve/lock/compile. batch fallback에열린Editorlock/조기quit주의, 이번설치0 |
| 33 | `unity-pipeline` · 1–335 | live Editor/개발Player·테스트·capture | server별명령·packageversion·Mono/IL2CPP | target고정→autotick시작상태→비동기compile/test→실제Play진행→restore. main Play와MPPM clone/scenario, methodreload와파일수정분리 |
| 34 | `urp-postprocessing` · 1–188 | Volume 효과·디버깅 | 활성URP14+·카메라·layer·profile·override | preflight→원하는effect→값/override→저장→Game view. sharedProfile/instance·HDR/Bloom설명차이·효과별규약확인 |
| 35 | `validate-urp-render-graph-renderer-feature` · 1–269 | Render Graph 코드 리뷰 | Unity/URP version·feature/pass·shader계약 | confirmed/likely분리→input/output·PassData·descriptor·global·ConfigureInput→최소수정안. 예제descriptor타입포함컴파일/렌더미검증 |

## 부속 문서에서 추가로 확인한 내용

| 파일(위 원본 skills 폴더 기준) | 읽은 행 | 추가로 확인한 점 |
|---|---|---|
| `unity-package-management/references/select-packages.md` | 1–126 전체 | 장르별 package 후보·registry known-id와검색차이. pixel-perfect전용본문과조건충돌가능 |
| `craft-game-floors/references/art-direction.md` | 1–85 전체 | 스타일/팔레트/조명 기준·기존개발자선택보존. 캐릭터예제/과장은기준디자인아님 |
| `craft-game-floors/references/visual-scorecard.md` | 1–43 전체 | 상태/실행진행·warmup·UI포함capture·범위별점수·시작상태복원 |
| `ui-ugui/references/scrollview-setup.md` | 1–29 전체 | ScrollRect/Viewport/Content·참조·동적중복·크기책임 |
| `sprite-editor/references/templates.md` | 1–72 전체 | data provider와capability실패시중단·Apply/Reimport |
| `implement-in-app-purchases/references/pre-check.md` | 1–205 전체 | 기존결제경로·D2C분기·codeless자동초기화경합 |
| `ui-uitk/references/common-issues.md` | 1–74 전체 | hover-out·selector/style·괄호·계층성능·theme참조의작성지침 |
| `manage-sprite-atlas/references/common-errors.md` | 1–123 전체 | runtime atlas를쓰는Editor예외·GetPackables/SetMaster·packing·API목록 |
| `initialize-ai-navigation/references/navigation-system.md` | 1–110만 | 컴포넌트·크기·수집·bake·agent·obstacle기본.111–794와이후레시피미검토 |

원본 README와 LICENSE.md도 읽었다. 나머지 references/resources/scripts/api-docs의 본문은 **미검토**다. 파일명 목록·크기를 조사한 것을 본문 열람으로 세지 않았다. 실제 원본/읽기 범위 해시와 미검토 부속 파일 목록은 [학습 기록 JSON](../reports/ExternalLearning/20261101_UNITY_OFFICIAL_SKILLS_STUDY.json)에 분리한다.

학습에서 나온 적용 제안과 원문 사실·버전 전제·API 의심을 구분한다. 매뉴얼을 만들었다는 이유로 원본 SKILL을 자동 설치·활성화하거나 프로젝트의 앱 조회 금지·설정 보류를 해제하지 않는다. Unity6.3 현행 웹/API 재대조와 모든 실기 검증은 아직 미완료다.
