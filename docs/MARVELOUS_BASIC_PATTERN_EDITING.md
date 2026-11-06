# Marvelous Designer 입문 — 선택·점·곡선·입구·출력

2026-11-06 표본 영상·공식 문서 학습을 재사용 절차로 정리했다. **공식 영상 4편의 25시점, 그중 화면 영어 자막 12시점과 공식 문서 17개 본문을 검토한 범위**다. 전체 기초과정 완주·오디오 청취·연속 재생·별도 자막 트랙 전체·MD9 전 기능 실습을 완료한 자료가 아니다. 이 학습에서는 제작 앱을 실행하지 않았다. 원자료·시점·방법·버전 제한은 [학습 근거](../reports/VideoLearning/20261106_MARVELOUS_BASIC_SAMPLED_STUDY.json)에 있다.

[기존 재단·봉제 매뉴얼](MARVELOUS_WALLET_PATTERN_WORKFLOW.md)의 과거 실기와 2026-11-05 영상 3편/109시점/자동 자막 2트랙 검토는 당시 범위 그대로다. 이번 표본 수에 다시 더하거나 전체 입문과정 이수로 바꾸지 않는다. 다른 제작 담당의 실행 결과도 이번 교육의 실습 성과로 세지 않는다.

## 1. 작은 별도 문서에서 UI·선택·단위를 확인한다

현재 사용자 문서와 원본을 먼저 보존하고, 승인된 실습 단계에서 별도 시험 문서를 사용한다. 2D는 평면 외곽·내부선·봉제 대응, 3D는 배치·앞뒤·거동을 보는 화면이다. 화면을 확대하거나 옮긴 것과 패턴 치수를 바꾼 것을 구별한다.

1. 선택을 해제하고 현재 도구를 확인한다. 판 전체·외곽 구간·내부선·점을 하나씩 구별해 선택한다.
2. 하이라이트가 필요한 범위에만 생기는지 보고 속성 창의 Name과 선택 길이를 대조한다. 파일명이나 주석을 native Name 확인으로 대신하지 않는다.
3. 각 입력란의 단위 문자열을 읽는다. 영상에서는 생성창의 mm와 다른 속성의 in이 각각 관찰됐다. 같은 앱 안의 모든 숫자가 같은 단위라고 가정하지 않는다.
4. 알려진 기준 길이를 가진 간단한 시험판을 만들어 입력값·화면 반올림·출력 좌표를 구별한다. 의류 예제의 치수나 단축키를 제품 정답으로 복사하지 않는다.

곡선점 도구에서 선 위 클릭은 점 추가가 될 수 있다. 선택이 안 된다고 같은 선을 반복 클릭하지 않는다. 아이콘 좌표·단축키·패널 위치는 현지 버전과 사용자 설정에서 확인한다. [UI 시연](https://www.youtube.com/watch?v=uizpDJdz7aA)과 [Edit Pattern 시연](https://www.youtube.com/watch?v=yxrx_6QGx8E)의 표본은 선택·속성의 관계를 보여주며 현지 메뉴 전수 검증은 아니다.

## 2. 외곽과 점의 종류를 나눈다

[Polygon](https://support.marvelousdesigner.com/hc/en-us/articles/47358178952345-Polygon)의 생성 절차와 [생성 시연](https://www.youtube.com/watch?v=3pPxqtBGVxY)을 대조했다. 먼저 일반 구간점으로 필요한 직선을 만들고 생성 중 길이 입력과 방향 안내를 확인한다. 닫힌 판의 시작점·끝점과 개별 구간 경계를 기록한다. 길이 입력 하나가 절대 위치와 전체 외곽을 보증하지는 않는다.

| 대상 | 구별할 의미 | 확인할 것 |
|---|---|---|
| Segment Point | 구간 경계를 정하는 점 | 직선–곡선–직선이 각각 선택되는지 |
| Free Curve Point | 곡선 위에서 형태에 영향을 주는 점 | 추가·이동 전후 곡선이 바뀌는지 |
| AI Bézier handle endpoint | 앵커에서 나온 핸들의 끝 | 실제 핸들이 표시되고 그 끝이 선택됐는지 |
| 내부선의 점 | 판 안 기준 요소 | 외곽·절개·홀과 혼동하지 않는지 |
| 출력 메시 정점 | 테셀레이션 결과의 점 | native 구간점과 같은 ID라고 추정하지 않는지 |

정확한 이차 곡선과 원호는 다른 목표다. 길이나 반경을 비슷하게 맞췄다는 이유로 서로 대체하지 않는다. 곡선 위의 보간점을 Bézier 제어점으로 해석하지 않는다.

## 3. 곡선 편집은 선택 대상과 전후 경계를 함께 본다

[Edit Curve Point](https://support.marvelousdesigner.com/hc/en-us/articles/47358435895065-Edit-Curve-Point)와 [시연](https://www.youtube.com/watch?v=ryejfKAinvs)을 읽고 봤다. 새 자유 곡선점을 추가하면 기존 곡선 형태와 핸들 구조가 바뀔 수 있다. 점을 더하는 동작을 무손실 분할로 취급하지 않는다.

1. 원 외곽과 보존할 끝점·직선을 별도 Guide에 표시한다. 승인된 후보는 Guide와 다른 사본으로 만든다.
2. 곡선 양끝의 구간 경계와 곡선 내부점을 구별한다. 직선까지 한 곡선으로 선택되면 먼저 선택 구조와 점 종류를 확인한다.
3. 필요한 내부점만 바꾸고 직선·접속점·나머지 경계의 전후 좌표와 선택 범위를 확인한다. 위치와 접선 보존을 타입 이름만으로 보장하지 않는다.
4. [AI Bézier 편집](https://support.marvelousdesigner.com/hc/en-us/articles/47358445584537-Edit-AI-Bezier-Curve)의 핸들 동작은 실제 핸들이 보일 때만 적용 후보로 검토한다. 일반 점의 Delete Point를 핸들 끝점 삭제로 대신하지 않는다.
5. [점 타입 변환](https://support.marvelousdesigner.com/hc/en-us/articles/47358462704665-Convert-Curve-Points-Segment-Points) 후에는 형태와 구간을 다시 측정한다. 메뉴 실행 성공은 정확 곡선 보존의 증거가 아니다.

시연의 이동 중 우클릭 수치창은 이동량 입력이다. 절대 좌표나 핸들 좌표 입력으로 바꿔 해석하지 않는다. 사용하는 자동화 도구가 이동 도중 입력을 지원하는지도 별도 확인 사항이다. 모호한 대상에 반복 입력하거나 비공식 파일 편집·새 브리지로 우회하지 않는다.

## 4. 내부선·홀·Trace를 서로 다른 단계로 취급한다

[Internal Polygon/Line](https://support.marvelousdesigner.com/hc/en-us/articles/47358276422297-Internal-Polygon-Line)은 판 안의 열린 선이나 닫힌 형상을 만드는 기능이다. 기준선을 그린 것만으로 재료가 잘리거나 포켓 입구가 열렸다고 하지 않는다.

[Convert to Hole](https://support.marvelousdesigner.com/hc/en-us/articles/47358440603161-Convert-to-Hole-Internal-Shape)는 닫힌 내부 형상을 홀로 바꾸는 동작이다. 열린 선을 폭 없는 칼집으로 만드는 기능과 같다고 가정하지 않는다. 실제 유한 폭·닫힌 윤곽·둘레·재열기 후 유지와 통과 여부를 별도 시험한다.

[Trace](https://support.marvelousdesigner.com/hc/en-us/articles/47358289149465-Trace)는 선·영역을 패턴이나 내부 요소로 옮기는 기능이다. 교차점 결합 여부와 변형되는 대상이 옵션에 따라 달라질 수 있다. OBJ의 UV를 이용한 패턴 추적은 다시 별도의 가져오기 경로이며 원래 해석적 곡선의 차수·제어점을 복원한다는 보증이 아니다. 실패한 가져오기 경로와 다른 기능의 문서상 존재를 섞어 성공으로 보고하지 않는다.

겹친 내부도형의 면적 합집합(Union), 두 Pattern을 합치는 Merge, 열린 내부선 끝점을 잇는 Merge Points는 서로 다르다. Trace의 교차점 결합도 내부 경계를 제거한 면적 Union을 보장하지 않는다. **MD9의 Boolean Union→CutHole 명령 사슬은 이번 조사에서 지원·도입 버전 근거를 확보하지 못했다.** 기능 부재로 단정하거나 최신 문서의 동작을 MD9에 소급하지 않는다.

문서상 유효한 단일 닫힌 Internal Shape의 Convert to Hole 기능과 정확한 복합 홀의 실기 성공은 구분한다. 승인된 별도 시험에서는 분기·자기교차·중복·틈 없는 단일 닫힌 체인, 변환 뒤 실제 재료 경계와 홀을 가로지르는 면의 유무, 원호·목폭·접속점의 실제 출력, 저장·재열기 유지를 확인한다. [보강 학습 근거](../reports/VideoLearning/20261106_MARVELOUS_INTERNAL_SHAPE_HOLE_STUDY.json)는 공식8본문(신규7·재열람1)과9.5 명시 영상10표본의 조사이며 전체 영상·오디오 검토나 MD9 native 실기 완료가 아니다.

## 5. 봉제 전에 개방 경계와 방향표를 만든다

판 ID·경계 ID·양쪽 시작점·방향·길이·개방 여부를 표로 만든다. [Segment Sewing](https://support.marvelousdesigner.com/hc/en-us/articles/47358199517209-Segment-Sewing-2D)은 구간 연결, [Free Sewing](https://support.marvelousdesigner.com/hc/en-us/articles/47358239854361-Free-Sewing-2D)은 부분 경로 지정이라는 차이로 검토한다. 실제 연결 방향과 시작점은 별도 시험 문서에서 확인한다.

입구는 연결에서 제외하고, 방향 표시가 교차하면 상대 경계와 시작점부터 점검한다. 화면의 길이 경고 기준을 작은 제품의 허용 공차로 복사하지 않는다. 의도한 여유를 없애려고 모든 구간 길이를 강제로 맞추지 않는다. 봉제 구속 생성과 보이는 실·눌림·바늘구멍·실물 수납 검증은 각각 다른 범위다.

## 6. 앞뒤·Layer·두께·물성을 분리한다

- [Flip Normal](https://support.marvelousdesigner.com/hc/en-us/articles/47358334132633-Flip-Normal) 전후에는 판 앞뒤와 접힘 관련 값을 함께 확인한다. 봉제 방향 오류를 숨기려고 법선을 바꾸지 않는다.
- [Layer](https://support.marvelousdesigner.com/hc/en-us/articles/47358288780441-Use-Layer-Drape-Additional-Garment)는 시뮬레이션에서 겹침 순서를 돕는 설정이다. 실제 가죽층 수·두께·접착을 뜻하지 않는다. 배치가 안정된 후 중립 Layer에서 유지되는지 시험하는 절차도 현지 검증 대상이다.
- [Particle Distance](https://support.marvelousdesigner.com/hc/en-us/articles/47358268602777-Particle-Distance-Setting)는 메시 간격과 계산량에 관계한다. 낮은 값이 정확한 native 곡선이나 올바른 경계 연결을 만든다고 하지 않는다.
- [Collision Thickness](https://support.marvelousdesigner.com/hc/en-us/articles/47358430412441-FABRIC-PHYSICAL-PROPERTIES-Adjust-Collision-Thickness)와 [Rendering Thickness](https://support.marvelousdesigner.com/hc/en-us/articles/47358450148761-FABRIC-PHYSICAL-PROPERTIES-Adjust-Rendering-Thickness)는 충돌 간격과 보이는 두께를 나누어 읽는다. 한쪽만 바꿔 물리 간격·완성 단면까지 해결됐다고 하지 않는다.
- [Bending Weft/Warp](https://support.marvelousdesigner.com/hc/en-us/articles/47358432358809-FABRIC-PHYSICAL-PROPERTIES-Adjust-Bending-Weft-Warp)는 굽힘 저항이다. 가죽 preset 이름이나 의류 예제 숫자를 실물 측정값으로 쓰지 않는다.

외곽·봉제 방향·초기 배치부터 점검한 뒤 충돌 간격과 물성을 한 변수씩 시험한다. 이 학습에서는 가죽 물성 보정이나 시뮬레이션 성공을 검증하지 않았다.

## 7. 저장·재열기·출력을 각각 검증한다

[Project Open/Save](https://support.marvelousdesigner.com/hc/en-us/articles/47358219651225-Project-File-ZPrj-Open-Save)를 참고하되 현지 버전의 메뉴를 확인한다. 원본과 다른 후보명으로 저장하고 같은 파일을 재열어 판 수·Name·선택 구간·홀·봉제·앞뒤·PD·물성이 유지되는지 확인한다.

[OBJ Import/Export](https://support.marvelousdesigner.com/hc/en-us/articles/47358223288601-3D-File-OBJ-Import-Export)의 객체 분리·용접·Thin/Thick·단위·축·배율은 각각 기록한다. 알려진 기준 길이와 원점을 유지한 전후 파일을 비교하고 위치 맞춤·전역 scale로 잔차를 숨기지 않는다. Thin 출력은 완성 측면 두께 검증 자료가 아니며 Thick은 별도 단면 계측이 필요하다.

native 곡선, GUI 반올림 길이, 출력 메시를 구별한다. 직선도·접속점 위치·전체 곡선·나머지 경계·판 수·법선·UV를 나눠 검사한다. native 곡선과 메시 사이 테셀레이션 오차의 상계가 없으면 메시 측정만으로 native 정확도를 보장하지 않는다.

## 8. 버전 경계와 실제 시험 대기표

| 출처의 기능·표기 | MD9 적용 상태 |
|---|---|
| UI 영상 제목의 9.5 | 표본 UI 관찰이며 MD9 전 메뉴 호환 검증은 아님 |
| 나머지 세 영상의 구 UI·2020 copyright | 정확 버전 숫자 미확인; MD9.0으로 단정하지 않음 |
| AI Bézier의 Ctrl 핸들 각도 유지 | MD10 표기를 MD9 절차에서 제외 |
| Maintain Curve / Convert Only | 2024.2 표기를 MD9 절차에서 제외 |
| Show Pattern Layer 표시 | 2024.1 표시 기능을 MD9 필수 조건으로 요구하지 않음 |
| New Project의 ver12.1 설명 | MD9 실행 경로로 소급하지 않음 |
| OBJ Weld Turned / 충돌 방향 갱신 | 각각 2026.0 / 2026.1 설명을 MD9에 소급하지 않음 |

| 다음 제한 실습 | 남길 근거 |
|---|---|
| UI·점·구간 선택 | 실제 선택 대상·단위·속성·변경 전후 |
| 직선–곡선 분리와 편집 | 독립 구간·끝점·직선도·전체 곡선·보존 경계 |
| 내부선·홀·Trace | 서로 다른 기능의 입력·결과·실제 입구·재열기 |
| 봉제·앞뒤·Layer | 개방 경계표·방향·배치·실제 거동 |
| 가죽·충돌·두께 | 통제한 변수·물리적 기준·단면·불확실성 |
| 저장·출력 | 재열기 readback·고정 파일 해시·동일 등록 조건의 전후 측정 |

위 표는 향후 승인된 실습에서 확인할 목록이다. 이번 문서 작성으로 이 실습을 완료 처리하거나 새 앱 점유를 배정하지 않는다. [공통 작업 규칙](COMMON_WORK_RULES.md)의 원본 보존·실제 Guide 선행·단일 점유·독립 검수·보고 범위를 유지한다.

## 9. 교정한 오독과 학습의 한계

Edit Pattern 표본의 자동전사가 불명확한 부분은 원프레임의 영어 화면 자막과 외곽·내부선 선택을 대조했다. 같은 Delete Point 글자라도 선택된 점·앵커·핸들의 종류를 먼저 확인한다. 이동량을 절대 좌표로, Layer를 물리 층수로, PD를 곡선 정확도로, Thin을 완성 두께로 읽지 않는다.

이 문서는 자체 설명·일반 절차·공식 링크만 제공한다. 영상 원프레임·공식 본문 전문·앱 캡처·제품 원사진과 비공개 제작 데이터는 배포하지 않는다. 표본 사이 모든 키 입력·음성 의도·현지 MD9 기능 차이·전체 강좌·봉제/가죽/제품 실습은 미확인이다. [학습 근거](../reports/VideoLearning/20261106_MARVELOUS_BASIC_SAMPLED_STUDY.json)의 시점과 한계를 함께 인수한다.

## 10. 봉제·조립 한정 학습으로 이어가기

[봉제·조립 절차](MARVELOUS_SEWING_ASSEMBLY.md)는 Segment/Free/Reverse/M:N, 개방 경계·방향, 법선·Layer·배치/지지와 시뮬레이션, 표시/충돌과 실제 마감의 구분을 정리한다. [학습 근거](../reports/VideoLearning/20261106_MARVELOUS_SEWING_ASSEMBLY_STUDY.json)의 이번22표본시점은 기존9시점 재열람을 포함하고 새 영상 원자료는1편이다. 공식10본문도 기존6재열람·새4개다. 자막 패널은0행이어서 전체 자막을 이번에 읽었다고 세지 않는다. 전체 강좌 완주·native봉제/조립/수납 성공이 아니며 기존 입문 학습과 실제 제작 기록은 당시 범위대로 보존한다.
