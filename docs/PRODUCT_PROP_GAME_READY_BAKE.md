# 초실사 소품 → 게임용 판(저면 메시·굽기·FBX) — 뼈·모양 키가 있는 제품 (2026-11-22, Claude)

블렌더에서 영상용으로 만든 초실사 제품(수백만 삼각형, 절차적 재질, 드라이버로 움직이는 뼈·모양 키)을 **원본은 그대로 두고** 유니티 URP용 가벼운 판으로 옮길 때 쓰는 매뉴얼이다. 가죽 반지갑(약 239만 → 30,826 삼각형, 4K + 2K 텍스처)을 실제로 옮기며 확인한 절차와 문제를 정리했다.

관련 정본: [Blender 스킬 절차 — UV·텍스처·베이크](BLENDER_SKILLS_WORKFLOW.md#uv텍스처베이크), [상품 가죽 고유 텍스처 세트](PRODUCT_LEATHER_UNIQUE_TEXTURE_SETS.md), [UV·텍스처 세트 인계](UV_TEXTURE_SETS_HANDOFF.md), [Unity 가져오기 규칙 에디터](UNITY_IMPORT_RULES_EDITOR.md)(URP Lit 채널), [가죽 지갑 교훈](PRODUCT_WALLET_MODELING_ANIMATION_LESSONS.md), [공통 작업 규칙](COMMON_WORK_RULES.md)(가이드 선행·단일 점유).

## 학습한 자료와 범위

| 자료 | 주소 | 확인 날짜·버전 | 실제로 읽은 범위 |
|---|---|---|---|
| Blender Manual — Render Baking | https://docs.blender.org/manual/en/5.2/render/cycles/baking.html | 2026-11-22, 5.2 LTS | 전체(설정·Bake Type·Influence·Selected to Active·Cage·Margin) |
| Blender Manual — FBX (Legacy) Export | https://docs.blender.org/manual/en/5.2/files/import_export/fbx_legacy.html | 2026-11-22, 5.2 LTS | Export 절 전체(Include·Transform·Geometry·Armatures·Bake Animation). 새 FBX 페이지(files/import_export/fbx.html)는 가져오기만 있고 내보내기는 FBX 애드온(Legacy)이라고 적혀 있음 |
| Blender Manual — Data Transfer Modifier | https://docs.blender.org/manual/en/5.2/modeling/modifiers/modify/data_transfer.html | 2026-11-22, 5.2 LTS | 앞 7,000자(사용법·옵션·One-to-One·Interpolated Mapping 앞부분). Topology Mapping 뒤쪽은 미열람 |

URP Lit 채널(BaseColor, Metallic 알파 = Smoothness, Normal, Occlusion)은 기존 [Unity 가져오기 규칙 에디터](UNITY_IMPORT_RULES_EDITOR.md) 5절(Unity 공식 문서 학습)을 그대로 쓴다.

### 자료에서 확인한 사실
- 굽기는 메시에 UV가 있어야 하고, **재질의 활성 이미지 노드**가 굽는 대상이다. 활성 이미지 노드가 없는 재질은 아무것도 굽지 않는다.
- Selected to Active: 광선은 저면 메시에서 **안쪽으로** 쏜다. 시작점은 케이지가 없으면 Extrusion, 거리는 Max Ray Distance로 조절한다. 케이지는 같은 토폴로지 사본이 필요하다.
- 노멀은 Tangent가 기본이고 움직이는 물체에도 쓸 수 있다. 축 배치(Swizzle)는 R·G·B 각각 고를 수 있다(블렌더 기본 +X +Y +Z = OpenGL식).
- Diffuse 등에서 Color만 켜면 조명과 무관한 표면 색(albedo)이 나온다.
- Margin은 UV 조각 둘레를 늘려 밉맵·필터에서 이음이 보이지 않게 한다(Extend / Adjacent Faces).
- 높은 해상도 물체는 물체마다 CPU 메모리를 고정으로 쓰므로, 메모리가 모자라면 합쳐서 굽는다.
- FBX 내보내기: Scale(기본 10은 다른 앱에 맞춘 값), Apply Scaling, Forward/Up(유니티는 -Z Forward, Y Up이 흔함), Apply Modifiers, Triangulate, Tangent Space, Only Deform Bones, Add Leaf Bones, Bake Animation/All Actions 항목이 있다.
- Data Transfer의 Interpolated 방식(Nearest Face Interpolated)은 가장 가까운 원본 면 위 점에서 그 면의 꼭짓점 값을 보간한다.

### 자료에 없어서 실제 작업으로 정한 것(적용 제안·실기 근거)
- 모양 키가 있는 메시는 Decimate 모디파이어를 적용할 수 없다 → **새 저면 메시를 만들고, 원본 면 위의 가장 가까운 점(무게중심 좌표)에서 모양 키 변화량과 뼈 가중치를 보간**해 옮겼다(Data Transfer의 Nearest Face Interpolated와 같은 원리를 스크립트로, 모양 키까지).
- 드라이버는 FBX로 넘어가지 않는다 → 규칙을 JSON 표로 뽑아 엔진 코드로 옮긴다.

## 절차

### 0. 가이드 먼저(공통 규칙 3절)
원본 복사본에 Guide 컬렉션을 만들어 **보존 경계**(윤곽·입구선·판 끝 단차·바깥 턱·접힘 띠·뼈 위치·모양 키 등고선), **형태 세부 지도**(주변 3 mm 평균보다 높낮이 0.02/0.06/0.12 mm 단계), **목표 면 흐름**, **목표 삼각형 수**를 그리고 확인받은 뒤 시작한다. 검수 창의 지적(뼈 수 표기, 주머니 솔기 띠 2/5/9 mm, 접힘 띠 마감칠 고리 1 mm, 계단 위·아래 추가 줄)은 가이드 v002로 반영했다.

### 1. 보이는 면만 새로 만든다
- 판마다 **보이는 윗면(또는 겉면)만** 만든다. 판의 평면 모양(경계)은 원본 면 집합의 경계 고리에서 얻고, 점은 경계(1 mm) + 보존 띠(윤곽 안쪽 0.8/2.0/2.3/2.7/3.2/5/9 mm, 입구 ±0.6/1.2/2.5/5/9 mm) + 접힘 띠 가로줄(1 mm 간격, 계단 위·아래 추가) + 안쪽 격자(6~8 mm)로 넣고 `mathutils.geometry.delaunay_2d_cdt`로 삼각형을 만든다.
- 높이는 원본 면에 수직으로 쏴서 얻는다(모양 키 Basis 좌표, 모디파이어·드라이버 적용 전).
- **가려진 면은 지운다**: 위층에 덮인 삼각형은 지우되, **입구(열린 가장자리)에서 3 mm 안은 남긴다**(들리면 보이기 때문). 단, 바깥 윤곽(마감칠 밑) 쪽은 열린 가장자리가 아니므로 남기지 않는다 — 남기면 UV에 액자 모양 조각이 생겨 판을 크게 낭비했다(사용률 38%).
- 입구·판 끝에는 **벽 띠**(윗면 가장자리 → 아래층까지 3줄)를 붙인다. 벽 위치는 원본 경계에서 0.18/0.30 mm 바깥. 둥근 입구 모양은 노멀로 굽는다.
- 마감칠(둘레를 감싸는 띠)은 원본 고리(16점, 0.2 mm 간격)에서 **10점(좌우 대칭, 꼭대기 유지)**만 고르고, 고리는 곧은 곳 3 mm·모서리 10°마다·접힘 띠 가로줄 자리·단면 높이가 0.06 mm 넘게 바뀌는 자리(층 시작·끝)에 둔다. 가중치·모양 키는 같은 원본 꼭짓점 값을 그대로 쓴다.
- **숨은 곳 편법**: 원본 마감칠이 가죽을 0.006 mm만 덮어서, 저면 메시의 직선 구간이 가죽을 드러냈다 → 윤곽 0.85 mm 안의 가죽을 0.04 mm 안쪽으로 넣었다(보이지 않는 곳).
- 카드처럼 휘면서 미끄러지는 물체는 평평한 상태에서 3 mm 가로·13.5 mm 세로로 잘라 토폴로지를 만들고, 지오메트리 노드로 움직이던 상태를 몇 단계(1, 0.75, 0.5, 0.25, 0)로 찍어 **모양 키(단계별)**로 넣는다. 값은 삼각(hat) 함수로 이웃 두 단계를 섞는다.

### 2. 뼈 가중치·모양 키 옮기기
- 저면 꼭짓점마다 원본 면 위 가장 가까운 점의 삼각형과 무게중심 좌표를 구하고, 그 세 꼭짓점의 **가중치·모양 키 변화량**을 같은 비율로 섞는다. 모양 키는 **Basis 좌표 + 변화량**으로 넣는다(키마다 Basis를 따로 옮기면 어긋난다).
- 같은 이름이라도 **드라이버 식이 다른 키는 이름을 나눈다**(예: GAPE와 GAPE__P11).
- 블렌더 5.2: `shape_key_add(from_mix=False)`로 만든 키의 값이 1로 들어가는 경우가 있었다 → 만든 뒤 **값을 0으로** 직접 둔다. `new_from_object`로 만든 메시는 원본 정점 그룹을 이미 갖고 있으니 다시 만들면 `.001` 이름이 생긴다 → 먼저 비운다.
- `delaunay_2d_cdt`는 입력 점을 합치거나 옮길 수 있으니, 경계점 대응은 좌표 비교가 아니라 **반환되는 원래 점 번호(orig_verts)**로 찾는다(좌표 비교로 찾았다가 입구 벽이 점선처럼 끊겼다).

### 3. UV 아틀라스
- 판은 위에서 본 평면(XY)을 그대로 UV로(실제 크기), 벽은 Smart UV Project, 마감칠은 **경로 길이 × 단면 길이로 직접 펴고 50 mm마다 자른다**(자동 펼침은 액자 모양 조각을 만들었다).
- Average Islands Scale → Pack Islands(회전 허용, CONCAVE, 여백 0.25%)로 한 장에 넣는다. 결과: 4K 한 장, 사용률 68%, 가죽 17.65 px/mm, 겹침 0.
- 카드는 원래 그림 UV를 2K 한 장의 칸(앞·뒤 1024×645, 옆면 띠)에 옮겼다.

### 4. 굽기(Cycles, GPU)
- Selected to Active, 케이지 없음, Extrusion 0.6 mm, Max Ray 1.2 mm(1 칸 = 100 mm 장면이라 0.006/0.012), Margin 16 px Extend.
- 굽는 순서: Normal(Tangent, +X +Y +Z = OpenGL) → Diffuse **Color만**(BaseColor) → Roughness → AO(64 표본). 바느질 실·보풀도 선택 물체에 넣어 노멀·AO·색에 함께 굽는다.
- **원본 물체를 한 덩어리로 합쳐서 굽는다(속도).** 원본 물체 19개(239만 삼각형)를 따로 선택해 4K로 구웠더니 40분 동안 한 장도 끝나지 않았다(GPU 사용률 2%, 원본↔저면 대응 계산이 CPU에서 물체마다 반복). 원본을 평가된 사본 하나로 합치고(모디파이어·지오메트리 노드 보풀·`rest_position` 유지, `new_from_object(preserve_all_data_layers=True)`), 저면 쪽도 같은 아틀라스를 쓰는 물체를 사본 하나로 합치니 4K 4종 + 카드 2K 4종이 **9분**에 끝났다(RTX 3060 OptiX). 1K 시험 한 장으로 먼저 시간을 잰다.
- 움직이는 카드는 지갑 AO에서 빼고(숨김), 카드 AO는 그 카드 자신만으로 굽는다.
- **미끄러지는 카드는 다 뺀(평평한) 상태에서 굽는다.** 꽂힌 상태는 칸 속 숨은 부분이 접히고 눌려 있어 그림이 줄무늬로 번졌다.
- 채널 정리: MetallicSmoothness = R 금속(가죽 0, 카드 0.35) + A 매끄러움(1 − 거칠기). AO는 따로 낸다.

### 5. 내보내기
- 가죽+마감칠은 같은 재질이라 내보낼 때 한 메시로 합친다(임시 사본). 드라이버는 사본에서 지우고 키 값 0으로.
- FBX: 선택만, ARMATURE+MESH, global_scale 0.1(1칸 = 100 mm 장면 → 미터), FBX_SCALE_ALL, -Z Forward / Y Up, Apply Modifiers 끔(모양 키 보존), Tangent Space 켬, Add Leaf Bones 끔, Bake Animation 끔(움직임은 엔진 코드). 유니티에서 실제 크기(지갑 폭 0.16 m)·축을 확인한다.

## 검수
- 같은 카메라·조명·색관리(원본 룩데브)에서 원본/게임용을 나란히 렌더(Cycles·EEVEE), Workbench solid·wire.
- **단면 겹침**: 모양 키 100%(드라이버 잠시 끔)에서 주머니마다 가로·세로 단면 2개, 0.1 mm 간격. 면 위 평균 차이 0.004~0.014 mm. 입구 벽은 0.1~0.3 mm 옆으로 밀려 계단 근처에서 최대 약 1 mm 차이가 날 수 있다(그림에서 확인).
- **뚫림 검사**: ① 펼친 상태 둘레 훑기(윤곽 안 0.15~0.6 mm에서 위·아래로 쏴 마감칠이 아닌 것이 먼저 맞는 곳), ② 자세별 고리 단면 검사 — 쉬는 자세에서 마감칠 U 안에 있던 가죽 점이 닫힘·반열림·들림·카드 뺌 자세에서도 U 안에 있는지. 최종 0곳.

- FBX를 다시 불러와 크기(0.161 × 0.111 m)·뼈 70·모양 키·UV를 확인한다. **유니티는 UV0만 쓰므로** 옛 UV(카드 그림용)가 첫 번째로 남아 있으면 지운다.
- 이미지 판독(로고·각인 확인 등)은 공통 규칙상 분석 프로그램(Qwen3-VL)을 먼저 쓴다. 모델 저장 드라이브가 연결되지 않아 쓸 수 없을 때는 그 사실을 기록하고 작업자가 원본을 직접 본다. `ollama list` 같은 확인 명령만으로도 서버가 켜질 수 있으니 주의한다.

## 남은 제한
- 유니티 실제 가져오기·URP 화면·모바일 성능은 이 문서 작성 시점에 미검증.
- 마감칠의 투명 코팅(clear coat) 광택은 Roughness 굽기에 들어가지 않는다 → 매끄러움이 실물보다 낮을 수 있다.
- 카드 미끄러짐은 5단계 모양 키라 단계 사이 직선 보간이다. 다른 카드 값과의 상호작용(위 카드 입술 따라가기)은 찍지 않았다.
