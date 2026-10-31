# 피부 레이어 · Adobe 공식 10개 수업 매뉴얼

[세 강좌 안내](PAINTER_CHARACTER_WORKFLOW.md) · [Adobe 공식 강좌](https://www.adobe.com/learn/substance-3d-painter/web/texturing-characters-in-substance-3d-painter), Magdalena Dadela, 표시 길이 74분.

공식 페이지의 10개 수업 제목을 읽고, 제목·순서·강사 설명이 일치하는 [Adobe Substance 3D 공식 재생목록](https://www.youtube.com/playlist?list=PLB0wXHrWAmCyxQQSMWfYuTRT1pntzCjY7)의 실제 영상 10개를 확인했다. 공식 페이지 자체의 DOM에서는 영상 주소를 얻지 못해 공식 채널 영상을 사용했다. 표본 시점 184개, 원본 크기 UI 8장 직접 확인. 음성 전체와 모든 프레임을 연속 검토한 것은 아니다.

## 수업별 실제 확인 범위

아래 시간은 각 수업 안의 시간이다. 고유 시점 수는 전체 흐름 표본+주요 구간+로컬 AI 입력을 중복 제거한 수다.

| 수업·영상 | 고유 시점 | 실제 화면에서 확인한 내용 | 작업에 적용할 원리 |
|---|---:|---|---|
| 1. [Introduction](https://www.youtube.com/watch?v=57ybKwtYoV4) | 5 | 00:10–00:30 완성 예시와 레이어/표시 설정 | 완성 예시는 목표 이해용, 새 제작 절차의 증거와 구분 |
| 2. [Setting up the scene](https://www.youtube.com/watch?v=N-FwA4A0nks) | 17 | 00:45–01:15 새 프로젝트, 02:00–03:00 환경/카메라, 04:00–04:22 베이크 창 | 메시·노멀 입력, 표시 환경과 베이크 준비를 먼저 고정 |
| 3. [Adding skin details](https://www.youtube.com/watch?v=cpAPk72xq-I) | 18 | 01:00 피부 소재 목록, 01:45 과한 요철, 03:00 UV Scale, 04:00 이후 마스크 Paint, 07:15 체크무늬 | 요철의 물리적 크기·세기·국소 범위와 UV 늘어짐을 함께 확인 |
| 4. [Tips for skin texturing](https://www.youtube.com/watch?v=YmZrz3hmhZg) | 11 | 00:30–02:30 피부/주근깨/색 분포 참고 이미지 비교 | 피부를 단색 또는 무작위 점으로 처리하지 않고 큰 분포부터 관찰 |
| 5. [Creating skin base color](https://www.youtube.com/watch?v=1L5hJalAUHg) | 29 | 02:00 기본색, 04:00 마스크, 07:00–11:00 색 변화, 12:00 붉은 Fill, 12:30–14:00 마스크/Levels, 15:00 이후 단독 색 보기 | 따뜻한색·차가운색·국소 변화는 독립 레이어와 마스크로 축적 |
| 6. [Refining layers](https://www.youtube.com/watch?v=eMX6Xo3D44Q) | 15 | 00:30 색 보기, 01:00–02:30 얼굴/목/어깨의 브러시 수정, 03:00 큰 검은 중간 자국 후 03:30 제한된 결과 | 전체 패턴 뒤에 국소 수정을 추가하고 임시 자국과 최종 상태를 구분 |
| 7. [Skin modifiers](https://www.youtube.com/watch?v=ERhrJIiN38o) | 24 | 01:00 Source 소재 목록, 04:00 주근깨, 06:00 색 보기, 09:00 체모, 11:30 과도한 점 마스크, 12:00 정리된 예시 | 소재를 전체 피부에 그대로 덮지 않고 빈도·크기·마스크를 조절 |
| 8. [Using SSS](https://www.youtube.com/watch?v=20Af67BNcUE) | 26 | 01:30–04:45 흑백 마스크·Levels·Paint, 05:15 재질 복귀, 06:45 Display의 SSS 활성 | 마스크/Scattering 데이터와 렌더러 표시 옵션을 구별 |
| 9. [Creating roughness](https://www.youtube.com/watch?v=ka9v9OiGoz8) | 24 | 02:00 Roughness 값, 04:00–05:00 패턴/마스크, 07:00 Roughness 단독 보기와 레이어 혼합, 08:30 얼굴 국소 페인트 | 색 변화와 광택 변화를 분리하고 회색조 맵과 반사를 함께 검사 |
| 10. [Texturing dark skin](https://www.youtube.com/watch?v=LBEH_1_oz-s) | 15 | 00:30 완성 예시, 01:00–02:30 여러 피부 사진, 02:45–03:15 피부색 변형 예시 | 한 가지 피부색에 검정을 곱하는 방식으로 단순화하지 않고 실제 참고의 색/반사를 관찰 |

10번째 수업은 참고 비교 비중이 크다. 사진의 사람을 식별하거나 루미의 피부색 변경을 승인받은 것으로 해석하지 않는다. 참고 사진·피부 소재 원본은 저장소에 재배포하지 않았다.

## 순서대로 따라가기

### 1. 메시·UV·표시 환경 준비

새 프로젝트에 승인된 메시 버전을 지정하고 사용할 노멀 규약과 기존 베이크 맵을 기록한다. 수업 2의 01:00 화면은 Painter **2019.1.2**, 해상도 1024, Normal map format **OpenGL**, 기존 `beast_head_Normal.tif` 입력을 보여준다. 이는 예제 설정이며 루미의 최종 규격이 아니다.

환경맵을 바꾸면 피부 반사와 밝기가 달라진다. 작업 전후 비교에 사용할 환경·노출·카메라를 고정한다. 고해상도 노멀을 이미 받은 경우에도 AO/Curvature/Position/Thickness의 필요성과 생성 상태를 따로 확인한다. 04:00 베이크 창의 512와 경고 표시를 모든 맵 최종 베이크 완료의 근거로 쓰지 않는다. 수업 화면에는 일부 시점에서 메시 노멀 재계산 경고와 읽기 전용 표시도 있다.

### 2. 큰 형태와 미세 요철을 분리

피부 디테일용 Fill은 필요한 Height/Normal 채널 위주로 시작한다. UV Scale로 반복 크기를 맞추고 너무 거친 모공·주름은 세기를 줄인다. 부위별로 다른 크기의 패턴이 필요하면 레이어를 나누고 마스크로 연결한다. 수업 3의 03:00 화면에는 `Male Shoulder Skin 4`와 UV Scale 약 111.97이 읽히지만, 메시/UV 크기가 다르면 같은 숫자의 결과가 다르다.

체크무늬로 눈/입/귀/목의 늘어짐을 확인한다. UV 경계를 숨기기 위해 강한 노이즈를 더하지 않는다. 실루엣·눈꺼풀 두께·입술 모양은 텍스처로 고칠 수 있는 범위와 구별하며 실제 형태 변경에는 Guide가 먼저다.

### 3. 피부색을 관리 가능한 레이어로 쌓기

승인된 기본 피부색을 아래에 두고, 넓은 색 변화 → 국소 홍조/입술 → 필요한 작은 반점 순으로 쌓는다. 각각 색·마스크·혼합량을 독립적으로 조절한다. 레이어 이름은 `Skin_Base`, `Warm_Variation`, `Cheek_Mask`처럼 역할이 읽히게 붙인다. 이 이름은 매뉴얼 제안이며 원본 화면의 정확한 이름을 전사한 것이 아니다.

단독 Base Color 보기에서 조명에 의한 그림자가 빠져도 색 분포가 자연스러운지 보고 재질 보기로 돌아와 확인한다. 수업 5의 강한 빨강이나 수업 7의 큰 점 패턴은 중간 마스크 작업이다. 루미의 어린 인상을 보존하려면 노화 반점·체모·굵은 혈관·깊은 주름은 목표에서 제외한다. 실제 승인 원본과 비교하기 전 홍조/주근깨의 양도 확정하지 않는다.

### 4. SSS는 별도 데이터와 표시 조건을 함께 확인

수업 8에서 흑백 마스크와 Levels를 조절한 뒤 Display Settings의 `Activate Subsurface Scattering`을 켜고 Scattering 채널을 다룬다. 06:45 화면의 Scattering 약 0.0378은 Painter 예제의 순간 값이다. Blender의 Subsurface Weight/Radius/Scale에 동일 숫자로 복사하지 않는다.

Blender 5.2에서는 Weight·Radius·Scale·방법이 각각 역할을 가진다. 현재 [Principled 공식 설명](https://docs.blender.org/manual/en/5.2/render/shader_nodes/shader/principled.html)에 맞춰 모델 크기와 렌더러에서 다시 조정해야 한다. 이번에는 피부 재질 제작이나 렌더 검증을 하지 않았다. Unity URP의 최종 피부 셰이더와 모바일 비용도 별도 판단 대상이다.

### 5. 거칠기는 얼굴 전체의 균일한 상수에서 끝내지 않기

Roughness 전용 Fill과 국소 마스크를 만들고 필요한 만큼만 변화시킨다. 예제 02:00의 약 0.7152와 07:00의 약 0.3873은 서로 다른 레이어·시점 값이다. 둘 중 하나를 피부 전체 처방으로 고정하지 않는다. 회색조 맵의 대비와 재질 반사를 함께 비교한다. 코·입술·눈의 광택을 피부 전체에 퍼뜨리지 않으며 실제 승인 스타일을 우선한다.

## 완료 기준과 한계

- 레이어/마스크를 끄면 해당 효과만 사라지고 기본 피부색·다른 재질은 보존된다.
- 같은 조명·시점에서 피부톤, 눈/입 경계, UV 솔기, 모공 크기를 비교한다.
- 색·Roughness·Normal·SSS용 데이터의 역할과 출력 대상을 표로 남긴다.
- Painter의 예쁜 미리보기와 Blender/게임의 최종 재질을 같은 것으로 선언하지 않는다.

이 강좌는 사실적인 성인 판타지 흉상 예제다. 레이어 분리와 검토 방법을 배우는 자료이며 루미에 그 디테일·연령·외모를 도입하는 디자인 지시가 아니다. 소재 사용권·현행 앱 재현·최종 게임 품질은 미검증이다.
