# Sampler 봉제실·엣지코트와 제품 모서리 마감

2026-11-05. Sampler 6.0.2 및 Blender 5.2.2 적용을 위한 문서 학습 기준이다. 아래 공식 문서의 본문을 실제 확인했으며, 문서 열람과 해당 제품에서의 실행 성공은 구별한다. 기존 [사진 PBR](SAMPLER_PHOTO_PBR.md), [지갑 모델링](WALLET_MODELING.md), [표면 맵](WALLET_SURFACE_MAPS.md)을 함께 적용한다.

## 형상과 재질의 역할

사진에서 얇아지는 입구 벽, 둥근 단면, 바늘구멍과 실의 진입 위치는 실제 형상으로 다룬다. 표면 맵으로 두꺼운 벽이나 잘못된 봉제 경로를 숨기지 않는다. 수정 전 원본·하단 보존 경계·입구·봉제 경로를 실제 Guide에 표시한다. 하단 유지 요청은 하단 정점과 기존 UV·리그를 보존한 별도 후보에서 확인한다.

둥근 엣지는 평면 외곽 반경과 두께 방향의 라운딩을 구별한다. 전체 폭이나 하단 두께를 줄이지 않고 단면의 날카로운 어깨를 완화할 수 있다. 기존 코팅 메시가 가죽·박스를 덮는 경우 코팅만 둥글게 해도 내부 박스가 드러날 수 있으므로 실제 측면과 같은 조건의 solid/wire를 대조한다. 비균일 Scale이나 리그를 무조건 적용하지 않는다.

## Sampler에서 두 재질을 분리한다

기존 가죽 프로젝트를 보존하고 별도 프로젝트/재질로 시작한다. 새 재질 창에서 이름, 해상도, OpenPBR/ASM, 필요한 채널을 직접 확인한다. Base Material은 일반 표면의 출발점이며, Coating은 별도의 반사층 설정을 제공한다. 내보낸 코팅 채널이 대상 렌더러에 자동 연결된다고 가정하지 않는다.

봉제실은 기존 한 땀의 볼륨을 유지하고 섬유의 방향·미세 요철·왁스 광택을 추가한다. Cloth Weave의 경사/위사 설정은 서로 구별된다. 실 종류·섬유 수·폭·장력·마감 설정을 실제 화면에서 확인하고, 필요한 섬유 영역만 실의 길이 방향 UV에 대응한다. 직물 전체의 교차무늬를 굵은 실 한 가닥으로 오인하지 않는다. 소형 실에 거대한 직물 타일을 그대로 입히지 않는다.

Quilt Stitch는 바탕 재질 위에 봉제·이음·퀼팅·도색 패턴을 만드는 기능이다. 이미 실제 실과 구멍이 있는 제품에 그대로 겹치면 봉제 표현이 중복된다. 이 경우 한 땀 형상을 새로 만드는 용도로 사용하지 않는다. 문서의 Edge Paint도 퀼팅 구획 경계 효과이므로 지갑 전체 외곽의 형상 베벨을 대신하지 않는다.

엣지코트는 비금속 도막으로 시작하고 사진의 색, 넓고 부드러운 반사, 작은 표면 불균일을 맞춘다. 거친 가죽 엠보싱을 그대로 복사하지 않는다. 도막의 넓은 형태는 메시, 작은 붓결/표면결은 낮은 강도의 노멀·높이와 거칠기로 분리한다. 수치는 사진 비교용 후보로 기록하며 실측 물성으로 주장하지 않는다.

## UV·출력·정렬 검수

1. Base Color는 색 공간, Roughness/Height/Normal은 데이터 공간으로 연결한다. 노멀의 DirectX/OpenGL과 높이의 돌출 방향을 별도로 확인한다. 지원되는 높이/노멀은 16비트로 출력하고 실제 헤더·채널 정렬·파일 존재를 확인한다.
2. 봉제실에는 길이와 둘레에 대응하는 새 UV를 사용하거나 기존 UV의 실제 의미를 확인한다. 끝부분의 수렴과 섬유 방향을 실제 접사에서 본다. 기존 UV를 덮어쓰지 않는다.
3. 전체 둘레의 각 실 끝을 가까운 바늘구멍과 대응하고 XY 위치뿐 아니라 가죽 표면에 진입하는 깊이도 본다. 같은 경로처럼 보인다는 이유로 일치 처리하지 않는다. 코너·시작/끝·부품 경계·안팎을 포함한다.
4. 양 끝 구멍이 서로 다른 표면에 속할 수 있다. 무제한 최근접 투영으로 반대쪽 면이나 슬롯 벽을 선택하지 않는다. 대상 부품·공유 구멍·한 땀의 방향을 제한한 뒤 수정한다.
5. 동일 카메라·중립 조명·색관리에서 전후 전체, 측면, 접사를 비교한다. 구멍 주변의 깨짐, 실의 뜸, 지나친 요철, 도막의 납작한 어깨를 확인한다. 저장·재열기와 외부 맵 경로 검증을 구별해 기록한다.

## 실제 학습 범위와 출처

서로 다른 Adobe 공식 문서 3개의 아래 본문을 브라우저에서 읽었다. 처음 문서가 비어 있는 상태에서는 학습 완료로 세지 않고 본문 로딩 후 다시 확인했다. 영상 시청·실측 복원·실기 성공 기록은 아니다.

| 출처 | 확인 범위·적용 |
|---|---|
| [Cloth Weave](https://experienceleague.adobe.com/en/docs/substance-3d-sampler/using/filters/generators/cloth-weave) — 2026-04-07 | 설명과 전체 매개변수: 경사/위사·실 종류·섬유 수·마감·높이/노멀·마스크. 직물과 한 가닥 실을 구별 |
| [Quilt Stitch](https://experienceleague.adobe.com/en/docs/substance-3d-sampler/using/filters/generators/quilt-stitch) — 2026-04-07 | 설명과 전체 매개변수: topstitch/seam/quilt/edge paint와 개별 강도·거칠기. 실제 봉제 형상 위 중복 적용 배제 |
| [Material creation presets](https://experienceleague.adobe.com/en/docs/substance-3d-sampler/using/interface/tools-and-widgets/material-creation-presets) — 2026-04-16 | 새 재질 작성·프리셋 범주·해상도·모델·채널·base fill. Coating/Fuzz와 일반 Base 출발점 구별 |

UI 언어, 현재 라이브러리 에셋 및 출력 채널은 실행 시 다시 확인한다. 전용 실 생성기의 존재, 사진 한 장의 정확한 물성 추정, 렌더러 간 전체 자동 호환은 이 문서로 검증되지 않는다. 교육은 Codex가 작성하고 Claude는 기존 문서를 읽어 제작에 적용한다.

## 도막 미세결 추가 학습 — 2026-11-05

기존 Brushed Paint 라이브러리 항목의 로드가 확인되지 않아, 적용 성공으로 기록하지 않았다. 다음 Adobe 공식 본문 3개를 별도로 읽어 기본 도막에서 시작하는 방법을 보강했다. 문서 열람 범위는 각 페이지 설명·전체 매개변수이며 영상 실습이나 제품 적용 성공을 뜻하지 않는다.

- [Paint](https://experienceleague.adobe.com/en/docs/substance-3d-sampler/using/filters/wear-and-finish/paint): 색·거칠기·두께와 Grain/Grain Size로 도막 결을 조절한다. 새 제품은 Peel을 0으로 두고 금속 효과를 추가하지 않는다. Normal/Height 채널 및 강도를 따로 확인한다.
- [Surface Relief](https://experienceleague.adobe.com/en/docs/substance-3d-sampler/using/filters/generators/surface-relief): 입력 결의 진폭·대비·반전·타일과 노멀/높이 혼합을 구별한다. 낮은 진폭의 표면 불균일 대안이며 엣지 베벨을 대신하지 않는다.
- [Varnish](https://experienceleague.adobe.com/en/docs/substance-3d-sampler/using/filters/wear-and-finish/varnish): 거칠기로 광택을 조절하고 두께가 커지면 아래 결이 완화된다. 현재 UI의 Coat And Varnish와 이름이 다르므로 동일 매개변수라고 단정하지 않는다.

세 문서 최종 표시는 모두 2026-04-07이다. Paint의 낮은 Grain 후보로 먼저 검수하고 실제 UV의 mm 환산과 접사 반사를 본 뒤 정한다. 사진에서 정확한 도막 물성을 역산했다고 주장하지 않는다.

## 제한된 실제 실행 확인 — Sampler 6.0.2 / Blender 5.2.2

별도 SSA에서 Cloth Weave와 Coating 출발점에 Paint 필터를 사용한 두 재질을 실제 생성·저장하고 4096² OpenPBR PNG로 출력했다. 실은 경사 폭을 0으로 두고 위사의 섬유 영역을 길이 UV에 대응했다. 도막은 비금속·Peeling 0·Grain 0.1 후보를 사용했다. 라이브러리의 Brushed Paint 항목은 로드 성공을 확인하지 못했으므로 사용했다고 기록하지 않는다.

색 선택창에서 HEX를 입력한 뒤 Return만 누르면 값이 바뀐 것처럼 보여도 Escape로 창을 닫을 때 취소될 수 있었다. 창 밖을 눌러 확정한 뒤 다시 열어 HEX와 미리보기를 대조했다. Qt 입력 직후 접근성 텍스트가 이전 상태를 반환하는 경우가 있어 새 화면과 최종 출력 파일을 함께 확인했다.

실 출력은 Base Color/Normal이 16비트 RGBA, Height가 16비트 회색, Roughness/Metalness가 8비트였다. 도막은 Base Color/Roughness가 8비트, Normal 16비트 RGBA, Height 16비트였다. 출력 템플릿이 채널마다 다른 비트를 사용할 수 있으므로 전체를 일괄 16비트라고 부르지 않는다. 파일 헤더와 값 범위를 별도로 검사했다. 일반 이미지 라이브러리가 RGB 16비트를 8비트 배열로 읽을 때 그 배열 통계로 원본 정밀도를 주장하지 않는다.

Sampler의 Preferences에서 원본 노멀 규약이 DirectX임을 직접 확인했다. Blender 5.2.2의 Normal Map 노드 실제 스키마에는 convention=DIRECTX가 있어 원본을 변환 없이 해석했다. 다른 Blender 버전에도 이 속성이 있다고 가정하지 않는다. 원본 DX 파일의 이름만 GL로 바꾸는 방식은 사용하지 않는다.

실·도막 Base Color/Roughness/Normal을 별도 새 재질과 새 UV로 연결하고 기존 UV·가죽 재질·가죽 Displace를 보존했다. 새 Height는 출력·보관했으나 실·도막의 실제 변위로 연결하지 않았다. 기존 가죽의 실제 변위와 새 재질의 노멀 표현을 구별한다. 섬유 주기와 도막 결의 mm 환산은 접사 검수용 가정이며 실측이 아니다.

실행 중 Sampler가 종료된 뒤 기존 실행 파일을 다시 열어 저장 SSA의 두 재질을 복구하고 Paint 필터 적용·출력을 확인했다. 종료 원인은 확정하지 않았다. 이 기록은 해당 프로젝트 재열기와 제한 기능 확인이며 모든 필터의 안정성 검증은 아니다. Blender 정지 Cycles 접사와 실제 구멍 진입 위치의 전수 검사는 수행했으나, 제품 영상의 전체 동작·시간적 반짝임·최종 외관 승인은 별도다.
