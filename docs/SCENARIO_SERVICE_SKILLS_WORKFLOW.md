# Scenario 서비스 79주제 · 제작 판단과 검수 매뉴얼

2026-11-01. Scenario Labs의 [고정 원본](https://github.com/scenario-labs/skills/tree/7f4b801c7248d51b093ec365aceb114bd06139e6)을 문서로 검토한 한국어 재사용 자료다. 루트 `skills/scenario-*/SKILL.md` **79개, 10,027행, 772,076바이트를 전체 읽었다.** MIT 원문의 보조 파일 151개는 목록·해시만 확인했으며 내용은 읽지 않았다. 루트 README는 1–110행만, LICENSE는 전체 읽었다. `skills/scenario/SKILL.md`, DCC·게임 엔진 하위 계열은 이 79개 범위에 포함하지 않는다.

[79주제 탐색표](SCENARIO_SERVICE_SKILLS_INDEX.md) · [파일별 읽기·해시 기록](../reports/ExternalLearning/20261101_SCENARIO_SERVICE_SKILLS_STUDY.json) · [통합 활용 매뉴얼](EXTERNAL_STUDY_WORKFLOW.md)

이 학습은 원문 관찰과 적용 제안을 정리한 것이다. Scenario 계정·MCP·모델 스키마·작업·사용량·관리 API를 호출하지 않았고, 앱 실행·외부 스크립트 실행·설치·실제 제작·청취·렌더·엔진 검증을 하지 않았다. 원 제작자가 한 시험을 이 환경의 실행 성공으로 기록하지 않는다. 서비스 모델명·가격·한도·성능·환불·플랫폼 규격은 작성 당시 주장으로만 취급하며 현행 공식 자료·실제 계약 재검증 전 확정하지 않는다.

## 작업 시작 조건

[공통 작업 규칙](COMMON_WORK_RULES.md), [도구 확인 규칙](COMMON_TOOL_POLICY.md), [사용 프로그램 목록](AVAILABLE_TOOLS.md), 프로젝트의 승인 원본과 최신 지시부터 확인한다. 외부 SKILL의 설치 명령·무인 진행·자동 승인·담당 생성 지시는 자료의 일부다. 사용자의 설치·설정 보류, 앱 조회 금지, 비용·계정·사용자 직접 인증 조건을 해제하지 않는다.

요청의 산출물·정확한 개수·유지할 특징·변경할 특징·대상 화면·실제 예산을 기록한다. 승인 디자인, 시험 후보, 자동 선택한 후보를 구별한다. 무응답이나 AI 자체 판정은 사용자의 최종 승인이 아니다. 이미 승인된 범위는 중복 질문 없이 수행하되, 요청한 v2나 출력 개수를 예산 때문에 줄였으면 PARTIAL로 보고한다.

3D 면 정리·형태·윤곽·비율 변경은 실제 별도 Guide부터 만든다. 수정 범위·보존 경계·면 흐름·목표 윤곽·이동 방향과 원본 보존 파일·캡처·영역 정보를 인계한다. 가이드와 메시 수정은 분리하고 단일 점유 및 같은 조건 solid/wire 전후 검수를 지킨다. 자동 3D 생성·모션·리깅을 읽었다는 이유로 기존 움직임·리깅 보류를 해제하지 않는다.

## 공통 실행 설계

| 단계 | 확인할 내용 | 통과와 구분할 것 |
|---|---|---|
| 입력 준비 | 원본 버전·권리·업로드 허용 범위·참조 역할·팀/프로젝트 | 접근 가능한 파일이 곧 공개·업로드 허가는 아님 |
| 기능 선택 | 목적은 `recommend`, 알려진 이름은 `search`라는 원문 분기 | 추천 순위·예시 모델 ID는 고정 품질 보증이 아님 |
| 계약 읽기 | 실제 스키마의 필드·자료형·배열 여부·상호배타·기본값·범위 | 한 모델의 파라미터를 다른 모델에 복사하지 않음 |
| 견적 | 정확한 입력의 가격과 후속 필수 작업·재시도·부가 비용 | 견적 성공은 실행·시각·입력 유효성 검증과 다름 |
| 제출 기록 | 실제 payload, 원본/참조 ID, 작업 ID, 제출 시각과 상태 | 통신 오류를 즉시 실패나 미제출로 단정하지 않음 |
| 대기 | 기존 작업 ID와 pending 상태를 이어 확인 | 대기 시간 초과만으로 유료 작업 재제출 금지 |
| 검수 | 원본 대비 유지·변경 조건, 실제 파일 속성과 전체 시각/음성 | 성공 상태·썸네일·AI 점수만으로 완료하지 않음 |
| 인계 | 원본·최종 후보·편집 설정·실제 검사·남은 문제·비용 | 파일 생성, 가져오기, 제품 적용, 최종 기기 시험을 분리 |

`model_run`의 `dry_run`·`wait`는 원문에서 최상위 인자다. 카탈로그 `asset_analyze` 같은 도구는 실행 래퍼의 `parameters` 내부에 견적 인자를 둔다. `workflow_run`은 직접 도구 인자다. 로컬 Blender 확장은 별도 `estimate_cost`/`generate`를 쓴다. 이 네 문맥을 섞으면 견적이라고 생각한 호출이 실제 과금될 수 있다. 실행기 `read`/`write` 분류 자체도 무료를 뜻하지 않는다.

참조 하나라도 배열 필드에는 목록을 넣어야 한다는 사례가 반복된다. 잘못된 scalar가 오류 없이 무시되면서 작업이 과금된 사례도 있다. 실제 소비된 입력과 출력 결과를 확인한다. 모델의 batch count는 보통 한 프롬프트의 여러 후보다. 다른 제품·각도·장면을 원하면 항목별 payload가 필요하다.

예산은 이미 제출한 작업의 약정 금액과 남은 필수 공정까지 포함한다. 아직 없는 출력에 임의 대체 입력으로 받은 견적은 후속 비용의 검증된 상한이 아니다. 엄격한 총액이면 가격 근거가 있는 예약 또는 승인된 단계별 지출이 필요하다. 계정 전체 사용량을 특정 작업의 비용이나 남은 잔액으로 오인하지 않는다. 원문에도 실제 작업 비용·견적·부가 Quality Gate 비용 설명이 서로 달라 최종 정산 대조가 필요하다.

## 이미지 · 참조 · 정체성

먼저 그림의 생성, 기존 구도의 편집, 결정적 크기/색 처리, 생성형 아웃페인트를 구분한다. 비율 프리셋과 실제 픽셀 크기는 다르다. 최종 가로·세로·alpha·색 공간·텍스트를 저장 파일에서 확인한다. `transparent` 요청이나 체크무늬 미리보기는 실제 alpha 증거가 아니다. 가장자리 halo와 유리 내부처럼 반투명해야 할 부분도 비교한다.

| 계열 | 본문에서 읽은 계약 차이 | 적용 시 검사 |
|---|---|---|
| GPT Image | 픽셀 격자·quality·입력 fidelity·alpha mask가 member별로 다름 | 보호 영역도 생성형 결과에서 바뀔 수 있음. 이름/가격/alpha 사례를 현행 OpenAI 사실로 확정하지 않음 |
| Seedream | 생성·edit·Layerize 입력과 sequence 지원이 다름 | 단일 입력/배열, 잘린 layer의 bbox·z-order, 반투명 보존 확인 |
| Gemini Image | 이미지 참조와 일부 영상 입력·thinking·검색 필드의 적용 범위가 다름 | member 스키마에 없는 seed/mask를 만들지 않음 |
| Ideogram | 일반 생성·Precise Edit·Transparent·Layerize·Character·배경제거가 별도 | mask 극성·source canvas·prompt 자동 변경·출력 alpha 확인 |
| Reve | `references`와 frame 태그 방식, Remix의 `referenceImages`가 다름 | 태그 번호와 실제 참조 순서 대조 |
| MAI | edit 배열과 Pro edit 단일 이미지 계약이 다름 | 누적 편집의 계보와 승인된 특징 재검수 |
| Luma Image | 수정 대상 source와 guidance imageRef의 역할이 다름 | 입력 한도에 source 포함 여부, 검색 사용 여부 확인 |
| Grok Image | edit는 원본 비율을 따르고 일부 비율 필드를 무시한다는 관찰 | 최종 픽셀과 변경되지 않아야 할 부위 확인 |

참조마다 정체성·스타일·포즈·팔레트·배경 중 역할 하나를 명시한다. 무엇을 복사하지 않을지도 정한다. 스타일 예시의 인물을 승인 캐릭터로 대신하지 않는다. 한 seed가 다른 프롬프트·모델의 정체성을 보장하지 않는다. 승인 hero와 개별 시점을 기준으로 변형한다. 복장처럼 지속되는 변화는 새 baseline을 만든 뒤 이후 컷에 사용한다.

독립 변형 세트는 공통 승인 원본에서 시작한다. 의도된 누적 국소 편집은 선택한 결과에서 이어갈 수 있으나, 변경 이력·보존 조건과 주기적인 원본 대조가 필요하다. 원문의 “항상 baseline”과 “이전 edit 결과 연결”을 목적 구분 없이 동시에 절대 규칙으로 쓰지 않는다.

Library collection·이름 prefix는 검색 관례다. 소유권이나 사용자 승인 상태를 증명하지 않는다. 승인된 개별 뷰와 메타데이터를 보관하고, 뷰 구성이 바뀌면 검토용 sheet를 다시 만든다. 같은 바이트를 재업로드하면 같은 ID로 합쳐질 수 있어 collection 개수를 독립 후보 수로 계산하지 않는다.

## 제품 · 브랜드 · 글자

제품은 실제 승인 사진의 외형·라벨·뚜껑·재질·색과 비교한다. 사진에서 보이지 않는 실제 치수·물성·숨은 면을 생성 이미지로 확인했다고 주장하지 않는다. UGC·광고·썸네일은 제공되거나 승인된 사실·문구만 사용한다. 리뷰 수, 추천사, 가격·효능·실제 없는 게임 기능을 만들어 넣지 않는다.

브랜드 작업은 팔레트·글꼴·여백·로고 원본을 먼저 고정한다. SVG의 정확한 fill/path 수는 렌더를 본 AI 답변이 아니라 파일 구조에서 확인한다. 원문 critic의 “닮지 않았다” 판정은 권리 검증이 아니다. 외부 글꼴의 실제 glyph·라이선스·오프라인 재현 조건도 확인한다.

정확해야 하는 문구는 생성 그림에 맡기지 않고 편집 가능한 텍스트 설정에서 렌더한 뒤 합성하는 절차가 유용하다. 최종 이미지에서 철자·기호·대소문자·줄바꿈·대비·실제 화면 크기·잘림을 확인한다. deterministic 렌더도 누락 글꼴이나 overflow를 막아주지 않는다. 템플릿의 raw HTML 치환은 신뢰할 수 있는 입력에 한정하고, PNG에 내장되는 payload에는 비밀정보를 넣지 않는다. 원문의 새 패키지·브라우저 설치 예제는 실행하지 않는다.

Formats는 승인 master에서 파생하고 파생본의 반복 재생성을 피한다. crop·resize·outpaint·재구성의 차이를 설명하고 필요한 구도를 보존한다. 썸네일은 원본 크기와 실제 작은 미리보기를 둘 다 확인한다. 가독성 검수를 클릭률 개선 실험으로 보고하지 않는다.

## 분석 · Quality Gate · 모델 비교

`asset_caption`·`asset_describe`·`asset_analyze`·`asset_detect`의 목적은 다르다. 원문 `asset_analyze`는 여러 이미지를 받지만 `num_outputs`는 입력 이미지 수가 아니라 답변 수다. 항목별 판정 형식을 지정한다. `asset_detect`의 기본 배경제거는 장면 전체의 depth/pose 맥락을 없앨 수 있어 의도에 맞춰 확인한다. 의미 검색이 켜지면 최신 정렬이 무시되는 사례, image와 images의 상호배타도 기록한다.

Quality Gate는 저장 판정이 없으면 평범한 호출도 새 분석과 과금으로 이어질 수 있다는 원문 계약이다. 재평가 `rerun`은 기존 결과를 대체한다. add-on 미지원 오류를 반복하지 않는다. 이미지 점수는 원본 정체성·물리적 구조·손가락/바퀴 수·접촉·모든 panel의 합격을 보장하지 않는다. 합성 전체가 아니라 거부할 수 있는 최소 단위로 검사하며 점수보다 실제 결함이 고쳐졌는지 본다.

모델 비교는 기준을 먼저 쓰고 동일 prompt bytes·참조·출력 수를 유지한다. 해상도·prompt rewrite·필수 tuning처럼 같게 할 수 없는 조건은 표에 드러낸다. 서로 다른 모델에 같은 seed를 준다고 같은 샘플 조건이 되지 않는다. 추천 추정치와 실제 billed cost·queue 포함 지연을 구분한다. 작은 sheet 다음 원본 크기, 영상은 전체 시간 범위와 실시간 재생까지 확인한다. 승자는 해당 brief·샘플 수·당시 카탈로그의 결과다.

Refine loop는 합격 기준과 시도/비용 한도를 정하고 국소 편집·재생성·후처리 중 필요한 경로를 고른다. 동일 결함이 반복되면 문구만 바꾸며 무한 지출하지 않는다. 실패 이유와 최선 후보를 보존해 PARTIAL로 인계한다. 원문의 3회 기본값은 모든 프로젝트의 허용 횟수가 아니다.

## 맞춤 모델 · 음성 학습

한 번의 결과는 먼저 프롬프트·승인 참조·제어 맵으로 해결 가능한지 본다. 세트 전체에서 drift가 지속될 때만 승인된 학습을 검토한다. 가짜로 다양해 보이는 한 장의 파생 이미지들은 독립된 정체성 신호가 부족할 수 있다. dataset 내용·캡션·다양성·권리와 보유 예산을 확인한다.

원문은 업로드 chunk·중복 첨부 금지·plan dataset 한도와 동시 학습 한도를 구분한다. chunk를 나눈다고 계정 한도를 우회할 수 없다. `configure`의 견적과 `start`의 실제 launch/job ID를 구분한다. 다중 epoch preview를 얻는 `sample_prompts`와 edit 계열 source 이미지의 대응도 member별 계약이다. base `runs_as`/`run_with` 불일치를 학습 실패로 오인해 재학습하지 않는다. 최적 epoch 선택과 마지막 weights 그대로 사용한 상태를 구별한다.

이 79본문은 base-model-selection·dataset-curation 보조 본문을 대신하지 않는다. 음성 clone·훈련은 해당 권리·동의·사용 목적과 현행 도구 계약을 별도 확인해야 한다. 이 학습에서는 모델·음성을 훈련하지 않았다.

## 게임 2D · 스프라이트 · 반복 애니메이션

게임 UI는 alpha bbox·고정 canvas·foot anchor·9-slice corners와 stretch 영역을 구분한다. baked shadow·glow가 참조에서 두꺼워지거나 형태로 복사될 수 있다. 실제 엔진 배경색에서 halo·반투명 내부를 확인한다. 픽셀 아트는 팔레트·격자·nearest 표시·프레임 공통 크기를 확인한다.

등각 ground footprint는 높이 솟은 건물·나무의 전체 실루엣이 아니다. mask용 base canvas, 극성·alpha 의미와 편집 바깥 변화량을 확인한 뒤 작은 조립 지도로 접합·겹침·시점을 검사한다. Wang 전환 세트를 특정 엔진의 47-tile blob으로 자동 취급하지 않는다.

Parallax는 실제 개별 plane과 구멍·뒤쪽 채움·스크롤 bleed가 필요하다. 한 장에 “여러 layer”를 그린 결과는 layer 파일이 아니다. plane offset 미리보기로 중복 지평선·남은 전경·halo를 찾고 파일별 alpha를 검사한다.

Sprite animation은 요구가 정확한 grid인지, native pixel cycle인지, keyframe 제어인지 먼저 고른다. 실제 cell/pose 수·타일 크기·동작을 확인하고 몸 bbox·수평 중심·발 기준선을 맞춘다. 영상 추출의 ID 순서도 틀린 원문 사례가 있어 개수와 시간 연속성을 대조하고 자체 frame→output 대응 목록을 유지한다. timestamps나 검색 정렬로 순서를 재구성하지 않는다.

반복 경계의 픽셀 차이를 그 window 내부의 움직임과 비교하는 수치는 후보 탐색의 보조 근거다. 발 접촉·속도·가속도·실시간 재생을 대신하지 않는다. 첫 frame의 재렌더 jump와 정지 tail을 피하는 내부 window 탐색을 먼저 검토한다. GIF의 시간 양자화·중복 frame·pingpong 설정과 실제 다운로드 재생을 확인한다.

Side-view 예제의 고정 magenta는 의상·무기 motion blur까지 지울 수 있다. key 색 겹침과 빠른 프레임을 검사한다. 비대칭 장비·무기 손을 단순 좌우 반전하지 않는다. loop 수치·색 수·캐릭터 높이·ground sink 값은 사례값이다. 플랫폼은 cap-middle-cap, 환경은 실제 반복 검수, 한 레벨의 사용 검수 후 나머지로 확대한다. 현재 게임을 실행한 결과는 아니다.

## 3D 생성 · 표면 · 공간

이미지→3D는 숨은 면과 구조를 추론한다. 보기 좋은 mesh, UV가 있는 mesh, 게임에서 쓸 수 있는 mesh는 별개다. 형상·위치·크기·축·origin·부품·poly/triangle/quad 수·재질·UV·법선과 출력 형식을 단계마다 확인한다. `hasUVs`는 깨끗한 layout 증거가 아니다. 자동 rig는 기존 skeleton 보존이나 변형 품질의 증거가 아니다.

| 계열/공정 | 주요 구분 | 남는 검사 |
|---|---|---|
| Meshy | shouldRemesh가 꺼진 polycount, image가 texture text를 대체, Ultra 입력 수, Animation 내부 rig | 실제 면 수·출력 maps·UV cap·rig 중복 작업 비용 |
| Rodin | Full/Fast 필드·tier·HighPack 형태, Bang segmentation와 재질 재생성 | quad/tri 예산·면 증가·예상치 않은 재질 변경 |
| Sparc3D | prompt 없는 이미지 위치별 입력, Portrait specialist, member별 resolution/face 존재 | front/back/left/right 순서·실제 출력·긴 작업 대기 |
| 일반 3D edit | prompt reshape가 faceBudget을 무시한 사례 | 지정하지 않은 부품·재질·topology 변동, 재리메시 필요성 |
| 저장/변환 | stored GLB 원본과 format 지정 재출력은 다름, GLB는 삼각화 | quad FBX 보존·PBR 누락·애니메이션 변환 보존 확인 |
| Video-to-motion | mesh auto-rig와 기존 rig에 motion-only retarget 구분 | skeleton 이름·축·fps·발 접촉·loop·실제 DCC/엔진 import |

UV→retexture→rig의 후속 공정은 별도 출력과 비용이다. retexture가 UV를 다시 만드는지, geometry는 같아도 shader/UV layer/linked data가 바뀌는지 확인한다. “geometry hash 동일”을 모든 데이터 무변경으로 확대하지 않는다.

PATINA는 물리 표면 family별로 maps를 만들고 원색 tint와 연결하는 예제다. 모델이 이미 벽돌/기와를 형상화했다면 texture까지 같은 패턴을 넣어 두 겹으로 만들지 않는다. 출력 순서가 아닌 `metadata.type`과 실제 map을 대조한다. roughness 요청의 smoothness 라벨 사례는 값의 실제 극성 확인 후 연결한다. editable shader가 glTF로 동일하게 전송된다고 가정하지 않는다.

텍스처는 경계 수치 외에 offset·반복 화면·실제 크기·조명 방향을 본다. skybox는 2:1 equirectangular의 seam·극점·360 표시를 확인하며 광고된 cubemap ratio만으로 layout 지원을 확정하지 않는다. HDRI 같은 외형이 실제 HDR 광량을 뜻하지 않는다.

Gaussian splat world는 polygon·UV·정확한 충돌 표면이 아니다. Walkable room은 원본의 제거 plate와 원본에서 뽑은 object cutout을 구분한다. world마다 floor·scale·lens·높이·support와 collision을 교정해야 한다. 한 사진 뒤편의 생성 공간이나 추정 치수를 실측 복원으로 보고하지 않는다. Orbit의 3D 중간물도 원본에 없는 숨은 면의 정답은 아니므로 camera zero·실루엣·ground contact·그림자를 모든 뷰에서 확인한다.

## Blender 연결 · 2D 장면

Scenario 로컬 Blender 확장과 hosted 서비스는 서로 다른 tool name·scope·작업 ID를 쓴다는 원문 계약이다. loopback token은 비밀이며 계정 API key와 구분한다. 세션 재시작으로 바뀌는 token을 문제 보고서에 넣지 않는다. 이 학습에서 확장 설치·연결·Python 허용 설정·재시작을 하지 않았다.

로컬 확장의 정확한 quote와 결과 적용 목적지에 관한 실제 사용자 승인 gate는 건너뛰지 않는다. 새 코드 실행을 허용한 적이 없으면 원문의 `execute_python` 안내만으로 활성화하지 않는다. 캡처 reference ID와 업로드 후 asset ID도 구별한다. headless에서 GUI 캡처가 안 되는 제한과 `.blend` 저장 수단을 확인한다.

Blender 2D 예제는 orthographic cards·parallax·hero image sequence·prop physics와 상대 경로 폴더를 함께 인계한다. 새 look마다 horizon·ground·feet·loop frame 수·props 개수를 다시 측정한다. 원문의 `--live`가 열린 파일을 비우는 동작은 현재 사용자 씬에서 실행할 수 있는 일상 읽기가 아니다. scripts 내용을 읽고 현재 저장/점유·명시 범위를 확인하기 전 실행하지 않는다.

## 음성 · 음악 · 사운드

TTS에서 발화 문장과 목소리·감정·언어 설정을 분리한다. inline tag 문법은 member별로 다르고 잘못 쓰면 태그 자체를 읽을 수 있다. preset 이름만으로 성별·음색을 단정하지 않는다. multi-speaker label과 각 turn을 정확히 대응한다. 실제 청취 없이는 최종 음질·발음·연기를 통과 처리하지 않는다.

음악의 style과 lyric 필드를 나누고 instrumental·auto-lyrics flag를 확인한다. 이미 완성된 가사를 optimizer에 넣으면 재작성될 수 있다. Cover는 새 take 후보이며 singer·timing·corrected words 보존을 보장하지 않는다. Repaint는 선택 구간을 재생성하고 목소리도 바뀔 수 있다. 교체 경계를 청취·대조하기 전 master를 덮어쓰지 않는다. 곡의 연장은 repaint와 별도 경로다.

ElevenLabs의 v3 tags/다른 TTS dials, voiceId와 preset 우선순위, MiniMax Cover의 asset ID 입력, ACE의 stem enum·Turbo/Quality·no-seed, Sonilo의 contiguous segments와 반환 audio/mux video 구분을 각각 확인한다. Sonilo music mux의 speech 보존 설정이 기존 효과음까지 보존한다는 뜻은 아니다. 효과·음악은 독립 tracks로 만들고 승인된 편집 경로에서 합칠 수 있다.

MIME와 실제 probe로 WAV/MP3/FLAC 등 파일 형식을 확인한다. 다운로드 인자의 format이 audio/video 변환 기능이라는 가정은 하지 않는다. 예시 작사법·BPM·말 빠르기는 실제 길이·청취로 확인할 출발점이며 현지 언어에 그대로 적용할 기준이 아니다.

## 영상 생성 · 편집 · 자막

First frame은 시작 구도, reference는 정체성/스타일이라는 목적 차이가 있다. 여러 member가 두 입력을 함께 받지 않는다. 마지막 frame은 첫 frame을 요구할 수 있다. duration은 숫자·숫자 문자열·단위 문자열·enum·Auto·source 상속 등 서로 다르다. extend가 전체 영상인지 추가 tail인지, lead-in을 포함하는지도 다르므로 실제 길이와 연결 경계를 측정한다.

| 계열 | 다시 읽어야 할 차이 |
|---|---|
| Kling | 전용/V3 Omni의 multiPrompt array/JSON 문자열, duration 타입, element 수, base/feature video, audio 상호배타 |
| Veo | image/reference 배타, reference mode 길이, full/Fast/Lite 차이, audio 필수와 extend source 규격 |
| Gemini Omni | 생성/참조/edit/extend member, source motion과 새 look, appended duration, audio toggle 없음 주장 |
| Luma | `5s`/`10s` 옵션 결합, Edit/Modify의 필드와 strength, Reframe의 outpaint |
| Runway | Gen4.5 첫 이미지의 ratio 우선, Aleph reference 배열 배타 및 파일 바이트/길이 상한 |
| Grok | I2V/R2V 분리, 참조 태그, edit truncation, extend 추가 초와 member별 resolution |
| Wan | 세대별 size/resolution, frame count/fps match flag, end-image/video 배타, audio 보존 모드 |
| Vidu | generationType와 이미지 수/순서, tier별 cap, 제한된 reference video, audio가 BGM이라는 원문 계약 |
| MiniMax | H3/Max/Turbo·대소문자 resolution·reference 결합·Insert/Recast·continuation lead-in |
| Seedance | mode를 정하는 입력, edit `-1`, extend tail, 역할 태그, Auto 비용, draft와 completion |

고해상도 재생성은 같은 take의 확대가 아니다. Seedance draft의 original asset ID·유효 기간·completion은 별도 계약이며 원문 7일/1080p 주장은 현행 확인이 필요하다. draft+completion 한 개가 곧 비용 절감은 아니다. 버릴 take가 많을 때의 전체 산술을 비교한다. 완료본도 draft와 실제 표본·길이·fps·file MIME를 대조한다.

Dubbing은 번역 음성, lipsync는 입 영역, portrait talking avatar는 새로운 전신/얼굴 연기라는 차이가 있다. 립싱크 전 얼굴 크기·각도·가림·blur·speaker 선택과 입력 상한을 확인한다. 성공 상태만으로 입이 움직였다고 보고하지 않는다. source와 출력의 같은 시간 입 모양, 전체 표본 및 실시간 영상·음성을 확인한다.

결정적 편집은 trim·split·resize·효과, 생성형 reframe은 그림을 추가하는 작업이다. contain/cover/stretch와 custom canvas의 보존·crop·왜곡을 구분한다. 투명 영상은 실제 codec/alpha decoding/엔진 지원까지 확인한다. 영상 재생 목록에서 추출 frames의 순서·누락 개수도 검증한다.

자막은 clean master의 실제 음성에서 timing을 얻고 원고와 철자를 대조한다. supplied SRT와 style preset의 casing·segmentation·animation이 최종 화면을 바꿀 수 있다. 원문의 Caption Studio `subtitles` inline base64 사례는 현행 계약 검증 없이 다른 입력에 일반화하지 않는다. asset ID를 넣고도 성공하며 0 captions가 나온 사례 때문에 segment 수·실제 glyph·cue 안과 경계 전후 frame을 검사한다. 정확한 SRT만으로 render timing을 통과시키지 않는다. 한국어를 라틴 문자 줄 길이 기준으로 자동 자르지 않는다.

## 조립 · 스토리 · 음악 영상

Concat은 순서 연결, compositor는 절대 시간 layer다. transition 수와 clip 수, start/end와 trim amounts, 전체 duration과 layer duration, canvas 숫자와 layer 문자열 크기를 구분한다. 원문의 0.1초 step을 frame 정확도로 광고하지 않는다. 소수 fps의 반올림·마지막 frame·자막 tail·음성 길이를 별도 측정한다. concat의 audio drift 사례가 있어 streams 길이·입/타격 cue를 실제 대조한다. compositor 사용도 무조건 sync 보장은 아니다.

원본 clean master, 실제 제출 layer payload, measured timings, 음성 원고·설정, title PNG와 layout, corrected SRT, output ID를 남긴다. 이 recipe는 네이티브 편집 프로젝트나 다른 환경에서 재실행 성공했다는 뜻이 아니다.

스토리/만화는 panel 단위로 고정 cast와 setting을 사용하고 lettering은 후처리한다. 축·화면의 좌우·facing·coverage와 앞뒤 상태를 확인한다. 연속 동작은 shot의 entry/exit pose뿐 아니라 위치도 연결한다. sheet와 board의 숫자·화살표가 영상에 누출되는지 전체 범위에서 본다. 검토한 storyboard는 실제 사용자 승인이나 자연스러운 choreography의 증거가 아니다.

음악 영상은 승인 master를 보존하고 실제 beat·word onset을 측정한다. hash는 원본 파일 보존 증거이며 AAC mix/re-encode된 배포 음원이 bit 동일하다는 뜻은 아니다. 시각 수정은 승인 음원을 재사용하고 승인된 음원 수정만 새 master 버전으로 만든다. sheet·spectrogram·상관 계수는 청취를 대신하지 않는다. shot beat의 local time은 master 시각·timeline 위치·head trim을 함께 계산한다.

Motion Loops는 순수 시간 함수·주기·고정 난수·정수 반복 이동으로 seam을 설계하고 page와 encoded file을 따로 확인한다. Kinetic 예제는 lyrics·mattes·tracking·JS timing·smoke AV 확인 뒤 전체 render를 한다. Apple Vision/OS별 dependency lock·새 sub-agent 구성은 이 Windows 환경의 실행 가능성이나 담당 생성 승인이 아니다. 규칙적 수학·deterministic 코드도 flicker·눈부심·좋은 디자인을 보장하지 않는다. 원문의 초당 flash 수 한 줄만으로 광과민 안전 판정을 내리지 않는다.

## 광고 변형 · 리캐스트 · 펫

광고 variants는 원본과 요청 delta를 고정한 독립 결과이며 옵션을 자동 Cartesian 조합하지 않는다. 선택 변형의 revision은 선택본에서 시작한다는 의도를 존중한다. 상태를 planned/submitted/pending/failed/verified로 남기고 실패 항목만 복구한다. gameplay 보존이 요구되면 생성형 배경 교체가 UI·기하·동작까지 바꿀 수 있음을 검사한다. hook endpoint의 포함 여부, overlay 존재, audio sync를 실제 출력에서 본다.

Recast는 승인 정체성·복장·장면 역할을 나누고 source firstFrame 기반의 장식 plate가 카메라·바닥과 맞는지 비교한다. 원래 음원을 따로 보존하고 출력 motion과 음원의 offset을 대조한다. 타임라인 step보다 작은 잔차와 상관 부족을 미검증으로 남긴다. Fan cam도 정체성 사진→방송 구도 still→영상의 단계마다 비교한다. 외형 동의·권리·합성물 오인 방지와 배포 범위를 따로 확인한다.

Pet create/update 본문은 row 단위 생성·기준선·jump·좌우 반전·16방향 의미·최종 bytes 검수의 원리를 준다. 원문 v1/v2 크기와 Codex/ChatGPT 업로드 경로·모델 ID는 현행 공식 Pets 도구 재확인 전 채택하지 않는다. 현재 연결된 전용 plugin/skill이 있으면 그 계약을 우선 확인한다. 생성 파일·로컬 package·Library 저장·활성화는 서로 다른 완료다. 원본 sheet를 보존하고 수정 안 한 row의 bytes를 비교한다. rename은 identity ID와 구분하고 새 의상은 전체 동작에서 일관되게 검사한다. 실제 펫 생성·설치·활성화는 하지 않았다.

## 워크플로 · 관리자 · 보고

Workflow의 input key는 label이나 오래된 editor node name이 아니라 실행 계약의 `name`이다. `required` object의 존재와 `required.always` 값을 구분한다. file array가 여러 항목별 실행을 뜻하지 않는다. `forEach`가 있어야 개별 모델 실행이 되는 경우, 견적이 한 iteration만 가격을 매기는 원문 사례가 있어 개수·반복별 입력 가격을 확인한다.

`workflow_run` dry run이 입력 길이를 검증한다는 원문 사실은 model_run 전체에 일반화할 수 없다. 목록을 작게 제한하고 pagination 방식, 빈 client-filtered page와 다음 토큰을 구분한다. parent job 비용 0을 전체 비용으로 보고하지 않고 child job·반복·부가 비용까지 대응한다. 승인 node는 정확한 workflow/run/node와 사용자의 실제 승인을 확인한다.

Authoring은 원본 graph를 보존하고 전체 `editor_info`를 read-modify-write한다는 계약이다. publish 전까지 실행 flow가 이전 버전일 수 있다. create 부분 성공의 ID를 무시하고 재생성하지 않는다. reverse edge 방향·handle·output pin·CEL·foreign graph mapping은 보조 reference와 현행 계약을 읽기 전 구현 완료로 주장하지 않는다. 공개·삭제·권한 변경은 학습 승인에 포함되지 않는다.

Team admin의 scope는 권한 부여가 아니다. cap의 0/null/-1, block/allow 추가의 반대 의미, additive tags와 전체 교체, membership·project 삭제를 구분한다. Analytics는 UTC와 명시 기간·페이지·cache freshness·통화/credit 단위를 기록한다. 사용자 중복 집계·할인 이중 차감·성립하지 않는 비례 join을 피한다. report는 필요한 최소 재현만 담고 secret·signed URL·개인/팀 결제정보를 제외한다. 지원문의·버그 공개 발송은 실제 승인 범위를 따른다.

## 원문 교차 검토와 교정

| 읽은 원문 주장/상충 | 이 매뉴얼의 적용 기준 |
|---|---|
| undated usage가 lifetime(team-admin 등) 대 default 31일(admin-analytics) | 명시 기간·응답 범위·현행 계약을 확인. 두 값을 합쳐 새 사실로 쓰지 않음 |
| consistency는 sheet 참조 금지, identity-library/reel-recast는 sheet 허용·권장 | 개별 승인 뷰 우선. 모델·작업별 좁은 검증 전 절대 허용/금지로 일반화하지 않음 |
| baseline만 사용 대 일부 editor의 이전 결과 연결 | 독립 세트와 의도된 누적 편집을 구분하고 계보·원본 대조 |
| 여러 본문은 local 편집 금지, color-grade/motion-loops/side-view/kinetic는 local 마감 | 서비스 중심 workflow 설명으로 읽음. 기존 승인 도구·산출물·검증 가능성으로 선택 |
| UGC/fan-cam은 platform 추출만 감사 가능 대 다른 본문은 local 표본 검수 | 원본 hash·frame 시각·추출 설정·판정 기록으로 추적. 유료 추출만 증거로 강제하지 않음 |
| Caption Studio fixed ID 대 recommend로 captioner 발견 | 요청한 기능과 실제 현행 제공 계약을 확인 |
| 일반 discover 원칙 대 pet 특정 생성 모델 순서 | 당시 recipe. 새 모델/설치 승인이나 현행 품질 순위 아님 |
| jobs_wait 실제 비용 대 pet의 quote가 add-on 포함 더 정확 | 견적·작업 billed·부가 분석·정산 차이를 기록. 현재 결제 계약 확인 |
| 모든 engine texture는 정사각 power-of-two 필요 | 보편 규칙 채택 안 함. 대상 import·압축·mip·플랫폼 예산 확인 |
| skybox 끝 열이 nearzero면 seamfree | 이웃 sample은 반드시 같지 않음. 실제 360·pole·기울기·반복 화면 대조 |
| source의 provider 전환/이름 삭제를 moderation 복구 기본으로 제안 | 조직 gate·정상 거절·권리 조건 우회 금지. 오류 분류·정직한 설명 수정·허용된 지원 경로만 |
| 원문 “unattended 승인 대신 진행” | 이미 승인된 범위 내 후보 판단만. 새 비용·권한·필수 직접 승인 대체 불가 |
| 특정 triangle·loops·pixel·fps·기간·flash 수가 성공 조건 | 원 제작자 사례값. 현재 대상·카메라·실제 환경에서 재검증 |
| 로컬 코드 deterministic이면 exact·loop·무비용 | 계산 재현성과 시각 품질·영상 인코딩·자원 비용을 분리 |
| 요청 ratio/duration·completed·quality score가 성공 | 실제 파일·전체 시간·원본 대조와 최종 표시/청취로 검수 |

## 기존 자료실과 함께 적용

| 기존 정본 | 이번 79본문의 보강 | 대체하지 않는 근거 |
|---|---|---|
| [심리스 검수](SEAMLESS_TEXTURE_QA.md) | 생성/업스케일 입력·PBR 출력 분기 | 경계값뿐 아니라 기울기·offset·3×3 반복·실제 조명의 검수가 우선. 첫/끝 열 강제 동일화 금지 |
| [UV·Texture Set 인계](UV_TEXTURE_SETS_HANDOFF.md) | 생성 mesh의 UV→retexture 단계, metadata map 역할 | UV/재질/이미지는 서로 다름. 채널 의미·색 공간·베이크·실제 shader 확인 |
| [Blender→Unity](MODULAR_MAP_BLENDER_UNITY.md) | GLB/FBX·quad·PBR·scale·rig 반환 주의 | 파일 생성→격리 import→엔진→기기 검증 분리. 자동 생성은 모바일/콜라이더 합격 아님 |
| [통합 활용](EXTERNAL_STUDY_WORKFLOW.md) | API/비용·멀티미디어·관리 기능 경계 | 실제 Guide·원본 보존·단일 점유·실행 미검증 유지 |
| [외부 교정표](EXTERNAL_STUDY_CORRECTIONS.md) | 서비스 본문 내부 상충과 과도한 단정 추가 | 문서 학습을 현행 API나 실제 제품 검수 PASS로 승격하지 않음 |

위 기존 5개 문서는 이번 종합 정리에서 본문을 대조했다. 다른 링크는 주제 연결이며 이번에 그 하위 전체를 다시 읽었다는 뜻은 아니다. 79본문이 참조하는 scripts·reference·template 151개는 해시 목록만 남겼다. 실제 구현에서 필요하면 승인된 학습 범위와 보류를 확인해 해당 내용을 먼저 읽고 현재 도구 계약을 대조한다.

## 결과 인수 기록

인수 기록은 산출물·원본 버전·실제 제출 recipe·실제 검사 시점/조건·비용·남은 결함을 함께 적는다. `문서 검토 완료`, `파일 생성`, `저장/재열기`, `시각/청취`, `엔진 적용`, `기기/배포`를 각각 판정한다. 이번 결과는 **79본문 문서 검토와 자체 매뉴얼 정적 검증 완료**이며 실행·제작 검증은 **NOT_RUN**이다. 전체 315개 학습의 완료 판정이나 다른 담당의 실기 결과를 대신하지 않는다.
