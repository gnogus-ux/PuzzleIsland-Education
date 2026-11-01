# 외부 DCC 자료와 기존 제작 매뉴얼 대조

2026-11-01 · 문서 대조만 수행. 원문의 프로그램 사용 명령은 실행하지 않았다.

## 고정 출처와 읽은 범위

- EL4CTEO/blender-skills: `fb92cfb4cc5a238c22113a6a230b09f535bd0656` — SKILL28+root README 전체.
- scenario-labs/skills: `7f4b801c7248d51b093ec365aceb114bd06139e6` — Blender15+Maya11+ZBrush9+핵심1+숨김지원7=SKILL43, root README 전체.
- 두 저장소 MIT 표기를 확인했다. 원문을 번역 복제하지 않고 자체 요약·판단과 고정 링크를 제공한다.
- 추가 전체 참조14개는 감사 JSON의 파일·줄·SHA로 명시한다. 모든 references/scripts/assets/tests를 읽거나 실행한 것은 아니다. 직접 읽지 않은 참조와 영상의 내용은 확인된 근거로 승격하지 않는다.
- Godot14는 후속 별도 묶음이다. Unreal10·Unity14·Roblox14·Scenario 서비스79는 이 첫 묶음의 본문 검토 대상이 아니며 별도 담당의 기록을 따른다.

## 충돌·과도한 일반화 교정

| 원문 주장/충돌 | 이번 판단과 재사용 조건 |
|---|---|
| EL Unity skeletal에서 root90° 때 Bake Axis Conversion 켬 / Scenario는 끔 | 서로 다른 경로·importer·root 변환 조건. 실제 프리셋 A/B와 재임포트로 판단, 단일 정답 지정 금지 |
| 모든 key가 움직여야 한다 / Scenario neutral sil | 요청한 활성 키와 의도된 중립·미사용을 구분. 이름 52개만으로 표정 완성 아님 |
| 엔진0–1 clamp·relative만 export | 엔진/format/version별 계약이며 보편 규칙으로 승격하지 않음 |
| 눈·입3링/관절3루프·고정18/24점 | 기능·곡률·접속 경계에 따른 시작점. 승인 얼굴·원본 정점 수를 숫자에 맞춰 변경하지 않음 |
| 낮은 평균 이격/고른 quad/pole 비율이면 고품질 | 동일 solid/wire의 실제 윤곽·주름·면 중앙·시각 개선 별도 필요 |
| inside40–60% /55% 초과는 수축 | 원문 내부 겹치는 경고 범위. 표본용 도구 heuristic이며 현재 모델 합격선 아님 |
| auto remesh→Decimate가 UV·형태 보존 | 원본 사본과 실제 비교 필요. 얼굴 변형 흐름을 보장하지 않음 |
| mirror+1U로 bake 해결 | 0–1 wrap·baker·UDIM 여부·비대칭 텍스처 계약에 제한 |
| normal 또는 displacement만 | 같은 요철 중복은 피하되 서로 다른 주파수 병용은 renderer에서 검증 |
| AO를 albedo에 절대 넣지 않음 / source 조명 복원용 곱함 | 최종 game shader의 AO와 사진 입력 보정·정지 양식을 구분 |
| 모든 roughness에 noise·피부 SSS·성인 비례 | 승인 스타일·기기·사용 거리 우선. 이 교육으로 루미 외형 재설계 안 함 |
| material 하나=draw call 하나 /join이 항상 최적 | submesh·pass·shadow·culling·엔진 batching·기기 측정 필요 |
| 큰 메시 QA 일부 skipped | 검사 생략을 PASS로 바꾸지 않음 |
| 저자 fake/offline pass·written score | 실제 앱 실행·사용자 파일 품질·local 버전 검증과 분리 |
| ZBrush4M점=2K·Divide후paint항상파괴 | 대략 밀도 안내와 실제 보간/데이터 상태 구분 |
| 출력1mm벽/0.12mm맞춤/104%축소보정 | 특정 장비·재료 예제. 시험 출력 없이 보증하지 않음 |

## 기존 공용 매뉴얼에 붙일 연결

다음 네 본문은 이번 대조에서 전체 읽었다. 기존 영상 표본 수·학습 방식은 기존 문서의 보고이며 이번 외부 SKILL 학습에서 영상을 다시 본 수가 아니다.

| 기존 문서 | 외부에서 보강할 절차 | 유지할 우선 기준 |
|---|---|---|
| [얼굴 기본 루프](FACE_RETOPOLOGY_BASIC_LOOPS.md) | 여섯 층 계획, 루프 수를 범위로 조정, cage/평가표면 양쪽 진단 | 실제 Guide·눈 opening과 두께/벽 구분·코/볼 전환·원본 용접 별도 판정 |
| [UV 통합](UV_WORKFLOW.md) | silent unwrap 실패, adaptive 투영의 문제 픽셀 위치·케이지 실패 사례 | 원본 UV/이미지 보존·시임→왜곡→밀도→패킹·mip/실제 디테일 검수 |
| [전신 제작](BODY_CHARACTER_WORKFLOW.md) | pivot/loop 문제와 weight/corrective 문제 분리, 단일 ROM 뒤 복합 검수 계획 | 별도 머리/승인 어린이 체형 보존·지정 부위 밖 재설계 금지·움직임 보류 |
| [모듈러 맵](MODULAR_MAP_WORKFLOW.md) | instance/LOD/culling·피벗·실제 export 왕복의 기준 | 최소 키트 접합 시험·플레이 폭/시야·현 프로젝트 경로 탐색 유지 |

진행 중 모델의 미완료 접속·곡률 문제를 외부 스킬 학습 완료로 해소 처리하지 않는다. Blender 5.2.2/RetopoFlow3.4.11의 기존 실행 기록도 해당 기존 작업의 근거이며 이번 앱 실행이 아니다. 프로젝트 맵 승인 상태와 임시 지도 범위도 바꾸지 않는다.

## 다음 실제 작업 전에 보완할 근거

특수 안구의 구조·동공 회전·깊이 표현·눈꺼풀 접촉은 이 묶음에서 실증되지 않았다. 실제 그 작업이 재개될 때 해당 제작법/버전의 근거와 현재 승인 Guide가 필요하다. 외부 scalar threshold나 ARKit key 이름을 그 근거로 대신하지 않는다.

Maya/ZBrush 설치·라이선스·Windows bridge·held key·GUI stroke·엔진 import는 미검증이다. Blender 코드도 원문의 5.2.1 보고와 로컬 실제 API를 구분해야 한다. 애니메이션·리깅·새 맵·Painter 연결은 보류 범위를 유지한다. 문서가 부족한 구체적 제작을 만났을 때 목적·부족한 근거를 먼저 명확히 하고 기존 승인 학습 범위 안에서 보완한다.
