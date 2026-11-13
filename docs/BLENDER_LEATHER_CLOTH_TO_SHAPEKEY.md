# Blender 가죽판 Cloth → 정적 모양 키 절차

2026-11-13. 대상 환경 Blender 5.2.2 LTS, classic Cloth modifier. 실측 가죽 물성의 역산이나 시뮬레이션 성공 보장 문서가 아니다. 실제 작업마다 물리 길이와 장면 길이를 구분한다.

## 학습 근거와 범위

ego-browser로 공식 5.2 매뉴얼의 다음 네 페이지 본문을 직접 읽었다. 최초 latest 색인은 5.3으로 표시되어 본문 학습은 5.2 주소로 다시 했다. 검색 결과나 페이지 제목만으로 학습하지 않았다.

1. [Physical Properties](https://docs.blender.org/manual/en/5.2/physics/cloth/settings/physical_properties.html): stiffness/damping, angular/linear bending, internal springs, pressure 전체. 신장·압축·전단·굽힘은 별도 저항이며 큰 bending은 넓은 주름 경향이다. 가죽의 실측 영률 값으로 해석하지 않는다.
2. [Shape](https://docs.blender.org/manual/en/5.2/physics/cloth/settings/shape.html): pin group, sewing, shrinking, dynamic mesh, rest shape key 전체. 핀 가중치로 고정을 조절한다. Dynamic Mesh는 매 프레임 rest shape를 바꾸며 Rest Shape Key와 배타적이다. 이미 들뜬 모양을 자연 rest로 잘못 지정하지 않는다.
3. [Collisions](https://docs.blender.org/manual/en/5.2/physics/cloth/settings/collisions.html): object/self collision, collection, quality/distance, troubleshooting 전체. 충돌 물체에도 Collision이 필요하다. 큰 distance는 공중에 뜬 둥근 외형을 만들 수 있어 무조건 늘리지 않는다. 품질/반복과 초기 교차를 먼저 확인한다.
4. [Cache](https://docs.blender.org/manual/en/5.2/physics/cloth/settings/cache.html): bake와 재설정, preview/render subdivision 일치, cached edit 제한 전체. 캐시 직접 편집은 현재 동작하지 않는다는 주석이 있다. Collisions 문서의 사후 편집 설명과 구별하여, 평가 메시를 별도 정적 모양 키로 복사한다.

보조: 공용 external/blender-skills의 blender-simulation 문서, 설치된 Blender 5.2의 `scripts/presets/cloth/leather.py`를 직접 읽었다. 설치 프리셋은 quality15, mass0.4, tension/compression/shear80, bending150, 관련 damping25, air1, pressure/internal springs off다. 프리셋은 시작점이며 메시 크기·밀도별 보정이 필요하다. 5.2 실제 RNA 지원·설정 반영은 각 작업의 실행 로그로 따로 검증한다.

## 실행 절차

1. 원본 해시와 별도 Guide를 먼저 만든다. 수정 영역·봉제 고정선·절개 자유단·이웃 접합부·목표 상승을 표시한다. 실제 카드 높이와 두께의 합을 구분한다. 충돌체 자체가 목표보다 높으면 cloth 수치만으로 목표를 만족시킬 수 없다.
2. 물리 mm↔장면 BU 환산, fps, gravity, quality, 프레임 범위를 기록한다. 10배 장면이면 실물1mm=0.01BU다. 일반 의상용 충돌값을 mm 가죽판에 그대로 복사하지 않는다. 크기 변경이 물리적 동등성을 자동 보장하지 않는다.
3. 시뮬레이션용 단일 표면을 분리한다. 폐곡면의 상하 양면을 별개 천으로 중복 계산하지 않는다. 슬롯 절개·끝 펀칭을 막지 않는다. 매우 가늘거나 면적0인 삼각형, 중복 정점, 불균일 밀도를 검사한다. 프록시를 쓰면 원본 대응과 보간 오차를 기록한다.
4. 둘레 봉제선에 pin group=1을 지정하고 자유단과 구분한다. 카드 A/B/C는 강체 형상의 Collision 메시다. 해당 충돌체만 모은 Collection을 Cloth collision collection에 지정한다. 필요한 받침/안감의 역할도 구분한다.
5. Leather 프리셋에서 시작해 늘어남과 과한 접힘을 억제한다. 충돌 없는 초기 상태 또는 점진적인 충돌체 진입으로 시작한다. 프레임을 순서대로 계산하고, 안정 프레임의 최대 이동·핀 이동·침투·높이를 측정한다. 큰 margin으로 떠 있는 결과를 성공 처리하지 않는다.
6. 안정된 평가 좌표를 원본과 같은 정점 순서의 모양 키에 저장한다. 두께 복원·접촉부 보정·접합부 전달은 시뮬레이션 원본과 구별해 기록한다. 시뮬레이션을 대체하는 넓은 수동 받침대 보정을 넣지 않는다. 다른 리그 상태의 보정과 합산/덮어쓰기 관계를 검사한다.
7. 키는 승인된 상태에서만 활성화한다. 빈 상태와 봉제선 좌표를 해시/허용오차로 대조하고, 카드 교차를 실제 평가 메시로 검사한다. 저장 후 새 프로세스로 열어 키와 검사 결과를 확인한다. 최종 렌더는 캐시 재생에 의존하지 않는다.
8. 같은 카메라·조명으로 전후 렌더/solid/wire와 실물 사진을 비교한다. 최대 상승은 원래 표면과 같은 대응점의 차이로 실물 mm 단위로 쓴다. 수치 통과·시각 통과·제작자 확인·독립 검수를 구분한다.

## 제한과 재시도

시뮬레이션 실행 전 원리 학습과 실제 안정화 성공을 구분한다. 같은 방법으로 두 번 실패하면 시도별 설정·최대 상승·교차·핀 이동·최신 후보를 보존하고 PARTIAL로 보고한다. 캐시를 무한 재실행하거나 실패를 숨겨 성공한 프레임만 고르지 않는다. 운영 도구·기존 사용자 장면을 임의 변경하지 않는다.

2026-11-13 제한 실기: Blender 5.2.2 background에서 단일 표면 Cloth + 세 고정 Collision 메시 + 둘레 pin을 100프레임 순차 계산하고 평가 결과를 정적 shape key로 복사했다. 핀 이동 0과 캡처는 확인했으나 안정화·높이·교차 조건은 실패했다. 따라서 이 절차의 설정 예제가 제품 완성에 성공했다고 보지 않는다. 고정 충돌체가 목표 높이보다 높은 경우, 물성 조절 전에 접촉면의 기하학적 최소 높이를 계산해야 한다. 해가 없는 조건에 같은 계산을 두 번 채우기 위해 반복하지 않는다.
