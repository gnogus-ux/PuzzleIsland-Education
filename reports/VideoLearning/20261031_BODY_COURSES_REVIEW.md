# 전신 세 강좌 · 전체 흐름과 주요 구간 학습 기록

2026-10-31 · 전담 자체 검토. **DOCUMENTED_WHOLE_FLOW_SAMPLED_VISUAL_AND_AUTO_CAPTION_STUDY**. 시작부터 끝까지 개요와 모든 주요 제작 단계의 상세 표본, 공개 자동 자막 정리문의 첫 줄부터 마지막 유효 줄까지 대조했다. 모든 프레임·클릭·음성의 연속 검토, 앱 재현, 독립 품질 검수나 실제 캐릭터 제작 완료는 아니다.

## 결과와 출처

| 강좌 | 로컬 길이 | 직접 읽은 고유 시점 | 원본 크기 확대 |
|---|---:|---:|---:|
| [Dikko ULTIMATE Part7](https://www.youtube.com/watch?v=3WnW_ZFXudk) | 91:14.940 | 245 | 12 |
| [Dikko Modeling for Animation03](https://www.youtube.com/watch?v=GxMz4HylQfU) | 21:11.618 | 102 | 8 |
| [Ironbark Game Character1](https://www.youtube.com/watch?v=TJZ2TutkYnA) | 55:43.534 | 150 | 10 |

로컬 총 길이168분10.092초의 흐름을 확인했다. 직접 읽은 접촉표96장, 원본 크기 UI30장, 중복 제외497개 시점이다. 같은 시점의 확대는 한 번만 집계했다. 연속 시청 분량은 아니다.

기존 누적1257개에 이번497개를 더해1754개 시점이다. 표본 수는 학습 품질 점수가 아니다.

산출물은 [연결 매뉴얼](../../docs/BODY_CHARACTER_WORKFLOW.md), [리토폴로지](../../docs/BODY_RETOPOLOGY.md), [관절 볼륨](../../docs/BODY_JOINT_VOLUME.md), [게임 베이스](../../docs/BODY_GAME_BASE_MESH.md), 자체 SVG1개, 본 보고서와 [검증 JSON](20261031_BODY_COURSES_VERIFICATION.json)이다. 기존 손 연결 매뉴얼에는 전신 링크 한 줄만 추가한다. 기존 얼굴·손·Painter 본문과 도식은 보존한다.

ego-browser space34 하나에서 실제 제작자 페이지·제목·챕터 설명을 읽었다. 기존 yt-dlp/FFmpeg로 공개 영상과 en-orig 자동 자막을 확보했다. 새 설치·로그인/유료 접근·모델 다운로드·유료 API 호출·유료 강좌 에셋 다운로드는 하지 않았다. 원본은 모두1920×1080 AV1/AAC이며 파일별 길이·크기·SHA-256·스트림을 JSON에 남겼다.

개요는 Part7과 Ironbark90초, Volume60초 간격 및 마지막 시점을 포함했다. 주요 구간은 대체로15–45초 간격, 반복 손 구성 등은 최대60초 간격으로 보강했다. 추가 AI 입력 시점40개를 모두 직접 읽었다. 어깨·골반·팔꿈치·무릎·목·손발 접합·최종 시연은 원본 크기로 확인했다. JSON의 cohorts/native_reviewed_times에 전체 표본 집합을 기록한다.

공개 자동 자막은 timed-word 새 텍스트를 중복 정리해 읽었다. 사람 검증 자막이 아니며 시작 몇 초의 말이 빠지거나 부위·단축키가 오인식될 수 있다. 음성 스트림 존재 확인과 모든 음성을 들었다는 주장을 구분했다.

## 부위 범위와 해석 교정

| 근거 | 확인한 내용 | 문서 반영 |
|---|---|---|
| Part7 05:45/09:15 | 골반·사타구니 띠와 Mirror 경계 | 앞뒤 높이/루프 수를 보편 처방으로 고정하지 않음 |
| Part7 15:35/17:05/25:15 | 어깨 링·쇄골/겨드랑이·팔 밀도 전환 | 어깨끝 한 점 집중과 단순 관 연결을 구분 |
| Part7 30:15 | 팔꿈치 간격·LoopTools와 모디파이어 | 원형화 도구와 실제 twist 리그 성공을 구분 |
| Part7 36:15/40:15 | 열린 엉덩이 패치·허벅지 전진 | 임시 구멍·노란 원본 발을 완성 새 메시로 오인하지 않음 |
| Part7 62:00/68:00/72:00 | 뒤통수/턱 아래–목–쇄골 연결 | 얼굴 경계 보호와 밀도 전환, 별도 머리 재설계 제외 |
| Part7 75분 이후 | 국소 정리·완화·다리 비틀린 격자 교정 | 모든 나선 금지/모든 추가 루프 유익이라는 단정 제외 |
| Volume 01:10/02:25 | 어깨 Ctrl+B 후 간격·Smooth | 선 수보다 부피·분포와 연결 평가 |
| Volume 06:25/09:05 | 엉덩이 띠와 완화 | 성인 예제 체형을 승인 캐릭터로 옮기지 않음 |
| Volume 10:57.5/13:00 | Merge At Last 메뉴·무릎 패치 | 팔꿈치를 손가락, Edit Mode를 Object Mode로 부른 AI 오류 거부 |
| Volume 18:40 | 두 모델의 굽힘·도약 자세 | 강좌 속 시연으로 기록, 동일 가중치 통제 실험·루미 PASS로 확장하지 않음 |
| Ironbark 01:30 | 전체 캐릭터 목표20,000tris 기획 | 최종 몸 측정값이나 모바일 예산으로 취급하지 않음 |
| Ironbark 12:45/14:45 | 깊이·세로 흐름 보강 | 한 시점 실루엣과 입체 기본형 구분 |
| Ironbark 34:10/44:50 | 손목·발목 연결 전 열린 경계 | Join/Bridge/용접 구분, 내부 면·순서·틈 검사 |
| Ironbark 48:10 | 키 표시 V로 Rip | 자막 B 오류 교정, 이동 취소 후에도 분리 유지 |
| Ironbark 50:45/54:20 | 무릎 흐름·팔 추가 선과 마감 | 실제 리깅 시연과 구분, 지느러미는 고유 디자인 |

어깨·겨드랑이·쇄골, 가슴·등·허리, 골반·사타구니·엉덩이, 팔꿈치·무릎, 목–몸통과 손목·발목 연결을 다뤘다. 전완 twist joint는 Part7의 설명만 있으며 뼈·분배·가중치는 미실행이다. 사람 발가락 구조, 발목 변형, 슬개골 전용 구조, 모바일 예산·LOD·UV·노멀 베이크·엔진 성능은 세 수업으로 입증하지 못했다.

첫 강좌는 손/발 미제작이다. 두 번째의 비교 리그는 자동 리깅 한계가 있고 실제 가중치 파일을 확인하지 못했다. 세 번째의 머리·UV·Painter·리그·엔진은 시리즈 다른 편의 소개다. 해당 편까지 읽었다고 확장하지 않는다.

## 현행 문서와 버전

Blender5.2의 [Shrinkwrap](https://docs.blender.org/manual/en/5.2/modeling/modifiers/deform/shrinkwrap.html), [Mirror](https://docs.blender.org/manual/en/5.2/modeling/modifiers/generate/mirror.html), [Rip Vertices](https://docs.blender.org/manual/en/5.2/modeling/meshes/editing/vertex/rip_vertices.html), [Armature](https://docs.blender.org/manual/en/5.2/modeling/modifiers/deform/armature.html), [Subdivision Surface](https://docs.blender.org/manual/en/5.2/modeling/modifiers/generate/subdivision_surface.html)를 실제 읽었다. 투영 방식과 축/원점, Merge 조건, Rip 취소, Preserve Volume의 역할·한계, Smooth Shading과 실제 세분화 차이를 보강했다. 로컬5.2 앱의 실행 검증은 아니다.

Ironbark 원본 하단은3.3.1로 읽었다. Dikko 두 자료는 읽은 확대에서 정확한 패치 버전을 확정하지 않았다. UI 외형으로 버전을 추정하지 않았다. ego space34는 finish를 한 번 실행해 종료했다. 업데이트 알림은 있었지만 설치하지 않았다.

## 로컬 AI 보조와 오류

기존 Qwen3-VL4B 로컬 모델로60초 클립당4개 이미지, 총10회/40개 입력을 사용했다. 모두 stop 종료 및 요청한4항목/문자열 uncertain 형식을 충족했다. **형식 성공과 내용 정확도를 구분**한다. 팔꿈치를 손가락/손잡이, 마지막 팔 장면을 다리로 부른 오류, 시점 회전을 팔 굽힘/형체 연장으로 추정한 오류, 낮은 시점을 높은 시점으로 부른 오류, 원본 조각/리토폴로지 색상·선택 범위 혼동을 직접 화면으로 교정했다. 자동 판단을 제작·검수 근거로 단독 채택하지 않았다.

FrameLens는60초 클립3개에서 각각 shot1을 반환했지만 semantic 필드는 모두 null이었다. 샷/영상 수치만 얻었고 관절 제작 의미를 이해한 결과로 집계하지 않았다. 원본 응답·입력 이미지·클립은 로컬에만 보존하며 해시·상태·교정 요약을 JSON에 남겼다.

## 보존·검증·미실행

원본·표본·보조 결과는 로컬의 Git 제외 폴더에 보존한다. PC의 절대 경로는 공개본에서 생략했다. 공개본에는 원본 영상·음성·캡처·자막 원문·강좌 자산·AI 이미지 페이로드·개인 브라우저 데이터·PC 절대 경로·비공개 Git 참조를 넣지 않는다.

문서 연결·UTF-8/LF·JSON·SVG 안전성·실제 도식 렌더·기존 문서 보존을 검사하고 관련 교육 파일만 게시한다. 공유 작업 폴더는 모든 대상의 기존 기준본/동일본/신규 여부를 먼저 검사한 뒤 좁게 동기화한다. 공개본 해시는 공개 manifest에서 검증하며 교육 당시 스냅샷 해시와 구분한다.

Claude/Painter 상태·연결·테스트·재시작 중단을 유지했다. Blender live 조회·점유·임포트·메시/UV/재질 수정·리깅·움직임·렌더·출력·엔진 테스트를 하지 않았다. 실제 Blender Guide 파일도 제작하지 않았으며 SVG는 Guide 대체물이 아니다. 기존 제작 상태를 변경하지 않았다. 실제 제작과 독립 검수는 후속 범위다.
