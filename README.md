# 공용 3D · 텍스처 · 게임 제작 교육 자료실

2026-11-03 예외: Blender 작업 전 [애드온 목록](docs/BLENDER_ADDONS.md)을 확인·활용하고, 작업에 필요한 애드온은 **추가 승인 없이 설치·활성화·호환/기능 확인**한다. 이 범위의 설치 보류는 해제한다. 새 유료 구매·사용자 직접 인증·도구 필수 승인·다른 앱 금지는 유지하며 [상세 규칙](docs/COMMON_TOOL_POLICY.md#blender-애드온-사전-확인활용설치-상시-승인)을 따른다.

Unity 매치3·Blender·Maya·RetopoFlow·Substance 3D Painter 강좌를 바탕으로 작성한 한국어 재사용 교육자료입니다. 이 저장소는 여러 프로젝트에서 공유하는 공개 교육 정본입니다. 새 매뉴얼은 이곳에서만 편집·게시하고 개발 저장소에는 정본 링크를 남깁니다. [편집·게시 규칙](CONTRIBUTING.md)을 따릅니다.

## 다른 GPT에서 사용하기

다음 저장소 주소를 전달하고 이렇게 요청하세요.

> README와 해당 주제의 docs 문서, reports/VideoLearning 학습 범위를 읽어줘. 영상에서 직접 확인한 내용·제작 원리·프로젝트 적용 제안·미검증 사항을 구분해줘. 교육 완료를 실제 게임/에셋 제작·엔진/리깅 검증 완료로 취급하지 마.

**전체 링크:** https://github.com/gnogus-ux/PuzzleIsland-Education

## 공통 도구와 사전 확인

[Windows 앱 캐시 이전·검증](docs/WINDOWS_APP_CACHE_RELOCATION.md): 순수 캐시와 실행 환경 구분, 잠금·MSIX 경로와 원본 복구 절차.

프로젝트 작업 전 [공통 작업·인계·검수 규칙](docs/COMMON_WORK_RULES.md)을 읽습니다. 승인 원본 보존, 실제 3D 가이드, 단일 점유, 동일 조건 검수, 사용량 인계, 교육 정본과 승인된 새 창 인수·보관 절차를 함께 따릅니다. 프로젝트별 승인 범위와 한시적 보류·조회 금지는 유지합니다.

새 대화·새 담당에게 인계할 때도 [공통규칙 숙지 절차](docs/COMMON_WORK_RULES.md#인수-전-공통규칙-숙지)를 적용합니다. 인수자가 정본과 적용 지침을 직접 읽고 승인 범위·보류·금지를 확인한 뒤 인수 완료를 보고합니다. 링크를 전달한 사실만으로 숙지나 인수를 완료 처리하지 않습니다.

이미 승인한 일상 작업은 재확인하지 않습니다. 전문 창 배정 전에 실제 작업 경로와 쓰기 권한·승인 모드를 먼저 맞추고, 전역 기본값과 현재 창의 권한을 구별합니다. [반복 승인 방지](docs/COMMON_WORK_RULES.md#반복-승인-방지)와 [권한 사전 확인 절차](docs/COMMON_TOOL_POLICY.md#반복-승인-방지와-실제-권한-확인)를 따르며, 필수 사용자 승인은 우회하지 않습니다.

[대용량 조회·연결 장애](docs/COMMON_WORK_RULES.md#연결-장애와-대용량-조회)는 같은 원칙으로 처리합니다. 조회량을 제한하고, 끊긴 원격 실행의 종료·점유 해제를 추정하지 않으며, 중복 실행·강제 재시작 없이 원본을 보존합니다. [최소 조회·복구 절차](docs/COMMON_TOOL_POLICY.md#조회량-제한과-연결-장애-처리)를 적용하고 독립 작업은 병행합니다.

작업할 때는 항상 현재 작업의 [참고 자료를 직접 확인](docs/COMMON_WORK_RULES.md#작업별-참고-자료-상시-확인)합니다. 첨부·지정·승인 자료의 출처·버전·적용 범위와 필요한 기준을 확인하며 다음 단계·인수 후 작업과 결과 검수에도 실제 참고와 대조합니다.

제작·분석·자동화 도구를 새로 만들거나 설치하기 전에 [사용 프로그램 목록](docs/AVAILABLE_TOOLS.md)과 [도구 확인 공통 규칙](docs/COMMON_TOOL_POLICY.md)을 읽습니다. 설치만 확인된 도구와 실제 실행 가능한 범위를 구별합니다. 필요한 도구가 없거나 미완료·사용 불가·미검증이면 명칭·용도·부족한 점·설치/계정/비용 필요 여부를 사용자에게 요청합니다. 현재 설치·설정은 재개 지시 전까지 보류합니다.

다음 작업을 시작한다고 판단할 때마다 아래 교육 목록과 매뉴얼 본문에서 관련 내용을 먼저 검색하고 필요한 절을 읽습니다. 같은 대화의 다음 단계·인수 후 작업도 포함하며 사용자의 재지시를 기다리지 않습니다. **매뉴얼을 읽지 않은 임의 작업은 금지합니다.** 매뉴얼이 없거나 내용·버전 근거가 부족하면 필요한 내용·자료를 요청하고 **관련 교육자료3개를 검색·실제 학습해 매뉴얼을 작성·보강한 뒤** 승인된 작업에 적용합니다. 검색·열람·적용 범위를 기록하고 [상세 절차](docs/COMMON_TOOL_POLICY.md#매뉴얼-미확인-작업-금지와-부재-시-3개-자료-학습)를 따릅니다. 이 범위의 학습·작성 승인은 반복 질문하지 않습니다.

Claude도 공통규칙과 기존 매뉴얼을 직접 읽고 제작에 적용합니다. **교육이 필요하면 Codex에게 알리며, 신규 교육·자료3개 학습·매뉴얼 작성·보강은 Codex가 담당합니다. Claude에게 교육을 맡기지 않습니다.** [역할 구분](docs/COMMON_WORK_RULES.md#claude는-규칙-숙지제작-담당-교육은-codex-담당)과 [Claude용 지침](docs/CLAUDE_RULES_AND_LIBRARY.md)을 함께 적용합니다.

## 외부 제작자의 교육·작업 매뉴얼

요청한 외부 저장소 4개를 원본 버전으로 고정해 가져왔습니다. [외부 자료 전체 목록](docs/EXTERNAL_LEARNING_SOURCES.md)에서 Blender·Unity·게임 제작 자료와 라이선스를 확인하세요. 후속 문서 학습은 [통합 활용 매뉴얼](docs/EXTERNAL_STUDY_WORKFLOW.md)과 [원문 교차 검토·교정표](docs/EXTERNAL_STUDY_CORRECTIONS.md)에서 시작합니다. 원문 문서 검토와 실제 앱 실행·제작 검증을 구별하며, 스킬 설치·외부 코드 실행은 수행하지 않았습니다.

4개 저장소의 **SKILL 본문 315개**를 읽고 선별 참고자료·기존 교육과 대조해 자체 문서 20개를 추가했습니다. [파일별 학습 범위와 검증 기록](reports/ExternalLearning/20261101_EXTERNAL_SKILLS_STUDY.json)을 함께 확인하세요. 부속 파일 전체·외부 영상 재생·현행 API와 실기 검증은 별도입니다.

## 교육자료

| 주제 | 매뉴얼 |
|---|---|
| Chili3D 로컬 CAD·제품 단면 검토 | [설치·단위·입출력·저장 검증](docs/CHILI3D_LOCAL_CAD.md) |
| PBR·광택·재질·조명·렌더 적용 | [Blender 제작 절차](docs/BLENDER_SKILLS_WORKFLOW.md) · [PBR·룩디벨롭·렌더 색인](docs/BLENDER_SKILLS_INDEX.md) |
| 얼굴 기본 루프·눈–코 연결 | [기본 루프 배치](docs/FACE_RETOPOLOGY_BASIC_LOOPS.md) |
| 상세 얼굴 토폴로지 | [2번 강좌 보강](docs/FACE_RETOPOLOGY_SECOND_TUTORIAL.md) |
| 눈꺼풀 두께·안쪽 면 | [눈꺼풀 볼륨](docs/FACE_EYELID_VOLUME.md) |
| 눈꺼풀 셰이프키·리깅·컨트롤 | [셰이프키 교육](docs/FACE_EYELID_SHAPE_KEYS.md) |
| 구강벽·잇몸·치아·혀 | [구강 구조](docs/FACE_ORAL_STRUCTURE.md) |
| 캐릭터 채색 전체 흐름 | [Painter 교육 시작점](docs/PAINTER_CHARACTER_WORKFLOW.md) |
| 만화형 캐릭터 채색 | [Stylized 채색](docs/PAINTER_STYLIZED_CHARACTER.md) |
| 피부 색·거칠기·투과광 | [피부 레이어](docs/PAINTER_SKIN_LAYERS.md) |
| Painter 텍스처 → Blender | [내보내기와 연결](docs/PAINTER_TO_BLENDER.md) |
| 모듈러 맵 전체 흐름 | [제작과 검수 시작점](docs/MODULAR_MAP_WORKFLOW.md) |
| 단위·원점·스냅·직선/코너 | [그리드와 키트](docs/MODULAR_MAP_GRID_KIT.md) |
| 지형·LOD·절벽·해안 | [지형 연결과 시험](docs/MODULAR_MAP_TERRAIN.md) |
| 벽·문·지붕·중첩 Prefab | [건물 조립](docs/MODULAR_MAP_BUILDINGS.md) |
| FBX·UV·재질·콜라이더·모바일 | [Blender→Unity 인계](docs/MODULAR_MAP_BLENDER_UNITY.md) |
| 배우·카메라·이동·복원 상태 | [플레이 검수 계획](docs/MODULAR_MAP_PLAYABILITY_QA.md) |
| 지정된 모듈러 맵5강 | [강좌 시간 색인](docs/MODULAR_MAP_COURSE_INDEX.md) |
| UV 전체 흐름·검수 | [UV 교육 시작점](docs/UV_WORKFLOW.md) |
| 시임·전개·체커·핀·Relax | [형태별 펼치기](docs/UV_SEAMS_UNWRAP.md) |
| 얼굴·눈꺼풀·눈·손과 몸 | [캐릭터 UV](docs/UV_CHARACTER.md) |
| 밀도 계산·정규화·패킹·간격 | [텍셀 밀도와 배치](docs/UV_TEXEL_DENSITY_PACKING.md) |
| 재질·Texture Set·UDIM·아틀라스·출력 | [텍스처 구성과 인계](docs/UV_TEXTURE_SETS_HANDOFF.md) |
| 지정된 UV 5강 시간 색인 | [강좌별 확인과 설명 대조](docs/UV_COURSE_INDEX.md) |
| 사진 심리스 텍스처 5강 | [제작 순서와 강좌별 핵심](docs/SEAMLESS_TEXTURE_WORKFLOW.md) |
| 가죽 높이·범프·실제 변위 | [높이 맵과 Blender](docs/SEAMLESS_TEXTURE_HEIGHT_MAPS.md) |
| 이음선·반복 띠·출력 검수 | [심리스 검수](docs/SEAMLESS_TEXTURE_QA.md) |
| 손·손가락 전체 흐름·검수 | [손 교육 시작점](docs/HAND_FINGER_WORKFLOW.md) |
| 손 기본형 모델링 | [손 제작](docs/HAND_BUILDING.md) |
| 손바닥·관절 면 흐름 | [손 리토폴로지](docs/HAND_RETOPOLOGY.md) |
| 손가락 컨트롤·가중치 | [손가락 리깅](docs/HAND_FINGER_RIGGING.md) |
| 전신 전체 흐름·검수 | [전신 교육 시작점](docs/BODY_CHARACTER_WORKFLOW.md) |
| 몸통·팔다리·목 면 흐름 | [전신 리토폴로지](docs/BODY_RETOPOLOGY.md) |
| 어깨·골반·팔꿈치·무릎 볼륨 | [관절 볼륨 보강](docs/BODY_JOINT_VOLUME.md) |
| 게임용 몸·손발 연결 | [게임 베이스 메시](docs/BODY_GAME_BASE_MESH.md) |
| 매치3 전체 흐름·출처 | [매치3 교육 시작점](docs/MATCH3_WORKFLOW.md) |
| 매치3 데이터·좌표·입력 | [보드와 입력](docs/MATCH3_BOARD_INPUT.md) |
| 제거·낙하·특수·장애물 | [해결 루프](docs/MATCH3_RESOLUTION_SPECIALS.md) |
| 목표·레벨·저장·시험 | [레벨과 검증](docs/MATCH3_LEVEL_SAVE_QA.md) |
| 네 자료의 구현·누락 비교 | [자료별 비교](docs/MATCH3_SOURCE_COMPARISON.md) |
| Taft Unity/C# 실제65편 | [회차별 학습 색인](docs/MATCH3_TAFT_EPISODES.md) |
| Unity6.3 적용 전 확인 | [호환 대조 목록·공식재확인 미완료](docs/MATCH3_UNITY6_COMPATIBILITY.md) |

자체 도식은 docs/assets/, 강좌별 실제 확인 범위와 오류 교정·미확인 사항은 [reports/VideoLearning](reports/VideoLearning)에 있습니다.

## 지갑·가죽·사진 기반 3D 교육

전용 도막 공정은 [가죽 엣지코트·건조·접힘부 검수](docs/LEATHER_EDGE_PAINT_PROCESS.md)를 확인합니다. 제조사·제작자 웹본문5개와 영상3편의 화면70시점·영어 자동 자막을 대조했습니다. 중앙 굽힘·안팎 길이·보강판 경계는 [겹 구조 매뉴얼 §8](docs/WALLET_LAYERED_SHELL_VOLUME.md#8-중앙-굽힘보강판-끝안팎-길이를-따로-검토한다)에 보강했습니다.

실제 공예의 재단·입구 선마감·피할·접착 후 본재단·두 바늘 봉제는 [소가죽 카드지갑 제작 매뉴얼](docs/COWHIDE_CARDHOLDER_CRAFT_WORKFLOW.md)을 확인합니다. [강좌4편·화면127시점·한국어 자동 자막 대조](reports/VideoLearning/20261105_COWHIDE_CARDHOLDER_STUDY.json)에서 키트 조립, 직접 재단, 보강재 패턴을 구분했습니다. 실물 제작·수납·MD 실기 검증은 미실행입니다.

패턴 기반으로 겹 가죽 지갑을 다시 구성할 때는 [Marvelous Designer 재단·봉제 절차](docs/MARVELOUS_WALLET_PATTERN_WORKFLOW.md)를 먼저 읽습니다. 공식 문서 10개에 이어 [영상 3편의 화면 109시점·공식 2편 영어 자동 자막 대조](reports/VideoLearning/20261105_MARVELOUS_WALLET_VIDEO_STUDY.json)를 보강했습니다. 열린 입구·봉제 방향·층·메시 밀도·겉실 단위와 CLO/MD9.5/2025.1의 차이를 다루며 실제 MD9 제작·시뮬레이션 검증과 구분합니다.

봉제실 섬유결·엣지코트·실과 바늘구멍 정렬은 [Sampler 봉제실·엣지 마감](docs/SAMPLER_THREAD_EDGE_FINISH.md)을 함께 확인합니다. 형상 라운딩과 표면 맵, 문서 학습과 실제 제작을 구별합니다.

설치된 Sampler에서 사진 표본을 분리하고 맵을 생성·출력할 때는 [Sampler 사진 PBR 절차](docs/SAMPLER_PHOTO_PBR.md)와 [공식 문서 4개 학습 범위](reports/VideoLearning/20261104_SAMPLER_DOCUMENT_STUDY.json)를 확인합니다. 문서 학습과 앱 실기 검증은 구분합니다.

상품 접사·영상에서 작은 가죽 타일의 반복을 줄이고 부품마다 고유 맵을 구성할 때는 [상품 가죽 고유 텍스처 세트](docs/PRODUCT_LEATHER_UNIQUE_TEXTURE_SETS.md)를 확인합니다. 레이어 해상도·AI Upscale·목적 UV와 접선 노멀 베이크, 원본 관측과 재구성 세부를 구별합니다.

사진에서 가죽 PBR 맵을 만드는 작업은 [Materialize 제작 순서·출력 검수](docs/PHOTO_LEATHER_MATERIALIZE_WORKFLOW.md)와 [실제 3강좌 재검토 범위](reports/VideoLearning/20261104_PHOTO_LEATHER_MATERIALIZE_STUDY.json)를 먼저 확인합니다. 사진의 명암과 실측 높이, 미리보기와 실제 변위를 구분합니다.

추가 검수: [매끈한 코팅 가죽·면광원 반사·미세 요철과 디노이즈](docs/LEATHER_LOOKDEV_AND_DENOISE.md) — 공식 자료3개의 해당 절을 Codex가 직접 읽고 대조한 절차 보강이며 [실제 학습 범위](reports/ExternalLearning/20261103_LEATHER_LOOKDEV_STUDY.json)와 실기 검증을 구분합니다.

모델링·표면 맵 10강과 사진→3D 5강을 분석한 한국어 적용 매뉴얼입니다. 예시 치수는 제품의 실측값으로 바꾸며, 교육 완료와 실제 제품 제작·스캔 검증은 구분합니다.

| 주제 | 정본 문서 |
|---|---|
| 외피·척추·포켓·봉제·접힘 검수 | [지갑 모델링](docs/WALLET_MODELING.md) |
| 추가 내피·봉제 구속·외피 여유분의 펼침 볼륨·가죽 두께와 내부 보강재 | [겹 구조와 외피 볼륨](docs/WALLET_LAYERED_SHELL_VOLUME.md) · [Salpa/Texon/Velodon 사양 학습](reports/ExternalLearning/20261105_WALLET_LEATHER_REINFORCEMENT_STUDY.json) |
| 넓은 곡면·포켓 기준 높이·상대 키 합산·native 드라이버 검증 | [곡면과 포켓 높이 조정](docs/WALLET_BROAD_CURVATURE_AND_POCKET_HEIGHT.md) · [공식 5.2 문서 열람 기록](reports/ExternalLearning/20261104_WALLET_CURVATURE_DRIVER_STUDY.json) |
| 사진 높이·범프·노멀·실제 변위 | [가죽 표면 맵](docs/WALLET_SURFACE_MAPS.md) |
| 모델링5강·표면맵5강 근거·오류 교정 | [10강 분석](docs/WALLET_COURSE_ANALYSIS.md) |
| 촬영·정렬·표면 복원·앞뒤 결합 | [사진→3D 촬영과 복원](docs/PHOTO3D_CAPTURE_RECONSTRUCTION.md) |
| 실측 스케일·Blender 정리·fSpy | [지갑에 적용](docs/PHOTO3D_WALLET_APPLICATION.md) |
| 사진→3D 5강 시간 색인·해석 교정 | [5강 분석](docs/PHOTO3D_COURSE_ANALYSIS.md) |

- 모델링·표면 맵: [PDF](docs/downloads/wallet-modeling-and-surface-manual.pdf) · [편집용 Word](docs/downloads/wallet-modeling-and-surface-manual.docx) · [HTML 원본](docs/downloads/wallet-modeling-and-surface-manual.html)
- 사진→3D: [PDF](docs/downloads/wallet-photo-to-3d-manual.pdf) · [편집용 Word](docs/downloads/wallet-photo-to-3d-manual.docx) · [HTML 원본](docs/downloads/wallet-photo-to-3d-manual.html)
- [모델링·표면 맵 분석 범위](reports/VideoLearning/20261101_WALLET_COURSES_VERIFICATION.json) · [사진→3D 분석 범위](reports/VideoLearning/20261101_PHOTO3D_COURSES_VERIFICATION.json)

원영상·전문 자막·강좌 캡처·제품사진·모델·개인 PC 경로는 포함하지 않습니다. PDF는 자체 작성한 문장과 표로 구성했습니다.

## 포함 범위

기존 개발/교육 작업 폴더의73개 교육 경로를 대조해 공개 내용 누락0을 확인하고 중복 사본을 정리했습니다. [정본 전환 기록](reports/EducationMigration/20261101_PUBLIC_CANONICAL_MIGRATION.md)을 참고하세요.

- 2026-11-01 기준 자체 학습 매뉴얼 66개, 자체 SVG 도식 16개, 학습 보고서와 검증 기록을 포함합니다.
- 손·손가락 세 강좌의 전체 흐름 표본·공개 자동 자막 분석을 추가했습니다. 고유393개 시점과 핵심 UI 확대24장을 확인했으며, 실제 모델 제작·리깅 검증은 수행하지 않았습니다. 전신 세 강좌도 전체 흐름과 주요 제작 구간을 분석해 추가했습니다. 전신은 고유497개 시점·원본 크기 UI30장을 대조했으며, 실제 캐릭터 변경·변형·엔진 검증은 미실행입니다.
- 매치3는 Taft Unity/C# 실제65편·Winterbolt1편·git-amend 공개3편(영상69편), Catlike 전체 글/FAQ와 제작자 C#7개를 분석했습니다. 고유2,094시점·472시트·135단독프레임(추출 폭1280)과 전편 정제 자동자막을 대조했습니다. Unity/Android 실행은 하지 않았고 Unity6.3 공식 웹 재대조는 미완료로 표시했습니다.
- 사진 심리스 텍스처 5편은 고유168시점·30시트·원본 UI10장과 정제 자동자막2,299행을 대조했습니다. 로컬 Qwen 10회·FrameLens 핵심300초를 실제 분석했고 AI 오독은 원본으로 교정했습니다. 새 텍스처·Blender/게임 적용은 수행하지 않았습니다.
- UV5강은 Ryan King Art·CG Boost/Jim Morren·Dikko·Josh/BlenderBros·Huge Menace/Tristan의 지정 원본을 학습했습니다. 고유364시점·66시트·단독33장(추출 폭1280)과 정제 자동자막4,163행 전체를 대조했습니다. 시임·얼굴/눈·밀도·패킹·재질 인계를 문서화했으며 실제 메시/UV·Painter·엔진 변경은 하지 않았습니다. 현행 Blender5.2 메뉴/API 재대조는 미완료입니다.
- 모듈러 맵 지정5강4:43:11을 고유446시점·80시트·단독37장(1280폭)과 정제 자동자막4개4,892행으로 대조했습니다. LMHPOLY는 자막이 없어 화면 지시문을 표본 확인했습니다. 접합·지형·건물·FBX/Prefab·모바일/이동 검수 계획을 기록했으며 실제 지도/모델/엔진 변경과 기기 검증은 하지 않았습니다.
- 강좌 원본 영상·음성·대량 캡처·외부 에셋·캐릭터 모델·텍스처·AI 요청 데이터는 포함하지 않습니다. 원 강좌의 링크와 제작자 정보는 각 문서에 있습니다.
- 공개본은 로컬 PC의 증거 파일 경로를 생략했습니다. 검증 JSON의 원본 스냅샷 해시는 교육 당시 자료를 가리키며, 이 공개본 파일 해시는 PUBLIC_MANIFEST.json에서 확인합니다.
- 문서와 도식의 검토·학습 범위는 실제 모델 제작 성공이나 독립 검수 통과를 보장하지 않습니다. 앱 버전이 다른 조작은 적용 전 확인하세요.

프로젝트별 승인 자료 준비는 [참고자료 안내](docs/PROJECT_REFERENCE_GUIDE.md)를 읽으세요.
