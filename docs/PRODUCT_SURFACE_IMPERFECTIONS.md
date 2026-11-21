# 제품 렌더의 미세 흔적(먼지·보풀·마감칠 점) — 실물에 있는 것만 넣기

2026-11-21 Claude 작성. 지갑 하이퍼리얼 작업에서 "사용 흔적"을 넣기 전에 매뉴얼이 없어, 서로 다른 교육자료 3개를 읽고 정리했다. 문서 학습과 실제 적용 검증은 구분한다. 적용 결과는 프로젝트 기록에 따로 남긴다.

## 1. 읽은 자료(실제 열람 범위)

| # | 자료 | 제작자·주소 | 확인 날짜 | 읽은 범위 |
|---|---|---|---|---|
| 1 | Blender 5.2 LTS Manual — Distribute Points on Faces, Principled Hair BSDF | Blender Foundation, [점 뿌리기](https://docs.blender.org/manual/en/5.2/modeling/geometry_nodes/point/distribute_points_on_faces.html), [Principled Hair](https://docs.blender.org/manual/en/5.2/render/shader_nodes/shader/hair_principled.html) | 2026-11-21 | 두 쪽 본문 전체(입력·출력·속성, 색 지정 방식·Random Color/Roughness) |
| 2 | Substance 3D Sampler — Dust | Adobe, [Dust](https://experienceleague.adobe.com/en/docs/substance-3d-sampler/using/filters/wear-and-finish/dust) (2026-04-07 갱신 표시) | 2026-11-21 | 본문 전체(용도·사용법·매개변수 4개) |
| 3 | Adding Surface Imperfections in 3D | David Ariew, School of Motion, [글](https://www.schoolofmotion.com/blog/adding-surface-imperfections) | 2026-11-21 | 본문 전체와 대본 앞부분(약 02:24까지). 영상은 보지 않음. Cinema 4D/Octane 예제 |

## 2. 세 자료가 공통으로 말하는 것

- CG의 기본 상태는 너무 완벽하다. 실제 표면은 먼지·기름·긁힘·눌림이 있다(자료 3).
- 흔적은 주로 **거칠기 변화**로 드러난다. 흑백 거칠기 맵으로 반사를 불균일하게 하면 사실감이 크게 오른다. 여러 맵은 더하기/곱하기로 겹치고, 범프는 대개 너무 세므로 1보다 작은 값을 곱해 줄인다(자료 3).
- 먼지는 **양·깊이·퍼짐 경계·경사면 억제**로 조절한다. 패인 곳을 부드럽게 메우는 쪽으로 쌓인다(자료 2: Dust quantity, Dust Depth, Spread Contrast, Prevent Spread on Slope).
- 같은 무늬가 반복되면 CG 티가 난다. 크기·회전을 바꾼 사본을 노이즈로 섞는다(자료 3).
- 닳음은 모서리(곡률 높은 곳)에 먼저 생긴다. 곡률 맵/Dirt 노드로 가린다(자료 3). **단, 실물에 닳음이 없으면 넣지 않는다**(아래 원칙 1).
- 보풀 같은 가는 섬유는 표면에 점을 뿌리고(밀도는 m²당 개수, 선택 영역으로 제한, 안정된 id로 변형 중에도 같은 점 유지) 그 위에 곡선을 세워 만든다. 섬유 재질은 Principled Hair BSDF(Cycles 전용)의 Direct Coloring으로 실 색을 맞추고, Random Color/Random Roughness를 조금 줘서 가닥마다 다르게 한다(자료 1).

## 3. 적용 원칙(프로젝트 작업용 제안)

1. **실물 사진에서 먼저 찾는다.** 분석 프로그램(Qwen 등)으로 먼저 읽고 1:1 확대로 직접 대조한다. 실물에 없는 흔적(손자국, 긁힘, 마감칠 닳음)은 "사실감"을 이유로 추가하지 않는다. 사용자에게 범위를 확인한다.
2. **크기를 실측으로 맞춘다.** 먼지 알갱이·섬유 굵기·점 크기를 mm로 정하고 장면 단위로 바꾼다(예: 1 Blender 단위 = 100 mm). 확대 사진의 땀 간격 같은 알려진 치수를 자로 쓴다.
3. **아주 약하게, 겹쳐서.** 흔적 하나가 최종 화면에서 눈에 띄면 너무 세다. 접사에서만 보일 정도로 시작한다. 거칠기·색·범프를 따로 조절할 수 있게 레이어/노드를 나눈다.
4. **위치는 물리적으로.** 먼지는 오목한 곳·바닥 쪽·경사 완만한 곳, 실 보풀은 실이 끊기거나 만나는 곳, 마감칠 점은 칠 표면 위에 불규칙하게.
5. **반복을 숨긴다.** 노이즈 하나로 점을 만들면 격자처럼 보일 수 있다. 크기가 다른 두 층을 섞거나 점 뿌리기(Poisson Disk)로 간격을 흩는다.
6. **같은 조건 전후 비교.** 같은 카메라·빛·노출로 흔적 없음/있음을 렌더하고, 최종 구도와 접사를 모두 본다. 수치나 노드 연결만으로 완료하지 않는다.

## 4. Blender 5.2에서의 구성 예(제안, 대상에 맞춰 조정)

| 흔적 | 방법 | 조절값 |
|---|---|---|
| 실 끝 보풀 | 실 메시에서 선택 영역(실 끝·교차 부근)에 Distribute Points on Faces → 짧은 곡선(점마다 무작위 방향·길이) → Curve to Mesh 대신 곡선 그대로 Cycles 렌더, Principled Hair(Direct Coloring, 실 색) | 밀도, 길이 0.2~1 mm, 반지름 수 µm, 휘어짐 |
| 칠 표면 작은 점 | 칠 재질에 작은 Voronoi/노이즈 문턱값 마스크 → 색을 약간 어둡게, 거칠기 약간 변화 | 점 크기·개수·어두움 정도 |
| 옅은 먼지 | 오목한 곳(AO/Pointiness) × 작은 점 마스크 → 밝은 회색 점, 거칠기 올림. 경사·윗면 조건 | 양·깊이·경계 선명도(자료 2의 개념) |

## 5. 한계

- 자료 3의 예제는 Cinema 4D/Octane이다. 노드 이름·세기 수치를 Blender에 그대로 옮기지 않는다.
- 자료 2는 Sampler 필터 설명이다. 이번 Blender 적용에서는 개념(양·깊이·경계·경사 억제)만 참고했다.
- 이 문서는 문서 학습 정리다. 실제 렌더 검증 결과는 각 프로젝트 기록에 남긴다.

[공용 교육 목록](../README.md) · [공통 작업 규칙](COMMON_WORK_RULES.md)
