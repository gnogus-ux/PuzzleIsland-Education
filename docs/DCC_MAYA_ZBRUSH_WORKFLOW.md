# Maya·ZBrush 외부 스킬 문서 학습 매뉴얼

2026-11-01 · Scenario Maya11·ZBrush9 SKILL 전체 및 두 family README 확인. 고정 커밋 출처는 [개별 색인](SCENARIO_DCC_SUPPORT_INDEX.md)에 있다. 모든 앱·브리지·스크립트·예제·라이선스 실행은 미실행이다. 설치/설정 보류와 사용자 앱 조회 금지는 유지한다.

## 검증 상태부터 읽는다

Maya는 저자도 2027 미설치, 실제 Maya 호출 전부 미실행이라고 명시한다. 순수 Python·가짜 cmds 검사는 실제 API와 렌더 성공의 근거가 아니다. family README의 written scenario 성적도 제작 재현 성적과 다르다. 문서의 대상은 macOS Apple Silicon/Maya2027이며 현재 Windows에서의 지원을 뜻하지 않는다.

ZBrush는 저자의 2026.2.1/macOS에서 일부 palette·합성 stroke·OBJ/PNG export가 시험됐다고 보고한다. 그 위에 조합한 전문 스킬 전체는 시작 지연 문제로 실기 시험이 막혔다. 브리지 일부 성공, 각 함수의 미검증, 전체 workflow 미검증을 따로 기록한다. 저자의 tests/archive 경로는 빌드 프로젝트의 출처이며 이 저장소에 모두 포함된 실행물이라는 뜻이 아니다.

## Maya에서 재사용할 작업 순서

1. 목적·단위·카메라·예산·최신 원본을 정하고 읽기 진단을 남긴다. 현재 사용자 변경을 원본보다 우선 보존한다. 모델링용 정적 사본의 freeze/history 정리 예제를 skin·driver가 있는 사용자 원본에 일괄 적용하지 않는다.
2. 큰 형태와 가장 좁은 기능 크기로 그리드를 정한다. primary → cut/보조 형태 → 목적별 support/bevel/crease → low/bake copy로 나눈다. clay·wire·금속 반사로 표면 꺾임을 본다. 위상 편집 뒤 component index를 재사용하지 않는다.
3. 애니메이션용 부위는 승인된 template와 랜드마크·루프 지도로 설계한다. 자동 Retopologize는 얼굴의 완성법이 아니다. `polyRetopo` history의 재계산과 preprocess의 형태 평활화도 따로 고려한다. 양쪽 눈꺼풀·입술 대응, 입꼬리–볼·관절 단면, 의도된 구강/눈 개구부를 보존한다.
4. UV는 실제 카메라·타일 지원·최소 mip로 밀도와 간격을 정한다. 시임→전개→왜곡→밀도→크기 보존 패킹→체커·실제 이미지 순서다. bake와 export는 같은 삼각화와 tangent 계약을 사용한다. 영상의 3루프·2배 화면 픽셀·4K UDIM은 사양이 아니다.
5. 리그 단계가 승인되었을 때만 joint pivot/orient와 control을 구성한다. local/offsetParentMatrix/parent 조합을 이중 적용하지 않도록 좌표 공간을 명시한다. ordered blendMatrix와 normalized parentMatrix를 같은 가중 평균으로 생각하지 않는다. guides·가중치·build data를 보존하되 사용자 수작업을 disposable로 취급하지 않는다.
6. rigid block weight로 pivot/loop 문제를 먼저 찾고, region·twist·mask → smoothing → weight로 해결할 수 없는 corrective로 진행한다. Skin Tools layer 삭제는 평가 가중치를 유지하더라도 편집 상태를 잃으므로 JSON·후보를 보존한다. live maximumInfluences 변경이 가중치를 초기화할 수 있다는 원문 경고를 자동 수정으로 옮기지 않는다.
7. corrective는 pre/post와 transform/tangent 공간을 고른 후 만들고 실제 control이 구동하는 joint 행렬을 읽는다. 분리 shape의 합, rest의0/목표 pose의1, 단일 관절 ROM 다음 복합 포즈를 확인한다. 4영향·3~5twist·특정 오차는 원문 예제다.
8. 애니메이션은 reference·오디오·beat → proxy/stepped → 핵심 몸 → overlap → 얼굴 → polish다. spline 전후의 hold와 contact를 확인하고 기존 곡선에 key 삽입 시 인접 구간 변화를 검사한다. 실제 playblast와 화면 공간 움직임을 숫자 검사보다 함께 평가한다. 곡선 PNG만으로 game feel을 검증할 수 없다.

## Maya 재질·조명·FX·groom

map마다 색공간·grayscale 출력 채널·연결 위치를 계약한다. ACEScg 렌더에서 Rec.709 HDRI를 무조건 Raw로 두면 다른 의미가 된다. 입력의 실제 gamut과 OCIO 역할을 확인한다. normal 방향, UDIM, displacement 중립값·길이, OpenPBR와 Standard Surface의 단위·lobe 차이는 수치 복사로 해결하지 않는다. chrome/gray 기준을 둔 turntable 후 목표 광원에서 본다. 원문 hero displacement·roughness breakup은 사실적 예제의 선택이며 모바일 양식에 강제하지 않는다.

조명은 이야기의 초점·reference → 회색 block → light group solo → 값/분리 → noise AOV 진단 → 해당 sampler → EXR 합성 복원 순서다. 저자의 upstage key·rim 우선순위·2stop 분위기는 스타일 규칙이다. scene-linear EXR와 display PNG를 구분하고, denoise가 작은 디테일을 지우는지 확인한다. 라이선스 실패를 watermark로 우회해 최종 납품하지 않는다. 이 학습에서는 라이선스를 조회하지 않았다.

FX는 장면 cm와 solver m의 변환, real size, collider/garment 사본, pre-roll부터 고정한다. 값 하나씩 바꾸고 시작 프레임부터 순차 평가해 cache를 만든 뒤 cache 자체를 검수한다. 비어 있는 Bifrost 출력·당겨 읽지 않은 graph·범위 밖 시작 프레임을 성공으로 보지 않는다. 50frame pre-roll,30/35 solver 설정, 특정 fabric 수치는 시연 예제다. 캐시/범위/handles/단위/로그와 미검증을 넘긴다.

groom은 reference 위 흐름 화살표 → 적은 guide → 실제 Guide 연결 → clump 계층 → 길이·stray·mask → shader와 옆광 coverage → motion/cache 순서다. mask와 strength는 역할이 다르고 root가 뭉치면 scalp gap이 생길 수 있다. GPU 기반 Interactive Groom의 headless 평가와 brush stroke API 부재는 원문에서도 제약이다. Unreal Alembic 태그·root UV는 대상 엔진 계약에서 확인한다.

## Maya 코드·인계의 실패 복구

선택에 기대지 않고 긴 DAG 이름/UUID를 사용한다. main thread, undo chunk의 finally, OpenMaya 쓰기의 undo 제약, UI단위와 cm/radian의 차이를 기록한다. 2027 PySide6·OpenPBR·math node·삭제 flag와 OCIO 이름은 실제 버전 확인이 필요하다.

batch는 파일별 process·timeout·결과·로그를 분리한다. FBX 전역 옵션은 push/reset/명시 설정/질의/로그/pop, clip 범위와 take accumulator를 명시한다. clean reimport는 count뿐 아니라 per-mesh bounds·normal·축·scale·joint·take를 비교한다. USD는 frameRange·scheme·skeleton·단위도 확인한다. reference 이름/DAG를 바꾸면 shot edit가 깨질 수 있어 실패 edit·누락·unloaded부터 진단한다. 원문 bridge/commandPort는 localhost라도 인증 없이 코드 실행이 가능하므로 설치·사용을 이번 학습에 포함하지 않는다.

## ZBrush에서 재사용할 작업 순서

1. 버전·현재 Tool/SubTool·Edit 모드·단위 대응·원본 파일·보존할 level/UV/paint를 기록하고 버전 ZTL을 보존한다. ZPR 열기는 여러 Tool을 대체할 수 있다. TPose 데이터 보존에는 ZPR도 필요하다. QuickSave는 버전 관리의 대용이 아니다.
2. primitive/ZSphere/낮은 DynaMesh로 silhouette와 큰 mass를 만든다. constant pressure의 scripted stroke는 펜의 Z intensity와 같지 않으므로 별도 사본에서 보정한다. 큰 형태는 낮은 SDiv, 중간 형태는 그 다음, 미세 detail은 마지막이다. 해부학 성인 canon과 70/30·평행선 금지는 승인된 어린이 디자인의 재설계 근거가 아니다.
3. remesh가 필요한 시점에는 사본과 checkpoint를 둔다. 대칭 여부는 매번 명시한다. posed/asymmetric 원본에서 자동 half mirror를 하지 않는다. DynaMesh·boolean·ZRemesh가 UV·level·layer·morph target·열린 구강을 바꿀 수 있으므로 위험 영역을 별도 보존한다.
4. retopo는 neutral과 polygroup/경계 가이드를 준비하고 실제 eyelid·mouth·finger 흐름을 검사한다. 자동 결과의 count·flow가 부족하면 human/다른 DCC의 계획된 수선이 필요하다. retry sweep 마지막 상태가 최선 선택인지 재확인한다. 임의 hole fill로 눈·입을 막지 않는다.
5. projection은 원본/target만 명확히 보이게 하고 checkpoint·morph target·layer·위험 영역 mask를 준비한다. 각 level의 비교를 본다. spike를 blind smooth로 지우지 말고 저장된 target·국소 재투영으로 복구한다. Dist0.1,5k target,특정 백분율은 예제다.
6. UV는 최저 교환 level에서 준비하고 map은 같은 SubTool의 level 차이 계약으로 만든다. normal tangent/world, green/FlipV, displacement Mid·bits·scale를 인수 renderer와 맞춘다. 32-bit이므로 항상0 또는 항상0.5라는 식으로 정하지 않는다. 각 SubTool의 Export Scale·offset과 실제 내보낸 치수를 확인한다.
7. 새 low·projected stack·maps·ZTL·분리 parts·실제 본 시각 근거·미검증을 인계한다. OBJ/GoZ의 이름과 정점 순서 계약을 유지하고 상대 앱에서 scale·axis·normal을 확인하기 전에는 왕복 성공이라 보고하지 않는다.

## ZBrush 특수 작업과 자동화의 한계

hard surface는 polygroup의 crease 계획, SmoothSubdiv와 CreaseLvl 간격, live cutter·array, boolean 전/후 coplanar·issues, 금속 반사·평면성을 검수한다. Mirror And Weld 방향과 good half를 확인한다. UV/layer/crease를 잃는 commit은 별도 사본에서 한다. micro detail은 topology가 확정된 뒤다.

paint는 vertex color이므로 실제 점 밀도와 map 픽셀 배분을 비교한다. 중립 MatCap와 Flat에서 색을 보고 mask·낮은 opacity를 단계별로 적용한다. 원문의 성별 피부 zone·사실적 saturation·4M점/2K는 루미의 승인 색감이나 보편 상한이 아니다. subdivision 뒤 paint가 반드시 파괴된다는 절대 설명도 실제 데이터와 보간을 확인해야 한다. source gamma2.2/1.8 예제는 모든 EXR의 색관리 규칙이 아니다.

pose/print는 게임 제작과 별도 목적이다. lowest level, TPose의 point order(개수만 같아도 부족), rigid prop 전체 변환, 각 부품 export scale를 유지한다. hollow·keys·drain은 print copy에서 하며 STL 무단위/3MF 단위를 기록한다. 1mm wall·0.12mm fit·104% PVC는 특정 재료/장비 예제로 실제 slicer·시험 출력 없이 제작 보증하지 않는다. 이 교육은 출력·새 포즈·리깅 승인도 아니다.

자동화는 파일별·단계별 호출, checkpoint, timeout, durable report, 입력/recipe hash로 resume한다. timeout은 queued code 취소가 아니므로 상태부터 확인한다. plugin이 제어권을 반환하지 않거나 dialog가 뜨면 사용자 앱을 강제 종료하지 않는다. 원문 owned process 재시작도 현재 단일 점유·사용자 보존 정책 아래에서만 가능한 별도 실행 결정이다. `press_key`·undo·mask/layer 데이터 제약, 잘못된 path의 silent set을 사전 확인한다. Force UV Auto-Unwrap와 Substance Bridge 언급은 Painter 연결 허가가 아니다.

최종 인계에는 성공 파일뿐 아니라 failed/partial·마지막 저장·변경 여부·계속 실행 중인지·복구 가능한 다음 단계까지 남긴다. 앱이 시작되지 않은 상태에서 반복 호출로 크레딧이나 시간을 소모하지 않는다.
