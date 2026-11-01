# 파란 가죽 높이맵과 범프 및 디스플레이스먼트 매뉴얼

예시 파란 내피는 **엠보싱의 능선과 골이 조명에 반응하되, 얇은 가죽과 카드 슬롯의 형태를 유지하는 것**이 목표다. 사진의 진한 부분을 모두 깊은 골로 바꾸거나, 강한 범프로 접합 띠를 가리는 방식은 피한다. 먼저 높이 데이터와 반복 품질을 정리하고, 범프로 결의 방향·크기를 확인한 뒤 필요한 만큼만 실제 변위를 더한다.

아래는 강좌 D1~D5의 원리를 가죽 제작에 맞춘 적용 절차다. 학습 완료는 높이맵이나 제품 품질의 실제 검증 완료를 뜻하지 않는다.

## 1. 표현할 크기에 따라 방법을 고른다

| 대상 | 기본 방법 | 판단 기준 |
|---|---|---|
| 접힌 등, 가죽 두께, 슬롯 입구 | 메시 모델링 | 외곽과 실제 공간을 형성함 |
| 표면 위로 나온 실밥 | 커브 경로를 따르는 실 메시 | 근접·옆면에서도 실루엣이 필요함 |
| 작은 결과 엠보싱 음영 | Height → Bump 또는 RGB Normal → Normal Map | 표면 방향을 바꿔 빛에 반응시킴 |
| 옆면·접사에서 필요한 능선 높이 | 세분화 + 실제 Displacement | 형상을 바꾸는 비용과 슬롯 변형을 감수할 이유가 있음 |

D1은 [01:00](https://www.youtube.com/watch?v=KH_o4KcsVyA&t=60) 부근에서 범프·노멀의 외곽이 평평한 것을 보여 주며, [03:16](https://www.youtube.com/watch?v=KH_o4KcsVyA&t=196) 부근에서는 변위 강도에 따른 형상 변화를 비교한다. 범프의 명암이 진해졌다는 사실과 실제 정점이 움직였다는 사실을 구분한다.

## 2. 사진에서 쓸 표본과 실제 결 크기를 정한다

1. 원본 사진에서 가죽만 있는 부분을 고른다. 실밥, 슬롯 경계, 그림자, 반사점, 원근이 큰 부분을 제외한다.
2. 픽셀 수와 별도로 표본이 실제 몇 mm를 덮는지 정한다. 정확한 근거가 없으면 추정값으로 기록한다.
3. UV의 방향과 가로·세로 비율을 맞춘다. 정사각형이 아닌 이미지도 사용할 수 있으며, 이미지 자체를 정사각형으로 늘여 결을 찌그러뜨릴 필요는 없다.
4. Base Color, Height, Normal, Roughness가 같은 표본과 방향을 사용하는지 확인한다. 타일 크기와 회전이 어긋나면 색 능선과 빛의 반응이 분리된다.

표본의 물리 크기는 사진과 실측 근거로 확인하며, 정확한 근거가 없는 값은 추정으로 기록한다.

## 3. 높이 데이터는 가죽의 상대 높이로 정리한다

D2의 [02:20~03:30](https://www.youtube.com/watch?v=DOn4G9HVo2M&t=140)는 흑백 변환과 Levels를, D4의 [03:00~05:03](https://www.youtube.com/watch?v=GItohAbyzCM&t=180)는 주파수별 조절과 Height 확정을 보여 준다. 이를 현재 사진에 옮기는 절차는 다음과 같다.

1. 원본을 보존하고 편집용 사본을 만든다. 이후 필터 계산은 가능하면 16비트 문서에서 한다. 8비트를 16비트로 바꿔도 이미 잃은 높이 정보는 복원되지 않는다.
2. 흑백 변환 후 넓은 조명 얼룩과 실제 작은 결을 분리한다. 넓은 밝기 차이가 높이에 섞이면 타일마다 가죽이 부풀거나 꺼진다.
3. High Pass 또는 주파수 조절은 조명 성분을 줄이는 보조 도구로 사용한다. 능선 양쪽의 이중 테두리나 고리 모양이 생기면 필터 반경·대비를 재검토한다.
4. Levels와 대비를 조절해 능선·골을 읽기 쉽게 하되, 넓은 영역을 완전한 흑백으로 잘라 평평한 단과 절벽을 만들지 않는다.
5. 반사점, 색 얼룩, 업스케일이 만든 선을 높이로 오인하지 않는다. 단일 사진에서 얻은 결과는 사진 기반 추정 높이다.
6. 진짜 능선과 골이 반대로 읽히면 높이 반전 또는 Bump Invert를 시험한다. 색상의 밝기만으로 최종 방향을 결정하지 않는다.
7. 중립값과 값 범위를 기록하고 무손실로 저장한다. PNG/TIFF라는 확장자만으로 16비트를 보장하지 않으므로 실제 저장 파일의 비트 깊이를 확인한다.

## 4. Materialize를 이용하는 선택 경로

D4의 원리는 Diffuse 사진 → Height 생성 → Height 확정 → Normal 생성 → 전체 재질 미리보기 → 저장이다. D5는 여기에 Metallic·Smoothness·AO와 Blender 연결을 더한다. [D4 Height와 Normal](https://www.youtube.com/watch?v=GItohAbyzCM&t=180), [D5 Blender 연결](https://www.youtube.com/watch?v=kvJuC8Wj_lQ&t=570)

| 순서 | 작업 | 현재 가죽에서 확인할 것 |
|---|---|---|
| 1 | Diffuse의 Open으로 사진 불러오기 | 원본 사진과 보정용 높이 소스를 구분 |
| 2 | Height의 Create에서 주파수·대비 조절 | 넓은 얼룩을 낮추고 결의 연결 유지 |
| 3 | Set as Height Map으로 확정 | 확정 전 미리보기와 실제 채택된 맵 구분 |
| 4 | Normal의 Create와 주파수·대비 조절 후 확정 | 높이를 바꾸면 파생 노멀도 갱신할지 결정 |
| 5 | 필요할 때만 Smoothness·AO 추가 | 가죽에 금속 마스크를 자동 생성할 이유는 없음 |
| 6 | Show Full Material로 여러 형태 확인 | Parallax 미리보기를 Blender 실제 변위 검증으로 취급하지 않음 |
| 7 | 프로젝트와 맵 저장 후 다시 열기 | 파일명, 채널 용도, 비트 깊이, 뒤집힘 확인 |

세부 결용 Normal과 큰 높이용 Height를 다르게 조정할 수 있지만 두 버전의 관계를 기록해야 한다. 같은 요철을 강한 노멀과 강한 높이로 중복 강조하지 않는다. 이 강좌들은 특정 사진의 반복 띠가 자동으로 해결된다는 근거를 제공하지 않는다.

## 5. 심리스 검수는 높이 변환 뒤 다시 한다

1. 단일 타일을 100%로 보고 흐린 복구 띠, 능선 끊김, 점 노이즈를 찾는다.
2. 가로·세로 Offset으로 원래 경계를 내부로 옮겨 본다. 기존 보정 지점과 다른 Offset도 검사한다.
3. 3×3 이상 반복을 축소해 밝기 체스판, 십자 띠, 결 밀도 차이, 독특한 흠집의 반복을 본다.
4. 최종 크기와 조명에서 검사한다. 경계 픽셀 평균 차이가 낮더라도 반복 띠가 보이면 보류한다.
5. 높이에서 자연스럽게 이어져도 노멀 변환 뒤 기울기 차이로 선이 생기는지 확인한다.

가장자리 단차가 줄어도 결 밀도와 복구 띠가 반복되면 부분 개선으로 기록한다. 새 높이맵에서 다른 Offset과 축소 반복을 다시 검사한다. [심리스 검수](https://github.com/gnogus-ux/PuzzleIsland-Education/blob/main/docs/SEAMLESS_TEXTURE_QA.md)를 함께 적용한다.

## 6. Blender 연결은 데이터 용도별로 만든다

| 이미지 | 색 해석 | 연결 |
|---|---|---|
| Base Color | 일반 색 이미지의 sRGB 등 원본에 맞는 색 해석 | Principled BSDF의 Base Color |
| 흑백 Height | Non-Color | Bump의 Height → Bump의 Normal → BSDF의 Normal |
| RGB Normal | Non-Color | Normal Map의 Color → Normal 출력 → BSDF의 Normal |
| Roughness | Non-Color | BSDF의 Roughness |
| Smoothness | Non-Color | 1 - Smoothness → Roughness |
| 실제 변위용 Height | Non-Color 또는 해당 텍스처 경로의 동등한 데이터 해석 | 선택한 실제 변위 경로의 Height/이미지 |

Height 이미지를 BSDF의 Normal에 바로 연결하지 않는다. D2는 [05:30~06:30](https://www.youtube.com/watch?v=DOn4G9HVo2M&t=330)에서 잘못된 직접 연결과 Bump 노드 경유 연결을 비교한다. [Bump 노드](https://docs.blender.org/manual/en/5.2/render/shader_nodes/displacement/bump.html), [Image Texture](https://docs.blender.org/manual/en/5.2/render/shader_nodes/textures/image.html)

Normal과 추가 범프를 함께 쓴다면 Normal Map 출력 → Bump의 Normal 입력, 별도 미세 Height → Bump의 Height로 연결할 수 있다. 두 입력이 같은 요철의 중복 표현인지 먼저 확인한다. 노멀의 UV와 접선 기준도 이미지에 사용한 UV와 맞춘다. [Normal Map 노드](https://docs.blender.org/manual/en/5.2/render/shader_nodes/displacement/normal_map.html)

Blender의 기본 노멀 규약은 OpenGL이다. DirectX 노멀이면 지원되는 Convention 옵션 또는 녹색 채널 반전으로 맞춘다. 이미 바꾼 맵을 노드에서 또 반전하지 않는다. [Blender 노멀 규약](https://docs.blender.org/manual/en/5.2/render/shader_nodes/displacement/normal_map.html)

## 7. 범프부터 약하게 확인한다

1. 중립 색과 고정 Roughness로 시작한다. 강도 0 대조군을 같은 카메라와 조명에서 만든다.
2. 먼저 결의 방향과 크기를 맞춘 뒤 강도를 올린다. 결이 너무 커 보이면 Strength보다 UV/표본 크기를 먼저 확인한다.
3. Strength는 효과를 섞는 정도, Distance는 높이 변화의 배율이다. 영상의 Distance 1을 mm 단위 가죽에 그대로 사용하지 않는다.
4. 빛을 좌우로 바꾸며 능선과 골의 음영이 반응하는지 본다. 사진의 하이라이트가 색에 고정돼 있으면 높이를 더 세게 하기 전에 사진 명암을 정리한다.
5. 근접과 최종 2K 구도를 모두 본다. 멀리서 모아레·반짝임이 생기면 반복 크기, 필터링, 대비를 다시 조정한다.

범프는 외곽 실루엣을 바꾸지 않는다. 외곽에 실제 능선 높이가 필요한 경우에만 다음 단계로 넘어간다.

## 8. 실제 디스플레이스먼트 두 경로

### A. Displace modifier 경로

실제 메시를 변형하므로 Solid 모드에서도 형상 변화가 보인다. 텍스처, UV, Direction, Midlevel, Strength와 정점 그룹을 명시한다. 높이를 표현할 정점이 먼저 있어야 하므로 필요한 세분화는 Displace 앞에 둔다. D3의 [07:00~08:18](https://www.youtube.com/watch?v=4yfNK1PG4Pk&t=420)에서 순서와 UV에 따른 차이를 확인할 수 있다.

가죽처럼 얇은 파트는 앞면 마스크와 가장자리 완충 구간을 이용해 뒷면·슬롯·접합부가 함께 부푸는 것을 제한한다. 기존 접힘 modifier와의 상대 순서는 현재 리그와 마스크가 정의된 좌표를 확인해 결정한다. 강좌 큐브의 순서만 보고 기존 리그를 일괄 재배치하지 않는다.

```text
로컬 변위 = (높이값 - Midlevel) × Strength
```

예를 들어 입력이 0~1, Midlevel이 0.5, Strength가 0.16mm이면 가중치·변환 전 범위는 -0.08~+0.08mm다. 실제 맵이 그 범위를 전부 사용하지 않을 수 있고, 월드 변위는 오브젝트/부모의 변환에 따라 달라진다. [Displace modifier](https://docs.blender.org/manual/en/5.2/modeling/modifiers/deform/displace.html)

### B. 재질 Displacement 경로

Height → Displacement 노드 → Material Output의 Displacement를 연결한다. 노드 연결 외에 재질의 Displacement 방식, 지원되는 렌더 엔진과 충분한 세분화를 함께 확인한다. Bump Only이면 외곽이 바뀌는 실제 변위를 얻었다고 기록하지 않는다. [재질 변위 방식](https://docs.blender.org/manual/en/5.2/render/materials/components/displacement.html), [Displacement 노드](https://docs.blender.org/manual/en/5.2/render/shader_nodes/displacement/displacement.html)

D3의 화면은 Blender 3.3.1을 사용하며 예전 Experimental·Adaptive Subdivision 설정을 보여 준다. 현재 버전의 메뉴 위치와 지원 조건을 확인한다. 목표 장면의 EEVEE 렌더에 Cycles용 설정만 옮겨 적용 완료로 표시하지 않는다. 엔진에 독립적으로 메시를 바꾸는 modifier 경로와 구분한다.

두 경로를 같은 요철에 동시에 강하게 적용하지 않는다. 상세 시험 중에는 Apply로 영구화하지 말고 비교 가능한 modifier와 원본을 남긴다.

## 9. 시험 후보의 기록과 비교

대상 모델·이미지의 비트 깊이·물리 표본 크기·UV·세분화·적용 범위·Strength·Midlevel을 기록한다. 설정값과 실제 월드 변위는 다를 수 있으므로 구분한다.

동일 모델·카메라·조명에서 기본 재질, 범프만, 변위만, 범프+변위를 비교한다. 실제 변위는 켜짐/꺼짐의 평가 정점 차이로 확인한다. 슬롯 단면·실밥·접힘을 검수한 뒤 후보 채택을 판단한다. 시험 중인 맵과 승인본은 구분한다.

## 10. 색과 반사를 망치지 않는 연결 규칙

D5의 [10:58](https://www.youtube.com/watch?v=kvJuC8Wj_lQ&t=658) 화면에는 Smoothness → Invert → Roughness 연결이 보인다. Roughness는 밝을수록 거칠고 Smoothness는 밝을수록 매끈하므로, 둘은 같은 이름의 맵이 아니다. 완전 반전 뒤 필요한 범위를 다시 조절한다.

가죽은 기본적으로 비금속으로 두고 Metallic을 올려 광택을 만들지 않는다. 금속 부품이 있다면 별도 재질 또는 확인된 마스크로 다룬다. AO를 Base Color에 곱하는 방법은 선택 사항이다. 사진에 이미 그림자가 있거나 렌더에서 접촉 음영이 계산되면 골이 지나치게 검어질 수 있으므로 AO 없는 상태와 비교한다.

Materialize의 평면 Parallax와 Blender의 실제 메시 변위, 사진의 색 변화와 가죽의 높이 변화, 미리보기와 저장된 데이터의 품질을 각각 구분한다.
