# Painter 세 강좌 표본 시각 학습·매뉴얼 검토

2026-10-31 · 전담 자체 확인. **DOCUMENTED_SAMPLED_VISUAL_STUDY**. 세 자료의 실제 화면을 읽고 매뉴얼로 정리했으며 전체 음성/전 프레임 연속 학습, 앱 재현 또는 루미 제작 완료 판정은 아니다.

## 결과와 범위

| 강좌 | 직접 읽은 고유 원본 시점 | 원본 크기 UI | 문서 |
|---|---:|---:|---|
| Khatri3D / L6vsR64BbXA / 약 33:12 | 105 | 5 | [스타일 캐릭터](../../docs/PAINTER_STYLIZED_CHARACTER.md) |
| Adobe 공식 10개 / 약 74분 | 184 | 8 | [피부 레이어](../../docs/PAINTER_SKIN_LAYERS.md) |
| Art of Pilgrim / Ze88TvD2ku0 / 약 3:30 | 47 | 7 | [출력·Blender 연결](../../docs/PAINTER_TO_BLENDER.md) |

총 **336개 고유 시점**, 접촉표 **77장**, 원본 크기 UI **20장**을 직접 확인했다. 확대 UI는 같은 시점이면 고유 프레임에 중복 가산하지 않았다. 기존 누적 528개에 이번 336개를 더하면 864개다. 프레임 수는 학습 품질 보증이나 연속 시청 분량이 아니다. 원본별 정확한 시점·길이·파일 크기·SHA-256·샘플 집합은 [검증 JSON](20261031_PAINTER_COURSES_VERIFICATION.json)에 남겼다.

[연결 매뉴얼](../../docs/PAINTER_CHARACTER_WORKFLOW.md), 강좌별 매뉴얼 3개, 자체 SVG 1개와 본 검토/JSON을 추가했다. 기존 기본 얼굴 매뉴얼의 참고 목록에는 연결 링크 한 줄만 추가했다. 이미지·강좌의 텍스트를 통째로 옮기지 않고 관찰한 절차와 프로젝트 적용 조건을 새로 작성했다. 기존 얼굴 본문/입/눈꺼풀 매뉴얼과 루미 파일은 보존했다.

## 출처와 접근

Khatri3D와 Pilgrim은 지정된 공개 YouTube 원본을 사용했다. Adobe Learn 페이지는 10개 수업 제목과 74분 표시를 읽었다. 그 페이지의 DOM에서 임베드 주소를 찾지 못해 Adobe Substance 3D 공식 채널의 동일 제목·순서·강사 설명을 가진 10개 재생목록을 찾아 실제 영상을 읽었다. 페이지 제목만 읽고 공식 수업을 학습 완료 처리하지 않았다.

- [Khatri3D 원본](https://www.youtube.com/watch?v=L6vsR64BbXA)
- [Adobe Learn 원문](https://www.adobe.com/learn/substance-3d-painter/web/texturing-characters-in-substance-3d-painter) · [공식 영상 10개](https://www.youtube.com/playlist?list=PLB0wXHrWAmCyxQQSMWfYuTRT1pntzCjY7)
- [Art of Pilgrim 원본](https://www.youtube.com/watch?v=Ze88TvD2ku0)

기존 yt-dlp/FFmpeg를 사용했다. Adobe 2–10번 영상의 첫 HTTPS137 형식은 403이었고 한 번의 일반 공개 HLS270+234 형식 대체로 모두 내려받았다. 로그인·유료 접근·DRM 우회는 하지 않았다. 첫 `.info.json`에 이전 형식 선택이 남을 수 있어 실제 ffprobe와 해시를 검증 기록의 기준으로 삼았다. 음성 스트림 존재를 확인한 사실과 음성 내용을 모두 검토한 사실을 구분한다.

브라우저는 ego-browser space29 하나만 사용했다. 사용자 제어 전환 시 멈추고, 사용자의 명시적인 재개 답변 뒤 같은 공간에서 이어갔다. 마지막에 finish를 한 번 실행해 종료했다. 다른 전담의 space28은 접근하지 않았다. 업데이트 알림만 확인했고 설치하지 않았다.

## 주요 교정 사항

| 근거 | 확인한 내용 | 매뉴얼에 반영한 교정 |
|---|---|---|
| Khatri 09:00 | 눈/머리 세트를 숨긴 피부 작업 | 눈구멍 화면을 메시 삭제로 해석하지 않음 |
| Khatri 20:00 | Eyes R 레이어, Roughness 0.2082 | 예제 순간값, 루미 안구 처방으로 고정하지 않음 |
| Khatri 30:00 | Position 생성기와 Global Invert | 챕터 AO 표기만으로 AO 베이크라고 단정하지 않음 |
| Khatri 32:00/33:00 | Blender 프리셋 출력, 뒤에 Body_Alpha.1001 생성 불가 경고 | 파일 목록과 전체 출력 성공을 구분 |
| Adobe 수업2 01:00/04:00 | Painter 2019.1.2/OpenGL/기존 노멀, 별도 베이크 창 | 기존 노멀 입력과 모든 베이크 완료를 구분 |
| Adobe 수업8 06:45 | SSS 표시 옵션과 Scattering 값 | Painter 값과 Blender Subsurface 입력을 1:1 복사하지 않음 |
| Adobe 수업9 02:00/07:00 | 다른 레이어/시점의 거칠기 값·단독 채널 보기 | 흑백 모델을 무텍스처/조각 작업으로 오인하지 않음 |
| Pilgrim 00:50/02:45 | Metallic RGB + Glossiness Alpha, 후반 Invert | 파일 개명이 데이터 의미를 바꾸지 않으며 Roughness=1−Glossiness |
| Pilgrim 03:20 | AO용 추가 이미지 sRGB, Multiply Fac0.5 | 정답 설정으로 복사하지 않고 데이터 맵·강도·중복 AO 검사 추가 |

Blender 5.2의 Normal Map에는 Convention 설정이 있으며 기본 OpenGL/DirectX를 구분한다. 이 부분은 [5.2 공식 Normal Map 설명](https://docs.blender.org/manual/en/5.2/render/shader_nodes/displacement/normal_map.html)을 실제 읽고 대조했다. [Image Texture](https://docs.blender.org/manual/en/5.2/render/shader_nodes/textures/image.html), [Principled](https://docs.blender.org/manual/en/5.2/render/shader_nodes/shader/principled.html), [Adobe Output templates](https://experienceleague.adobe.com/en/docs/substance-3d-painter/using/export/export-window/output-templates)도 실제 확인했다. 로컬 5.2 앱의 현행 메뉴/노드 실행 검증은 아니다.

## 로컬 AI 보조 결과와 실패

기존 Qwen3-VL 4B 로컬 모델을 재사용했으며 새 모델·유료 API를 쓰지 않았다. 4개 이미지씩 11회 입력(총44개 입력 발생) 중 **6회만 요청한 4항목 배열 형태**였다. Adobe 4회는 단일 객체만 반환했고 Pilgrim 출력 구간 1회는 반복 문자열과 length 종료로 불완전했다. 응답 생성 성공을 클립 이해 성공으로 처리하지 않았다.

반환된 내용에도 Texture Set을 레이어로 부르는 오류, Fill을 Filter로 읽는 오류, Material 표시 모드를 선택된 세트로 오해하는 오류가 있었다. Blender의 노드를 Painter의 fill-layer/texture-set node라고 부른 설명, Adobe 흑백 보기를 무텍스처/토폴로지라고 설명한 내용, 브러시 화면을 조각 작업으로 추정한 내용은 거부했다. AI 입력 시점을 모두 직접 읽고 세밀한 값은 원본 크기 UI로 확인했다. 단독 품질 판정·자동 제작 근거로 쓰지 않았다.

FrameLens는 강좌별 클립 1개씩 총3회 실행했다. 각각 shot1을 반환했지만 semantic 필드는 모두 null이었다. 이미지/샷 지표만 얻었으며 작업 의미를 분석한 것으로 집계하지 않았다. 도구 출력의 해시와 상태는 JSON에 기록하고 원문/이미지 페이로드는 공개하지 않았다.

## 보존과 미실행

원본 영상은 로컬 `[local evidence location omitted]`, 샘플/보조 결과는 `[local evidence location omitted]`에 보존했다. 모두 Git 제외 대상이다. 공개 저장소에는 강좌 원본·캡처·프로젝트·소재·개인 브라우저 DOM·계정 데이터·AI 이미지 페이로드를 넣지 않는다.

Claude–Painter 연결/상태/재시작 테스트 중단 지시를 유지했다. Blender live 조회·점유·메시/UV/텍스처 수정·노드 변경·파일 임포트·렌더·리깅·움직임 작업을 하지 않았다. 실제 `.spp` 제작/출력, Node Wrangler 설치/활성화, Unity/Android 재질 품질·성능은 미검증이다. 루미 v021은 기존 **PARTIAL** 그대로다.

이번 결과는 자체 문서 검토이며 독립 검수 PASS가 아니다. 이후 실제 제작은 승인 원본 확인과 Blender Guide 인계부터 진행해야 한다.
