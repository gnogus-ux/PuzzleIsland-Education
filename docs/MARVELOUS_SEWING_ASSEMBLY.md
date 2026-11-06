# Marvelous Designer 봉제·조립 — 방향·입구·배치·검증

2026-11-06의 한정 학습을 일반 실습 절차로 정리했다. 공식 봉제·배치 영상 **2편의22표본시점**을 확인했으며 새 영상 원자료는1편이다. 기존 봉제 영상의13시점 중9시점은 이전 명세와 겹친다. 공식 문서10개 본문도 기존6개 재열람·새4개로 구분한다. 전체 강좌 완주·오디오·연속 재생·전체 자막·MD9 native 봉제/조립/수납 실습 완료가 아니다. [학습 범위·시점·출처](../reports/VideoLearning/20261106_MARVELOUS_SEWING_ASSEMBLY_STUDY.json)를 함께 읽는다.

먼저 [입문 도구](MARVELOUS_BASIC_PATTERN_EDITING.md)와 [재단·봉제 workflow](MARVELOUS_WALLET_PATTERN_WORKFLOW.md)를 읽고 대상의 실제 Guide와 연결표를 인수한다. 이 문서는 새 실행 배정이나 제품 합격 판정이 아니며, 다른 제작 담당의 성과를 교육 실습으로 세지 않는다.

## 1. 연결 수와 개방 경계를 먼저 기록한다

실제 부품과 승인 Guide에서 연결 상대를 정한다. 보이지 않는 안감·보강재·칸막이를 학습 예제로 새로 추가하지 않는다. 예를 들어 여덟 패턴을 사용하는 사례라도 판 수·구간 수·논리 연결 수·입구 수·수납 용량은 서로 다른 수다. 판 수나 가능한 조합에서 봉제 개수를 역산하지 않는다.

| 관계표 필드 | 실제 인수할 내용 |
|---|---|
| 논리 연결 ID | 설계상 의도한 연결 하나 |
| 양쪽 대상 | 판 ID·경계 ID·구간 순서·시작/끝 랜드마크 |
| 방향 | 양쪽 진행 방향과 대응 시작점 |
| 길이 | 양쪽 경로 길이·합계·차이·설계 여유의 근거 |
| 연결 제외 | 포켓 입구·통과 홀·자유 굽힘 등의 개방 범위 |
| native 증거 | 선택 범위·실제 봉제 관계·저장·재열기 확인 |
| 판정 | 생성·자체 확인·독립 QA·미검증 구분 |

빈 표는 교육용 양식이다. 실제 상대와 경계를 채우기 전에는 완성된 연결표나 제품 Guide로 취급하지 않는다. 닫힌 홀의 윤곽과 봉합해도 되는 경계를 혼동하지 않고, 겹친 입구를 가로막는 연결이나 입구 전체를 뒷판에 봉제하는 관계를 만들지 않는다.

## 2. Segment와 Free Sewing을 연결 범위에 맞춰 검토한다

[Segment Sewing](https://support.marvelousdesigner.com/hc/en-us/articles/47358199517209-Segment-Sewing-2D)은 구간 단위의 대응이다. 첫 구간과 상대 구간의 선택 범위·시작점·방향 표시를 함께 확인한다. directional notches가 교차하면 잘못 뒤집힌 연결이 생길 수 있으므로 시뮬레이션 전에 관계를 점검한다.

[Free Sewing](https://support.marvelousdesigner.com/hc/en-us/articles/47358239854361-Free-Sewing-2D)은 경계의 시작/끝을 정하는 부분 연결이다. 필요한 부분만 연결하는 경우 전체 구간 선택과 구별한다. 길이 안내와 반대쪽 진행 방향을 보고 입구가 선택 범위에 포함되지 않는지 확인한다. 생성 도중 길이 입력과 정지 상태의 좌표 입력은 다른 동작이다.

문서의 길이 차이 경고는 프로그램 안내다. 작은 제품의 허용 공차나 설계 여유로 복사하지 않는다. 길이가 다르면 올바른 경계인지와 의도한 여유부터 확인하고, 숫자를 맞추려고 재단 외곽·포켓 깊이·입구를 임의 변경하지 않는다.

## 3. 방향 수정과 봉제선 길이 편집을 구분한다

[Reverse Sewing](https://support.marvelousdesigner.com/hc/en-us/articles/47358393261593-Reverse-Sewing)은 Edit Sewing으로 실제 봉제 관계를 선택한 뒤 방향을 바꾸는 명령이다. 시연160초의 메뉴와 공식 본문을 대조했다. 이는 판의 앞뒤 법선을 바꾸는 동작이 아니다. 출처의 단축키는 현지 설정을 확인한 뒤 사용하고 메뉴 이름·선택 대상을 먼저 확인한다.

[Edit Sewing Line Length](https://support.marvelousdesigner.com/hc/en-us/articles/47358392328857-Edit-Sewing-Line-Length)는 봉제선 끝의 이동과 길이 편집을 다룬다. 이동 중 수치창을 정지 상태의 절대좌표 입력으로 해석하지 않는다. 봉제 관계의 길이를 바꾸는 것과 재단 외곽을 바꾸는 것을 구분하고, 변경 전후 양쪽 경로·시작점·개방 범위를 기록한다. 자동화가 이동 도중 입력을 지원하는지도 별도 확인 사항이다.

## 4. M:N은 그룹의 순서·길이·대응을 검증한다

[M:N Segment Sewing](https://support.marvelousdesigner.com/hc/en-us/articles/47358238742553-M-N-Segment-Sewing-2D)의 절차는 한쪽 구간들을 선택해 Enter로 확정하고 다른쪽 구간들을 선택해 다시 확정하는 방식이다. 각 그룹의 실제 구간 수·순서·총길이·진행 방향을 남긴다. 길이 차이에 따른 비례 분배가 설계 랜드마크까지 보존한다는 보증은 아니다.

생성 도중 Delete로 마지막 선택을 취소하는 것과 Esc로 현재 생성을 취소하는 것을 완료된 관계 편집과 구분한다. 다른 도구에서 같은 키를 누르는 것으로 대신하지 않는다. 거부된 구간을 반복 클릭하거나 이미 완성된 관계를 다시 생성해 중복 연결하지 않는다. 기존 관계와 연결표를 대조하고 오류 관계만 좁게 수정한다.

## 5. 배치·법선·Layer와 실제 재료 구조를 분리한다

[Basic Pattern Arrangement 시연](https://www.youtube.com/watch?v=eAOYYgn5RK0)은 2D 재단과3D 배치·회전이 다른 작업임을 보여주는 표본 근거다. 의류의 인체 배치점·곡면화·치수를 작은 제품의 조립 좌표로 복사하지 않는다. 실제 Guide에서 기준 평면·좌우축·앞뒤·중력축·초기 간격·지지/고정 조건을 확인한다.

[Flip Normal](https://support.marvelousdesigner.com/hc/en-us/articles/47358334132633-Flip-Normal) 전후에는 앞뒤와 Fold Angle 등 영향을 받는 값을 함께 확인한다. 잘못된 봉제 방향을 숨기기 위해 판 전체의 법선을 일괄 반전하지 않는다.

[Layer](https://support.marvelousdesigner.com/hc/en-us/articles/47358288780441-Use-Layer-Drape-Additional-Garment)는 겹침 순서를 돕는 시뮬레이션 설정이다. 물리적 가죽층 수·두께·접착이나 영구적인 포켓 번호가 아니다. 필요한 배치 후 중립 Layer에서 유지되는지도 실제 후보에서 확인한다. 현재 설계에 없는 재료를 Layer 값에 맞춰 추가하지 않는다.

## 6. Simulation은 영향 범위와 지지를 확인한 뒤 시험한다

[Simulation](https://support.marvelousdesigner.com/hc/en-us/articles/47358232630937-Simulation)은 중력과3D 의상 거동을 다룬다. 판을 선택했다는 사실만으로 선택한 포켓군만 계산된다고 가정하지 않는다. 영향을 받는 전체 판·기준 지지·초기 관통·안정된 저장 checkpoint를 먼저 확인한다.

후속 승인 실습에서는 한 연결 또는 포켓군부터 확인하고 추가한다. 모든 판을 이어 발산한 뒤 외곽·물성·두께를 동시에 바꾸지 않는다. Normal/Stable/Fitting 등의 이름은 문서 목적과 현지 메뉴를 함께 보며, Fitting이라는 이름으로 실물 가죽 검증을 완료 처리하지 않는다.

| 문제 | 먼저 확인할 것 |
|---|---|
| 판이 뒤집히며 당겨짐 | 상대 경계·시작점·방향 표시·법선의 구분 |
| 입구가 막힘 | 입구를 가로지른 오봉제·중복 관계·뒷판 연결 범위 |
| 모든 판이 떨어짐 | 중력축·기준 지지/고정·초기 배치 |
| 겹이 붕 뜸 | 충돌 간격·초기 겹침·Layer·법선·표시 두께 |
| 관통·발산 | 방향·배치·물성·메시 조건을 원인별로 분리 |
| 정지 호출이 미확인 | 기존 호출·사용자 작업 보존, 중복 입력·강제 종료 금지 |

마지막 안정 후보를 보존하고 정지 반환·저장 상태를 확인한다. 파일 저장, 앱 응답, 진행 호출 종료와 정상 점유 해제는 별도 증거로 기록한다. 이 학습에서는 실제 시뮬레이션을 수행하지 않았다.

### 6.1 임시 지지 기능과 복귀를 구분한다

임시 지지 기능은 계산·충돌·구속 범위가 다르다. 실제 Guide와 시험 범위에서 대상을 확인한다.

| 기능·공식 출처 | 문헌에서 확인한 효과 | 복귀·주의 |
|---|---|---|
| 선택·[표시/숨김](https://support.marvelousdesigner.com/hc/en-us/articles/47358200025497-3D-Window-Display-Icons) | 편집 대상·보이는 상태를 지정 | 선택·숨김만으로 계산·충돌·Pin이 제외된다고 하지 않음 |
| [Freeze](https://support.marvelousdesigner.com/hc/en-us/articles/47358315135897-Freeze-Unfreeze) | 판을 고정하되 충돌체로 유지 | Unfreeze. 다른 판에 미치는 충돌 영향도 확인 |
| [Deactivate: Pattern Only](https://support.marvelousdesigner.com/hc/en-us/articles/47358262829849-Deactivate-Pattern-Only-Activate) | 판을 계산·충돌에서 제외 | Activate. 연결 Sewing까지 같은 방식으로 제외된다고 보장하지 않음 |
| [Deactivate: Pattern & Sewing](https://support.marvelousdesigner.com/hc/en-us/articles/47358273409945-Deactivate-Pattern-Sewing-Activate) | 판과 연결 Sewing Lines를 비활성화 | Activate 후 실제 대상 봉제선의 복귀도 확인 |
| [Create Pin](https://support.marvelousdesigner.com/hc/en-us/articles/47358422800537-Create-Pin)·[Pins](https://support.marvelousdesigner.com/hc/en-us/articles/47358146159769-Pins) | 선택 메시 정점·영역을 고정 | 기존 사용자 Pin을 보존하고 자기 시험 Pin의 선택·삭제 범위를 확인 |
| [Attach/Detach Pin](https://support.marvelousdesigner.com/hc/en-us/articles/47358452805913-Attach-Pin-to-Detach-Pin-from-Avatar) | Pin을 가장 가까운 Avatar 부분에 부착 | Detach는 부착 해제이며 Pin 삭제와 별도 |
| [Strengthen](https://support.marvelousdesigner.com/hc/en-us/articles/47358253657497-Strengthen-Unstrengthen) | 판의 강성을 임시 강화 | Unstrengthen. 측정 물성·강체 고정으로 해석하지 않음 |
| [Solidify](https://support.marvelousdesigner.com/hc/en-us/articles/47358310357529-Solidify) | Strength에 따라 현재 drape 형상을 유지 | 읽은 본문에 확정 OFF/해제법 없음. 현지 해제 확인 전 기본 시험 수단으로 채택하지 않음 |

판별 기준 상태·시험 상태·연결 봉제 활성·Pin/부착·복귀 확인을 장부에 남긴다. 재활성화 뒤 판·봉제·배치·개방 경계와 임시 구속/강성 잔여를 대조하며, 기준부터 있던 상태를 일괄 해제하지 않는다. 고정 지지체나 임시 강성 아래 얻은 결과는 자유 가죽의 전체 조립·수납 적합을 증명하지 않는다. 이 설명은 특정 판에 적용할 지지 방법·새 물성/충돌값을 정하지 않는다.

일반 Project 저장 설명만으로 이 상태들이 MD9에서 저장·재열기 후 유지된다고 보장하지 않는다. 같은 파일 재열기 뒤 판·봉제 활성·Pin/부착·형상·배치를 실제 readback한다. [OBJ 문서](https://support.marvelousdesigner.com/hc/en-us/articles/47358223288601-3D-File-OBJ-Import-Export)의 선택·Thin/Thick·Weld 옵션도 상태별 자동 포함/제외나 플래그 보존 규칙의 증거가 아니다. 실제 export 선택·옵션·객체/그룹 수·경계·좌표·단위로 범위를 대조하고, OBJ 재가져오기로 임시 상태가 복원된다고 하지 않는다. 이번 보강은 문헌 준비이며 이 저장·출력·해제 동작의 MD9 실기 검증은 미실행이다.

## 7. 표시·충돌·완성 단면은 다른 측정이다

[Collision Thickness](https://support.marvelousdesigner.com/hc/en-us/articles/47358430412441-FABRIC-PHYSICAL-PROPERTIES-Adjust-Collision-Thickness)는 충돌 간격, [Rendering Thickness](https://support.marvelousdesigner.com/hc/en-us/articles/47358450148761-FABRIC-PHYSICAL-PROPERTIES-Adjust-Rendering-Thickness)는 보이는 두께로 나누어 읽는다. 충돌 문서의 일부 Operation 표현은 제목·목적·위치와 Rendering 문서를 대조해 구별했다.

두께 장부는 아래 항목을 분리한다. 각 항목의 대상 부품/Fabric·단위·설정값 또는 실측값·출처·미확인을 함께 기록한다. 예제 기본값은 제품 추천 수치가 아니다.

| 장부 항목 | 구별할 범위 |
|---|---|
| 실물 가죽 t | 실제 재료 두께·피할 상태. 보강재·접착은 확인된 별도 재료로 기록 |
| Fabric Thickness | Fabric 단위 표시 두께. 실물 t의 측정값이 아님 |
| Add'l Thickness-Rendering | Pattern별 추가 표시 두께. 임의 합계를 완성 단면으로 보고하지 않음 |
| Add'l Thickness-Collision | Pattern별 충돌 간격. 표시 두께·재료층 수와 다름 |
| 상대 물체 offset | 상대측 설정과 실제 native 대상 유형을 확인. 판측 값만으로 접촉을 설명하지 않음 |

legacy 표면 간 거리도 이 장부의 실물 두께나 충돌값으로 대체하지 않는다. Collision 문서 Operation의 `rendering` 표현은 제목·목적·위치가 Collision인 사실과 별도로 대조한다. 표시를 바꾼 것만으로 물리 간격·완성 단면이 검증된 것은 아니며 실제 형상은 Guide와 전후 단면으로 확인한다.

Thin 출력은 완성 두께의 직접 계측 자료가 아니다. 별도 단면·출력 조건이 필요하다. 이번 학습은 새 가죽 물성·절대 두께·허용 공차·봉제 개수를 정하지 않았다.

### 7.1 프리셋·미측정 물성과 시험 기준을 인수한다

[Preset](https://support.marvelousdesigner.com/hc/en-us/articles/47358440962713-FABRIC-PHYSICAL-PROPERTIES-Physical-Property-Preset)은 물성 묶음이며 실측 인증서가 아니다. 확인된 정확한 이름·앱 버전·Fabric 배정·변경 전 상수/단위·변경분을 인수한다. 문서에서 확인되지 않은 MD9 가죽 프리셋 이름이나 값을 만들지 않고 저장값을 모르면 미확인으로 남긴다. [Detail Setting](https://support.marvelousdesigner.com/hc/en-us/articles/47358427696025-FABRIC-PHYSICAL-PROPERTIES-Physical-Property-Detail-Setting)의 slider 단계와 constant 입력도 같은 숫자 체계나 실물 재료 상수 측정으로 해석하지 않는다.

방향별 굽힘 저항과 [신장·전단](https://support.marvelousdesigner.com/hc/en-us/articles/47358420149017-FABRIC-PHYSICAL-PROPERTIES-Adjust-Stretch-Weft-Warp-Shear)은 목적이 다르다. [Friction](https://support.marvelousdesigner.com/hc/en-us/articles/47358444242457-FABRIC-PHYSICAL-PROPERTIES-Adjust-Friction-Coefficient)의 garment–garment 설명은 카드가 Avatar 등 다른 충돌 대상일 때의 마찰·인출 거동까지 검증하지 않는다. [Pressure](https://support.marvelousdesigner.com/hc/en-us/articles/47358312998809-Express-Air-Pressure)는 공기·패딩 효과용으로, 목표 부풀음 높이와 같은 숫자를 넣는 항목이 아니다. [Gravity·solver 조건](https://support.marvelousdesigner.com/hc/en-us/articles/47358125463321-Simulation-Properties)은 장면 기준으로 기록하며 현행 옵션 전체를 MD9 지원 목록으로 소급하지 않는다.

시험은 기존 승인 재단·물성·설정을 보존한 별도 기준 사본에서 배치·봉제 방향·개방·초기 관통을 먼저 확인한다. 한 변수군씩 바꾸고 두께 장부·지지/중력·Layer·PD·전후값·단면/관통·저장·재열기 유지를 남긴다. 충돌을0/음수로 만들거나 중력 제거·임의 신장으로 fit을 맞추지 않는다. 실제 삽입·인출·간섭·닫힘과 독립 QA는 별도 후속 시험이며 이번 문헌 준비가 이를 완료하지 않는다.

## 8. 버전 제한과 후속 실기 기록

| 출처 | MD9에서 남길 제한 |
|---|---|
| 두 영상의9.5 표기·봉제 영상의MD9 설명 | 정확 build와 모든 메뉴 호환을 새로 인증한 것은 아님 |
| 2024.1 Layer 표시 | 구버전 실습의 필수 표시 조건으로 요구하지 않음 |
| 2024.1 Density→Weight 명칭·단위 설명 | 현행 gsm 표기를 MD9의 실제 필드·단위로 자동 대입하지 않음 |
| 2024.2 CPU/GPU 충돌 일치·옵션 | MD9에서 같은 결과를 보장하지 않음 |
| 2025.2 즉시 정지 개선 | MD9의 정지·응답 동작에 소급하지 않음 |
| 2026.1 충돌 방향 개선 | MD9에서 개선이 적용됐다고 하지 않음 |
| Pin 대칭복사2024.2·전체선택2025.2 / 상태색2024.1 / OBJ Weld Turned2026.0 | 후대 설명을 MD9 절차·호환 인증에 소급하지 않음. 역사적 도입 표기만으로 MD9 지원도 확정하지 않음 |

실기 담당은 봉제 생성, 방향·개방 자체 확인, 안정된 조립, 저장·동일 파일 재열기, 수납·간섭·닫힘, 마감·독립 QA를 각각 기록한다. 판 Name·홀·개방 경계·관계 수·방향·물성·메시 조건의 유지와 동일 등록 조건의 출력을 확인한다. 실제 연결표가 없으면 임의 봉제 수를 확정하지 않는다. 교육 설명이나 시연의3D 연결 표시만으로 제품 PASS를 선언하지 않는다.

원본·사용자 작업·기존 실/구멍·승인 범위를 보존하고 [공통 규칙](COMMON_WORK_RULES.md)의 Guide 선행·단일 점유·정상 종료·독립 검수 절차를 적용한다. 이 문서는 후속 실습의 참고이며 현재 제작 담당에게 중복 실행을 배정하지 않는다.

## 9. 실제 열람 범위

[봉제 시연](https://www.youtube.com/watch?v=bZR8j70mA0Q)의 요청시점은50/60/75/90/105/125/140/160/180/200/225/245/270초다. 첫50초 요청의 실제 캡처는50.04864초이며 나머지 범위도 표본 확인이다.270초는 마무리 로고여서 실습 동작을 관찰한 시점으로 확대하지 않는다. 기존 명세와 겹친9시점과 추가 요청4시점을 분리한다.

새 배치 시연은19/49/76/143/186/212/275/297/330초를 확인했다.76/212초의 화면 영어 자막2시점은 읽었지만 전체 자막 패널은 본문0행을 반환했다. 봉제 영상도 이번 패널에서 본문0행이어서 전체 자막을 새로 읽었다고 세지 않는다. 과거 전체 자동자막 검토는 [이전 학습 기록](../reports/VideoLearning/20261105_MARVELOUS_WALLET_VIDEO_STUDY.json)의 당시 범위로 유지한다.

영상 사이 모든 프레임·오디오·연속 재생·강좌 전과정·native 봉제/조립/수납은 미확인이다. 공개 자료는 자체 절차·정상 공식 링크·열람 메타데이터뿐이며 사용자 사진·앱 캡처·영상 원프레임·자막/공식본문 전문·비공개 인계자료는 배포하지 않는다. [이번 학습 근거](../reports/VideoLearning/20261106_MARVELOUS_SEWING_ASSEMBLY_STUDY.json)의 중복 집계와 버전 한계를 함께 인수한다.

2026-11-06 별도 물성 준비 보강은 **공식12개 유효 본문=기존5개 재열람+이번7개 보강**이다. 기능 본문이 부족한 Overview1개는 제외했고 새 영상·오디오·자막·전체 강좌·실기/설정은0이다. 보강7개 중 기존 workflow가 이미 인용한 출처도 있어 자료실 전체에 처음 추가된7출처라고 세지 않는다. [단계별 학습 기록](../reports/VideoLearning/20261106_MARVELOUS_SEWING_ASSEMBLY_STUDY.json)에 이전22표본/10본문을 그대로 두고 이 준비의 출처·한계·MD9 미검증을 구분했다.

2026-11-06 별도 지지 기능 준비는 **공식10페이지의 필요한 본문**을 읽었다. OBJ는 기존 출처 재열람이며 Create Pin/Pins/Attach 본문의 겹침을 독립 신규 강좌로 세지 않는다. 새 영상·오디오·자막·전체 강좌·앱 실기는0이다. 게시 단계의 같은 출처 교차 확인도 신규10자료 학습으로 더하지 않는다. [단계별 학습 기록](../reports/VideoLearning/20261106_MARVELOUS_SEWING_ASSEMBLY_STUDY.json)에 이전 집계와 이 보강의 MD9 미검증 범위를 분리했다.
