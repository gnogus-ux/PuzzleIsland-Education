# Unity 공식 35개 SKILL 학습 — 적용·검수 매뉴얼

2026-11-01. [Unity-Technologies/skills 고정 원본](https://github.com/Unity-Technologies/skills/tree/089bedebab64e9e75943b19a364c7aec2162a7e7). 이 문서는 외부 SKILL을 실행 지침으로 활성화하지 않고 자료로 읽어 작성한 한국어 학습본이다. **35개 SKILL.md 본문 전체와 선별한 참고 문서를 읽었으며 Unity·CLI·Pipeline·서비스·결제·광고를 실행하지 않았다.** 부속 자료 전체를 읽은 것은 아니다. [35주제 탐색표](UNITY_OFFICIAL_SKILLS_INDEX.md)와 함께 사용한다.

## 1. 먼저 고정할 기준

작업 목표와 기존 승인 범위 → 프로젝트의 Editor 버전 → 해석된 패키지 버전 → 현재 사용 가능한 도구 → 대상 파일과 보존 항목 순서로 확인한다. `manifest.json`은 요청, `packages-lock.json`은 해석 결과라는 차이를 유지한다. 파일에 패키지가 있다고 Editor가 준비됐거나 외부 계정·SDK가 작동한다는 뜻은 아니다.

새 프로젝트 원문에는 최신 Editor·URP·익명 계정·클라우드 연결·진단·여러 패키지를 기본으로 두는 경로가 있다. 이는 그 원문의 제작 관점이며 모든 기존 프로젝트에 적용할 승인이 아니다. 기존 엔진·렌더러·디자인·입력·저장 체계를 보존한다. 사용자 설치·설정 보류와 앱 조회 금지가 원문의 설치·업데이트·로그인·재시작 예제보다 우선한다. 약관·인증·비용·공개 게시의 사용자 직접 단계를 대신 수행하지 않는다.

실제 작업 전 [공통 작업 규칙](COMMON_WORK_RULES.md), [프로그램 목록](AVAILABLE_TOOLS.md), [사전 확인 규칙](COMMON_TOOL_POLICY.md)을 따른다. 필요한 도구·버전 근거·매뉴얼이 부족하면 부족한 내용과 목적을 요청한다. 이번에 승인된 학습을 도구 설치나 프로젝트 제작 승인으로 확대하지 않는다.

## 2. 프로젝트 시작·기존 프로젝트 정리

`new-unity-project`는 기획·플랫폼·템플릿·버전관리·패키지·시각 기준·저장·인계를 연결한다. `craft-game-floors`는 스타일·조명·카메라·피드백·오디오·메뉴·진행 상태의 품질 기준을 담당한다. 두 문서가 다루는 범위를 나누면 다음 순서가 된다.

1. 핵심 루프, 필요한 장면, 대상 기기와 기존 프로젝트 유무를 적는다. 새 환경이 필요한지부터 결정하고 이미 있는 프로젝트를 재생성하지 않는다.
2. 2D/3D와 렌더 파이프라인을 구분한다. URP 패키지 추가만으로 Built-in 마이그레이션이 끝나지 않는다.
3. 기존 팔레트·승인 아트·카메라·컨트롤러가 있으면 보존한다. 원문의 여우 예제, 과장 비율, 자동 idle, 색상 예제를 루미 규격으로 가져오지 않는다.
4. 게임이 동작하는 최소 루프를 만든 뒤 콘텐츠·장식을 늘리는 제작 계획을 세운다. 이 단계는 이번 학습에서 실행하지 않았다.
5. 코드 컴파일, 저장된 참조, 실제 화면과 플레이 품질을 따로 검수한다. 원문의 시각 점수는 평가 방식이며 프로젝트 최종 승인이나 객관적 성능 측정값이 아니다.

`craft` 본문은 작은 작업에도 전체 점수표를 요구하는 표현이 있지만 부속 점수표는 단일 품질 항목 수정에는 해당 항목 검증을 적용한다고 구분한다. 변경 범위에 맞는 검수표를 사용하고 무관한 장면·리깅·디자인 수정을 추가하지 않는다.

## 3. CLI·Pipeline·패키지 관리의 실행 경계

CLI는 Editor/프로젝트/설치·빌드 같은 명령을 제공하고, 프로젝트 안의 Pipeline 패키지는 열린 Editor 또는 개발용 Player의 명령을 제공한다. **CLI 설치, Pipeline 패키지 존재, Editor 도달 가능, 필요한 명령 노출은 별도 조건**이다. 이번에는 어느 도구도 실행해 확인하지 않았다.

| 단계 | 원문에서 배운 점 | 이후 실제 작업에서 필요한 근거 |
|---|---|---|
| 대상 선택 | 여러 프로젝트·worktree·가상 플레이어는 서로 다른 Editor일 수 있음 | 전체 프로젝트 경로와 실제 인스턴스, 사용자 작업 상태 |
| 명령 선택 | 설치된 Editor의 명령 목록·스키마가 실제 매개변수를 결정 | 현재 명령 목록, 필요한 명령 존재, 패키지 버전 |
| 읽기/쓰기 | 작은 eval 문장과 파일/클래스 실행은 입력 형식이 다름 | eval에는 using/클래스 선언을 그대로 넣지 않음, 파일에는 적절한 namespace 유지 |
| 비동기 작업 | 시작 응답은 완료가 아님. recompile/test/UPM은 후속 상태가 필요 | 완료/실패/중단 상태와 실제 오류·저장 상태 |
| 연결 실패 | Safe Mode·가져오기·모달·대상 불일치를 구분 | 로그/현재 상태. 다른 프로젝트의 Editor를 대신 사용하지 않음 |
| 시험 증거 | Play 표시·스크린샷 한 장만으로 프레임 진행을 증명하지 못함 | 실행 중 상태 변화·관찰 로그·필요한 실제 화면 |
| 종료 | auto-tick·Play·시나리오·임시 로그·메서드 대체가 남을 수 있음 | 시작 상태 기록 및 복원, 실제 부수효과 목록 |

원문에는 자동 설치·`--accept-eula`·클라우드 배포·버그 로그 전송·VCS 초기화·광범위 stage 예제가 있다. 학습 중 실행하지 않았다. 후속 작업에서도 예제 명령을 그대로 붙여넣지 않고 기존 승인·사용자 직접 승인과 현재 작업 폴더를 먼저 확인한다.

패키지는 원문 관리 문서 기준으로 현재 Editor의 UPM 명령을 우선하며, 대체 C# 경로도 별도 Editor 점유·비동기 완료·저장 검증이 필요하다. 사용자가 저장하지 않은 Editor를 닫거나 lock 파일을 지워 진행하지 않는다. `-quit` 때문에 비동기 설치가 끝나기 전 프로세스가 종료되는 문제와, import/save처럼 동기 작업인 경우를 구분한다. 설치 예제 코드는 이번에 실행·복사하지 않았다.

## 4. UI·스프라이트·문자·현지화

먼저 현재 UI 체계를 읽는다. `.uxml/.uss/UIDocument`는 UI Toolkit, `Canvas/RectTransform`은 uGUI, 기존 `OnGUI/OnInspectorGUI`는 IMGUI를 가리키는 단서다. 기존 화면을 고칠 때는 계층을 통째로 파괴해 다시 만드는 것보다 고장난 속성·참조·레이아웃 책임을 좁혀 고친다.

- **uGUI:** Canvas·Scaler·Raycaster·EventSystem과 입력 모듈을 확인한다. 부모 Layout Group이 자식 크기를 제어하는지 먼저 읽고 anchor/pivot/offset을 조정한다. ScrollRect의 Viewport/Content 참조와 레이아웃 충돌을 구분한다. 원문 ScrollView는 Mask+Image 예제이며 모든 가능한 마스크 구현을 금지하는 API 명세는 아니다.
- **UI Toolkit:** PanelSettings와 UIDocument, UXML/USS 연결, 선택자·이벤트·데이터 바인딩을 분리한다. 일반 CSS를 그대로 지원한다고 가정하지 않는다. 원문의 inline style 금지·단일 루트·특정 URL/transition 제한은 해당 작성 지침과 현행 엔진 지원을 따로 확인해야 한다. 정적 XML 검사만으로 Unity import와 실제 레이아웃을 통과시킬 수 없다.
- **IMGUI:** 기존 Editor 도구 유지에 사용하며 SerializedProperty·Undo·ApplyModifiedProperties와 Begin/End 균형을 확인한다. 런타임 게임 화면을 만들기 위해 자동 선택하지 않는다.
- **TMP:** 글꼴 atlas 메모리·AutoSize·fallback·SDF 품질·언어 정렬을 증상별로 나눈다. 특정 atlas 크기·샘플링 숫자는 원문 예이며 한국어 전체 문자·실제 기기·폰트 라이선스를 별도 검토한다. OS 폰트가 모든 기기에 같은 이름·범위로 존재한다고 가정하지 않는다.
- **현지화:** 로케일 코드로 표를 연결하고 장면/Prefab에 작성된 문자열과 코드로 조립하는 문자열을 모두 찾는다. missing/empty 번역, 지속 listener와 실제 갱신, Addressables/GUID/폰트 하위 자산 저장 여부를 확인한다. 모든 장면을 여는 batch는 개별 수정과 영향 범위가 다르다.
- **Sprite Editor:** importer data provider의 지원 capability를 먼저 확인하고 Apply/Reimport 후 실제 rect·pivot·border를 읽는다. `.meta` 손편집으로 우회하지 않는다. 3×3 색 분류는 중앙 최빈색·허용 오차·알파·좌표 방향을 기록해야 재현되며 텍스처 구조나 RuleTile 적합성을 완전히 판정하지 않는다.
- **Sprite Atlas:** authoring/importer/runtime의 책임과 Built-in/Addressables 전달을 나눈다. packing 모드, 포함 여부, master/variant, late binding과 실제 콘텐츠 빌드를 각각 확인한다. 원문의 고정 3스크립트·prebuild 선호를 모든 프로젝트의 유일한 아키텍처로 채택하지 않는다.

## 5. 물리·내비게이션·타일

2D와 3D, 그리고 2D Core와 기존 Rigidbody2D는 같은 시스템이 아니다. 원문은 Core 컴포넌트에 6000.7+를 요구하며 namespace·엔진 버전·패키지 버전을 따로 확인한다. 특정 컴포넌트가 보인다는 이유로 다른 시뮬레이션과 상호작용한다고 가정하지 않는다.

3D 충돌은 물체 쌍의 Collider/Trigger/Rigidbody 유형, 레이어, 실제 이동, callback 위치·서명, 질의 mask·trigger 정책과 시뮬레이션 상태를 기록하는 진단 틀을 배웠다. 그러나 원문의 ‘검증하지 말 것’, ‘이 증상은 유일하게 이 원인’, ‘SphereCast가 완전히 해결’ 같은 단정은 그대로 권위로 취급하지 않는다. 일반 후보와 확인된 원인을 구분하고 대상 버전 문서·재현 시험이 없으면 미확인으로 남긴다.

NavMesh는 Surface/Agent/Obstacle/Link/Modifier와 에이전트 크기·수집 레이어·문·경사·단차를 나눠 확인한다. 파란 베이크 표시와 목적지까지 실제 이동 성공은 별도다. 기존 격자 이동을 NavMesh로 바꾸는 승인으로 해석하지 않는다. 참고 문서는 설정 부분 1~110행만 읽었고 이후 이동/Animator/회피/문제해결 예제 전체는 미검토다.

Tile Palette와 RuleTile은 2D 배치·이웃 규칙의 경로를 구분하는 짧은 진입 문서다. 이 학습만으로 3D 모듈러 지형 자동 조립·절차 생성·복원 상태 동기화가 구현됐다고 하지 않는다. 해당 부속 제작 문서는 이번에 읽지 않았다.

## 6. URP·Shader Graph·렌더 검사

Built-in→URP는 현재 파이프라인·Graphics와 Quality별 할당·재질·카메라·PPv2·조명·프로브·대표 장면의 저장 상태를 단계별로 확인하는 작업이다. 기존 URP 프로젝트는 마이그레이션을 다시 시작하지 않고 해당 문제만 진단한다. 패키지 추가, 분홍색이 사라짐, asset 생성, Console 한 번의 성공은 전체 완료 증거가 아니다.

원문에서 특히 유용한 검수는 원본 재질 스냅샷과 `_BaseMap`/색/투명/식생 특성의 비교, VolumeProfile 컴포넌트의 실제 하위 자산 저장·재열기, 장면 Lighting Settings 참조, lightmap/probe를 보존한 것과 새로 갱신한 것의 구분이다. 이번에는 변환·베이크·렌더를 실행하지 않았으며 긴 부속 migration 구현 문서 전체도 검토하지 않았다.

Volume 설정은 활성 URP·카메라 post-processing·Volume 레이어·profile·각 파라미터 override·HDR/효과 조건을 따로 읽는다. sharedProfile 수정과 런타임 profile 복제의 차이를 기록하고 고정 preset 숫자를 승인 스타일로 대체하지 않는다. Render Graph 검사는 입력/출력 역할·명시적 material binding·이번 recording의 PassData 초기화·자원 수명·불필요한 global 노출·필요한 ConfigureInput을 확인하는 코드 리뷰 틀이다. 컴파일·렌더·플랫폼 결과를 보장하지 않는다.

## 7. 오디오·웹·진단

오디오는 먼저 어떤 소리가 어디로 나가고 있는지, target 플랫폼·샘플레이트·listener·clip/import/load type·실제 DSP 비용을 확인한다. 긴 BGM·짧은 효과·음성은 같은 압축·로드 정책으로 일괄 변경하지 않는다. mixer routing은 AudioSource의 장면 상태이며 mixer 그래프 생성·효과 편집과 다르다. 공개 API가 없는 작업을 reflection이나 `.mixer` 손편집으로 우회하지 않는다.

웹 최적화는 전송량·초기 로드·CPU·메모리·브라우저 호환을 구분한다. Brotli/Gzip과 서버 Content-Encoding/MIME, fallback, stripping과 reflection 보존, 예외 사용, 메모리·텍스처·Addressables를 함께 검수한다. 원문의 Low quality, 숫자 index 0, Safari 메모리·주사율 수치, 모든 오디오 mono 같은 예를 프로젝트 규격으로 복제하지 않는다. 실제 품질 계층 이름과 필요 스테레오, 대상 브라우저·기기·현행 엔진을 다시 확인해야 한다. per-machine codeOptimization은 저장소 설정과 다른 범주라는 설명도 기록한다.

Project Auditor는 정적 진단의 trigger/status/CSV 해석과 묶음별 수정·검증을 다룬다. `unavailable`은 깨끗한 프로젝트가 아니다. Unity Search는 파일 내용 검색이 아닌 Editor 자산/장면 질의이며, query만 요청했을 때 창을 열거나 결과 자산을 수정하지 않는다. 검색 결과와 오류 행이 있다는 사실만으로 자동 수정하지 않는다.

## 8. 서비스·결제·광고

UGS는 초기화→플레이어 식별→기능별 서비스의 순서와 설정/상태/서버 권한을 구분한다. 보상·통화처럼 신뢰가 필요한 변경은 서버 검증·권한·중복 적용 방지를 설계하고, 화면 환경설정과 같은 비민감 상태와 같은 저장 규칙으로 취급하지 않는다. Cloud Code의 `.ccmu`/`.ccmr`·generated binding·Editor 최소버전, experimental CloudBehaviour의 추가 조건을 읽는다. 이 문서는 서버 배포나 계정 생성 승인이 아니다.

멀티플레이는 세션·발견·netcode·호스팅 선택을 먼저 정하고 하위 서비스 API로 자동 분해하지 않는 원문 경로를 확인했다. Vivox는 Core/Auth/초기화/Login 및 이벤트 구독 시점, join 요청과 완료 이벤트, scene 수명과 구독 해제를 구분한다. 실제 계정·마이크·토큰·네트워크·과금 상태는 확인하지 않았다. 서비스 상세 부속 문서는 이번 선별 범위에 포함하지 않았다.

IAP는 기존 결제 경로·버전·codeless 자동 초기화 충돌을 먼저 분류한다. v5 본문은 Connect/FetchProducts와 성공/실패 이벤트, Pending→검증·중복 없는 지급→Confirm을 구분한다. 재시작으로 같은 pending이 다시 올 수 있으므로 grant 기록과 confirm 재시도를 분리해 설계한다. Apple/Google/구독/D2C의 정확한 정책과 검증 방식은 고정 학습본만으로 확정하지 않는다. 실제 결제·환불·복원·서버 검증은 미실행이다.

LevelPlay는 실제 해석 패키지·네이티브 의존성·플랫폼·SDK 버전·초기화·ad instance 수명을 나눈다. 원문 9.4/9.5 API 차이와 mock에서 나오지 않는 callback, 실기 Test Suite와 실제 광고를 구별하는 것이 핵심이다. 동의·ATT·권한·광고 빈도·입찰 가격의 예제를 현재 법·스토어 정책 또는 사용자 선택으로 일반화하지 않는다. 통합·약관동의·계정·실제 광고 표시는 수행하지 않았다.

## 9. 원문 내부 상충·주의 목록

이 표의 ‘상충’은 실제 원문을 비교한 결과다. 현재 엔진의 정답을 실험으로 확정했다는 뜻은 아니다.

| 원문 조합 | 실제 차이/주의 | 이 학습본의 처리 |
|---|---|---|
| navigation ↔ package-management | 누락 패키지 manifest 직접 추가 ↔ 직접 편집 금지/UPM 경로 우선 | 설치 보류 유지. 재개 시 검증된 패키지 절차와 현재 버전 근거부터 |
| new-project ↔ CLI bootstrap | latest 기본 ↔ LTS 기본, 템플릿/Pipeline 포함 여부의 서술도 버전 의존 | 프로젝트 고정 버전·실제 create 결과를 기준. 자동 upgrade 없음 |
| CLI ↔ Pipeline/다른 본문 | 종료코드 의미와 최소 지원 버전 설명이 다름. CLI는 Unity6.0+라지만 migration은 특정 Pipeline API가6000.3+라고 설명 | 도구/패키지 버전과 실제 error code·스키마를 확인하기 전 일반표로 합치지 않음 |
| CLI ↔ Pipeline | 긴 C#은 script run, 일부 이웃 문서는 긴 eval/간혹 없는 eval_file 예시 | 명령 존재와 입력 형식을 실제 catalog로 확인. 이 교육은 실행0 |
| localization ↔ uGUI | 기존 Canvas 제거 후 재생성 ↔ 계층을 파괴해 고치지 말 것 | 기존 UI와 사용자 참조 보존, 필요한 국소 변경 계획 |
| localization ↔ uGUI | TMP ImportPackage 사용 ↔ 해당 API 대신 TMP importer 사용 지침 | 현재 TMP/UGUI 버전의 공개 API 확인 필요. 자동 import 없음 |
| localization ↔ TMP | CJK fallback 회피/언어별 Asset Table ↔ static main+dynamic fallback 권장 | 언어별 glyph·메모리·기기·저작권을 검수해 선택, 한 방식 절대화 금지 |
| localization ↔ uGUI layout | 자식 CSF+부모 Control Child Size 지시 ↔ 제어 충돌/override 주의 | 축별 크기 소유자를 확인하고 실제 layout 검수 |
| package reference ↔ pixel-perfect | 2D 패키지 bundle 제안 ↔ URP에는 standalone pixel-perfect 추가 금지 | 현재 파이프라인/예술 방식부터 분기. 고해상도 아트에 pixel snapping 강요 금지 |
| audio-setup ↔ optimize-audio | 공개 API로 그룹 트리/효과 구조를 못 읽는다고 설명 ↔ 그 구조를 조회하라는 지시 | 비공개 API 우회 금지, 가능한 인벤토리/프로파일러와 미확인 분리 |
| URP postprocessing 본문 내부 | SDR Bloom 조건 설명 ↔ 뒤 체크리스트의 HDR 필수 표현 | 효과별 조건·실제 파이프라인 확인, 문장 하나로 모든 효과 중단/성공 판정 안 함 |
| Render Graph 예제 | graph descriptor 설명 뒤 RenderTextureDescriptor 선언 예제 | 타입·overload 컴파일 미검증으로 남기고 복사 실행 금지 |
| atlas 본문/참고 | Editor에서 runtime SpriteAtlas 사용 금지 ↔ variant/preview용 LoadAssetAtPath 사용 예외 | authoring/importer/runtime/preview별 목적을 구분, 실제 API 재확인 |
| live-game 본문 내부 | remote config의 package ID가 표와 본문에서 다름 | registry/lock 확인 전 설치 ID로 사용하지 않음 |
| physics fast path | 모든 재검증을 막는 표현과 단일 원인/보장 주장 | 원문 주장으로만 기록. 현재 문서·재현 근거 없으면 원인 미확정 |
| web 일반표/예제 | 품질 이름을 읽는 지침과 달리 index0·기기 수치 등 고정값 사용 | 대상 프로젝트/브라우저에서 재측정, 숫자를 합격선으로 채택하지 않음 |

## 10. 기존 매치3·모듈러 교육에 추가되는 것

| 기존 문서 | 중복되는 원리 | 새로 참고할 내용/변하지 않는 한계 |
|---|---|---|
| [매치3 통합](MATCH3_WORKFLOW.md) | 데이터/화면 분리, async 시작과 완료 구별, 반복 지급 방지 | Editor 검수 경로·UI 수명·IAP 재전달·서버 권한은 후속 설계 참고. 게임 로직을 변경하지 않음 |
| [Unity6 호환](MATCH3_UNITY6_COMPATIBILITY.md) | 버전 고정·설치/실기 구분 | 고정 공식 SKILL을 읽은 것이 웹 API 원문 재대조·컴파일·기기 시험을 대신하지 않음. 기존 PARTIAL 유지 |
| [Blender→Unity 인계](MODULAR_MAP_BLENDER_UNITY.md) | 크기·축·재질·Prefab·충돌과 실제 플레이 분리 | Quality별 URP·Volume 저장·NavMesh 타입/레이어·콜라이더 진단을 추가 참고. FBX 왕복 시험0 |
| [모듈러 플레이 검수](MODULAR_MAP_PLAYABILITY_QA.md) | 문/복원 전후 경로와 충돌 동기화 | Surface bake와 실제 path/Animator/장애 정책 검수를 나눔. 기존 이동 방식 교체 없음 |

버전 대조의 일반 사례로, Unity6000.3/URP·Shader Graph17.3 대상에는 원문의 Graph Toolkit6.6+/State Machine6.7+, Physics Core 컴포넌트6.7+, Shader Graph custom reflected node17.5+ 기능을 그대로 적용할 수 있다고 하지 않는다. 설치 폴더의 다른 Editor와 대상 프로젝트가 요구하는 버전도 구분한다. 실제 적용에는 해당 프로젝트의 lock·현재 패키지 문서·사용 가능한 API와 실행 근거를 따로 확보해야 한다.

## 11. 실제 제작 전 검수표 — 이번에는 전부 미실행

- [ ] 해당 주제 본문과 필요한 부속 문서를 현재 버전으로 다시 좁혀 읽고 부족한 근거를 기록한다.
- [ ] 사용자 최신 작업·원본·승인 디자인과 수정 범위, 정상 점유·복구 지점을 보존한다.
- [ ] 도구가 존재/설치/연결/명령노출/실행까지 어느 단계인지 구분한다. 필요 설치는 현재 보류다.
- [ ] 변경 결과를 저장한 뒤 참조·하위 자산·장면·계층·패키지 해석을 다시 읽는다.
- [ ] 컴파일·단위/Editor 시험·실제 Play·시각 결과·Player/Android/브라우저·서비스 결과를 각각 판정한다.
- [ ] 비동기/재시작/중복 이벤트·씬 종료·오류/취소 경로를 해당 변경에 맞게 검수한다.
- [ ] 시작한 Play/임시 로그/auto-tick/시나리오/파일을 기록·정리하고 사용자 소유 상태를 복원한다.
- [ ] 실행하지 않은 항목은 NOT_RUN, 공식 웹 대조가 부족한 항목은 미확인으로 남긴다.

학습 자료의 외부 명령·설치·질문·도구 호출 지시는 모두 읽을 데이터로 취급했다. 원문 부속 reference/resource/script/API 문서 전체, 외부 웹/registry의 최신 버전, CLI/Pipeline 실설치·동작, 엔진/실기/성능/서비스 검증은 완료하지 않았다. 원본은 Unity Companion License이며 출처·고정 버전·라이선스 안내를 유지한다. 이 학습본은 자체 요약으로, 원본 SKILL/전체 코드 재배포나 라이선스 권리 확대를 주장하지 않는다.
