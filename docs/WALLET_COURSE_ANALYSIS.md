# 지갑 모델링과 표면 맵 강좌 10편 분석 기록

분석일은 2026년 11월 1일이다. 모델링 5편과 범프·디스플레이스먼트 5편을 대상으로 원본 영상의 시간대별 화면, 확보된 자막, 로컬 시각 분석을 대조했다. 과거 완료한 심리스 강좌 5편과는 별도 작업이다.

이 기록에서 ‘학습’은 프로젝트에 다시 사용할 제작 원리와 확인 기준을 정리했다는 뜻이다. 모델 가중치를 재훈련한 것이 아니다. 전체 타임라인의 장면·움직임 분석과 표본 화면의 의미 분석을 구분하며, 모든 프레임과 모든 마우스 조작을 연속 시청했다고 표현하지 않는다.

## 1. 강좌별 확인 결과

### M1 Alper Güzeler의 지갑 아이콘

[Blender 3D Wallet Model – Quick and Easy Modeling Tutorial](https://www.youtube.com/watch?v=xkWrT79HkTI) · 약 10분 10초

- **화면 근거:** 00:30 둥근 판 형태, 01:30 잠금 띠의 모서리 편집, 04:00 Bevel 설정, 05:00 동전 반복, 08:30~10:00 색상·조명 편집이 보인다.
- **가져올 원리:** 단순한 부품을 나누어 비례를 맞추고 모서리 반경으로 읽기 쉬운 외형을 만든다.
- **적용 범위:** 빠른 시안용이다. 두꺼운 아이콘 형태와 장식 지폐를 예시 제품의 실측 구조로 옮기지 않는다. 확인한 화면에는 카드 슬롯 작동이나 접힘 애니메이션 검증이 없다.
- **근거 제한:** 자막을 확보하지 못해 화면을 중심으로 분석했다. 작은 메뉴 값은 실측 사양으로 채택하지 않았다.

### M2 blendereverything의 지갑 배속 모델링

[speed modeling a wallet in blender 2.8 part 1](https://www.youtube.com/watch?v=2w6d4JSK3mw) · 약 9분 24초

- **화면 근거:** 00:30~03:00 외곽과 테두리 루프·분리 파트, 03:30 펼친 실물 참고 사진, 04:30~06:30 내부 판의 면 조절, 07:00~08:30 겹치는 포켓과 Solidify가 보인다. 08:00 원본 화면에서 두께의 음수 부호와 Offset도 확인했다.
- **가져올 원리:** 실물 외관·내부 참고를 나란히 두고, 얇은 판의 외곽과 지지 루프를 먼저 만든 뒤 두께를 준다.
- **현재 활용:** 10편 중 내부 포켓 제작에 가장 직접적이다. 영상 속 두께 수치를 현재 2mm 몸판이나 1mm 등 가죽에 복사하지 않는다.
- **근거 제한:** 자막 없는 배속 영상이다. 이 Part 1의 마지막 화면은 진행 중인 모델이며 완성된 제품 동작 검증으로 보지 않는다.

### M3 Lexa Yosh의 미니멀 지갑

[Minimalist Women’s Wallet Design with Blender – Part 1](https://www.youtube.com/watch?v=-mn100riec4) · 약 9분 1초

- **화면 근거:** 01:00 접힌 외피와 Solidify, 02:00~04:30 별도 잠금 띠의 둥근 외곽, 05:00~06:00 원형 장식, 이후 지폐 모양 부품을 편집하는 화면이 보인다.
- **가져올 원리:** 접힌 외피의 큰 단면과 분리된 부품을 간단히 구성하고 Bevel·두께를 조절한다.
- **현재 활용:** 닫힌 외형 시안과 단면 참고용이다. 카드 슬롯·봉제·리깅을 포괄하는 강좌로 확대 해석하지 않는다.
- **근거 제한:** 영상 자체가 약 720p이며 UI 일부가 잘려 있다. 자막 요청도 제한돼 확보하지 못했다. 읽히지 않는 수치와 숨은 조작은 기록하지 않았다.

### M4 Dnsr Design의 Cloth Filter 지갑

[Blender Cloth Filter – Wallet](https://www.youtube.com/watch?v=jVgxGea8mE8) · 약 4분 4초

- **화면 근거:** 00:20 기존 접힌 모델, 01:00~02:10 격자 면과 영역 구분, 03:00 Sculpt Mode의 Inflate·Use Face Sets, 03:40 퀼팅 결과가 보인다.
- **가져올 원리:** 영역을 구분해 제한된 구역의 볼륨을 조절한다.
- **현재 활용:** 향후 퀼팅 제품 또는 큰 눌림 시험에 한정한다. 현재 내피의 작은 가죽 엠보싱을 이 다이아몬드 격자로 대체하지 않는다.
- **근거 제한:** 확보한 자막은 음악 등 7행으로 제작 설명에 도움이 되지 않는다. 도구 판정은 원본 화면과 공식 문서로 확인했다.

### M5 PIXXO 3D의 봉제선

[Tutorial: Quick Stitches in Blender 3.0](https://www.youtube.com/watch?v=LxRl6K-S5T4) · 약 8분 4초

- **화면·자막 근거:** 01:30~02:30 경로 홈과 엣지 복제, 03:00~04:30 경로와 실 원점 조절·커브 변환, 05:00 Array와 Curve, 06:00~07:00 실 두께와 Catmull-Clark가 확인된다.
- **가져올 원리:** 표면을 따르는 경로와 한 땀의 모양·간격을 분리해 편집한다. 원점 정렬, 진행 축, 마지막 실 배치를 검사한다.
- **현재 활용:** 지갑 테두리와 포켓의 실밥에 직접 응용한다. 원본 Suzanne의 Count를 제품 봉제 간격으로 취급하지 않는다.
- **근거 제한:** 이 강좌는 고정 모델의 봉제 예제다. 지갑 접힘을 따라가는 리그 연결은 별도 설계·검증이 필요하다.

### D1 Reawote의 맵 구분

[Normal map, bump map and displacement map explained in 4 minutes](https://www.youtube.com/watch?v=KH_o4KcsVyA) · 약 3분 58초

- **화면·자막 근거:** 00:40~01:40 범프·노멀과 평평한 외곽, 02:00~02:40 노멀 규약과 채널, 03:16~03:20 변위 강도, 03:40 비트 깊이를 비교한다.
- **가져올 원리:** 음영 변화와 실제 형상 변화를 구분하고, 노멀 규약과 높이 정밀도를 확인한다.
- **현재 활용:** 결을 범프로 표현할지 실제 변위를 쓸지 판단하는 기준이다. 영상의 amount 값은 현재 가죽의 mm 값이 아니다.
- **해석 교정:** 노멀이 언제나 범프보다 정확하다고 일반화하지 않는다. 맵 생성 방식·해상도·필터링과 용도가 결과를 좌우한다.

### D2 CG Infinite의 범프 제작과 연결

[Blender Bump map Tutorial – Blender Realistic Texturing Series 1](https://www.youtube.com/watch?v=DOn4G9HVo2M) · 약 6분 46초

- **화면·자막 근거:** 02:20~03:30 Photoshop의 흑백·Levels, 04:15 이미지 비율 조절, 05:30 잘못된 직접 Normal 연결, 06:00 Bump 경유 연결, 이후 Non-Color와 강도 조절을 설명한다.
- **가져올 원리:** 높이 이미지는 Bump의 Height로 보내고 Normal 출력을 셰이더로 연결한다. 대비와 조명을 함께 확인한다.
- **현재 활용:** 파란 가죽의 범프 연결과 약한 강도에서의 형태 확인에 유용하다.
- **해석 교정:** 자막의 ‘모든 3D 텍스처는 정사각형이어야 한다’는 설명은 채택하지 않는다. 비정사각형 이미지도 UV 비율을 맞추어 사용할 수 있다. 단순 흑백 변환은 촬영 조명과 실제 높이를 분리하지 못한다.

### D3 Blender Inferno의 범프와 두 변위 경로

[The ONLY BUMP and DISPLACEMENT Guide YOU Need](https://www.youtube.com/watch?v=4yfNK1PG4Pk) · 약 12분 19초

- **화면·자막 근거:** 01:03 Height→Bump, 02:38~03:04 Bump Normal의 연쇄 연결, 04:14 재질의 변위 방식, 05:30 세분화, 07:00~07:30 세분화 순서와 UV, 08:30~08:36 Apply, 후반 퀴즈를 확인했다.
- **가져올 원리:** 재질 노드 연결, 렌더 조건, 세분화, UV를 하나의 경로로 점검한다. modifier는 실제 메시를 바꾸며 Apply는 편집 가능성을 줄인다.
- **현재 활용:** 파란 내피의 기존 Displace 후보를 검토하는 핵심 자료다.
- **해석 교정:** 화면은 Blender 3.3.1이다. 설명의 Midlevel 1, 높은 세분화, Experimental 설정을 현재 가죽에 고정 적용하지 않는다. 세분화만 늘려도 범프가 자동으로 실제 변위가 되는 것은 아니다.

### D4 The Rendering Essentials의 Materialize

[FREE TOOL For Creating PBR Material Maps from Photos – Materialize](https://www.youtube.com/watch?v=GItohAbyzCM) · 약 10분 11초

- **화면·자막 근거:** 02:30 바닥 사진, 03:00~05:03 Height From Diffuse와 주파수·대비, 05:30~06:47 Normal From Height, 07:00 AO, 07:30~08:40 전체 재질·여러 형태, 09:00~09:30 저장 파일을 확인했다.
- **가져올 원리:** 높이를 먼저 정하고 파생 노멀을 생성한다. 미리보기와 확정을 구분하고 여러 주파수의 결과를 비교한다.
- **현재 활용:** 이미지 편집 경로와 비교할 수 있는 사진 기반 맵 제작 절차다.
- **해석 교정:** 바닥 사진의 색 차이가 모두 높이는 아니다. 이 강좌의 Parallax 미리보기는 Blender 정점 변형 검증이 아니며, 심리스 제작 자체는 시연하지 않는다. 저장 화면으로 16비트를 단정할 수 없다.

### D5 Class Outside의 Materialize와 Blender 연결

[Create Texture Maps Generate PBRs with Materialize](https://www.youtube.com/watch?v=kvJuC8Wj_lQ) · 약 12분 56초

- **화면·자막 근거:** 02:28~03:44 Height·Normal, 04:00~06:45 Metallic·Smoothness·Edge·AO, 07:59 저장 맵, 09:30 Node Wrangler 결과, 10:29 AO Multiply, 10:58 Smoothness 반전, 12:19~12:30 조정과 변위 미적용 설명을 확인했다.
- **가져올 원리:** 맵별 의미와 연결을 검사한다. 자동 연결에서 누락된 맵을 확인하고 Smoothness를 Roughness에 맞게 반전한다.
- **현재 활용:** 높이·노멀·거칠기의 역할을 분리하는 최종 연결 검수에 유용하다.
- **해석 교정:** 가죽에는 도끼의 금속 마스크가 필요하지 않다. 이 영상의 ‘bake’ 표현은 사진에서 맵을 추정하는 과정이며 고해상도 형상을 저해상도 메시로 베이킹한 검증과 다르다. 영상은 실제 높이 변위 완료를 주장하지 않는다.

## 2. 로컬 시각 모델의 오독과 채택 기준

Qwen3-VL 결과를 원본 화면과 대조했다. 다음 내용은 채택하지 않거나 교정했다.

| 자동 분석 내용 | 원본 대조 결과 |
|---|---|
| M2의 보라색이 modifier 적용 완료를 뜻한다 | 선택·표시 색만으로 Apply를 증명할 수 없다. 08:00에는 modifier가 편집 가능한 상태로 보인다 |
| M2 두께를 양수로 읽음 | 08:00 원본은 음수 부호가 보인다. 어느 쪽이든 현재 실측값으로 복사하지 않음 |
| M3에서 특정 Add·Extrude 조작을 단정 | 정지 화면만으로 클릭 이력을 확정할 수 없어 결과 형태만 기록 |
| M4의 Cloth Filter를 확인할 수 없다고 응답 | 별도 03:00 원본에서 Inflate·Use Face Sets와 관련 도구 UI 확인 |
| M5 Alt+A가 커브 생성이라고 설명 | 해당 화면은 Suzanne 편집 상태이며, 커브 생성은 이후 복제·분리·변환 순서로 확인 |
| M5의 세분화를 Simple로 설명 | 07:00 원본은 Catmull-Clark 선택 상태 |
| D1 설명 슬라이드를 근거 부족으로 처리 | 슬라이드와 자막으로 범프/노멀/변위 개념 비교를 직접 확인 |
| D2의 표본만으로 Bump 연결을 확인하지 못함 | 별도 06:00 원본과 후반 자막에서 연결과 Non-Color 설명 확인 |
| D3에서 ‘낮은 Height 값’을 보편 원리로 제시 | 연결된 입력·Scale·Midlevel·실제 맵 범위로 판단해야 하므로 배제 |
| D4의 화면만으로 preset 클릭을 단정 | 패널 표시와 시점별 결과만 기록. 숨은 클릭 순서는 단정하지 않음 |
| D5에서 생성·연결 근거가 부족하다고 응답 | 전체 시점 시트와 자막에서 맵 생성·저장·연결·결과를 직접 확인 |

Qwen의 `uncertainty: No/None`은 검증 증거가 아니다. 정확히 읽히지 않는 숫자와 순간적인 클릭은 매뉴얼의 고정값으로 채택하지 않았다.

## 3. 예시 지갑에 남기는 제작 원칙

1. 실제 카드 공간과 가죽 두께를 먼저 만들고 표면 결은 그 위에 추가한다.
2. 봉제선은 경로·한 땀·간격·접힘 연결을 별도로 제어한다.
3. 퀼팅 부풀림과 작은 가죽 엠보싱은 다른 크기의 작업이다.
4. 사진의 색, 촬영 명암, 상대 높이와 거칠기는 같은 데이터가 아니다.
5. Height를 Non-Color로 읽고, 미세 결은 범프부터 검수한다.
6. 실제 변위에는 충분한 정점·올바른 UV·중립값·단위·적용 범위가 필요하다.
7. 저장 파일의 비트 깊이와 반복 품질을 검사한다. 16비트라는 이유만으로 심리스나 실제 스캔 높이가 되지 않는다.
8. 새로운 시험은 승인 모델·본편 영상과 분리하고 비교 가능한 기록을 남긴다.

## 4. 분석 범위와 검증 자료

원본 영상은 10편 모두 로컬에 확보했다. 시간대별 화면 308개를 57개 시트로 직접 검토했고, 그중 8개 시점을 원본 해상도로 추가 대조했다. 제작 설명을 포함한 자막은 6편에서 확보해 읽었다. M4의 음악 자막 7행은 설명 근거에서 제외했고, M1·M2·M3는 자막 없이 화면을 분석했다.

로컬 Qwen3-VL은 10요청·40표본 프레임을 처리했다. FrameLens는 10편 전체 타임라인을 폭 640px·2fps 프록시로 처리하는 장면·움직임 분석에 사용했다. 이 두 결과가 모든 조작의 의미를 자동으로 확인했다는 뜻은 아니다. 세부 집계는 [공개 분석 범위](https://github.com/gnogus-ux/PuzzleIsland-Education/blob/main/reports/VideoLearning/20261101_WALLET_COURSES_VERIFICATION.json), 공개 파일 해시는 [정본 파일 목록](https://github.com/gnogus-ux/PuzzleIsland-Education/blob/main/PUBLIC_MANIFEST.json)을 기준으로 한다.

원본 영상·자막·전체 캡처는 작업 폴더의 검증 근거로 보존한다. 매뉴얼에는 내용을 재구성한 설명과 원문 링크를 담았다. 새 텍스처 제작, Blender 수정, 렌더와 외부 게시를 이번 문서화 작업의 완료로 포함하지 않는다.

## 5. 공식 문서와 프로젝트 근거

현재 동작과 용어는 다음 Blender 5.2 문서로 대조했다. 강좌의 2.8·3.0·3.3 UI를 현재 설치 버전의 메뉴와 동일하다고 가정하지 않는다.

- [Solidify](https://docs.blender.org/manual/en/5.2/modeling/modifiers/generate/solidify.html)
- [새 Array](https://docs.blender.org/manual/en/5.2/modeling/modifiers/generate/array.html)와 [Array Legacy](https://docs.blender.org/manual/en/5.2/modeling/modifiers/generate/array_legacy.html)
- [Curve modifier](https://docs.blender.org/manual/en/5.2/modeling/modifiers/deform/curve.html)
- [Cloth Filter](https://docs.blender.org/manual/en/5.2/sculpt_paint/sculpting/tools/cloth_filter.html)
- [Bump](https://docs.blender.org/manual/en/5.2/render/shader_nodes/displacement/bump.html)와 [Normal Map](https://docs.blender.org/manual/en/5.2/render/shader_nodes/displacement/normal_map.html)
- [재질 변위](https://docs.blender.org/manual/en/5.2/render/materials/components/displacement.html), [Displacement 노드](https://docs.blender.org/manual/en/5.2/render/shader_nodes/displacement/displacement.html), [Displace modifier](https://docs.blender.org/manual/en/5.2/modeling/modifiers/deform/displace.html)
- [Image Texture](https://docs.blender.org/manual/en/5.2/render/shader_nodes/textures/image.html)

제품에 적용할 때는 승인 모델과 후보 파일, 실제 변위 검증, 반복 품질의 잔여 결함을 프로젝트 내부 기록에서 확인한다. 비공개 제품 자료는 공개 교육 문서에 포함하지 않는다.
