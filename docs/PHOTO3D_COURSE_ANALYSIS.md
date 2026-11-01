# 3부. 강좌별 분석과 확인 근거

## 분석 범위

사진→3D 강좌 5편, 총 약 **101.5분**을 대상으로 영어 자막 전체를 읽고 주요 화면을 대조했다. 직접 검토한 표본은 **145시점·28개 시트**, 원본 해상도 추가 대조는 **7시점**이다. 자막의 중복 표시를 합친 설명 구간은 **2,742행**이다. 의미 분석은 자막과 표본 화면에 근거하며 모든 원본 프레임을 연속 시청했다는 뜻은 아니다.

로컬 Qwen3-VL 보조 분석은 10회·40개 표본 이미지에 사용했다. FrameLens는 전체 시간대를 폭 640픽셀·초당 1장으로 처리해 장면·움직임 지표를 얻는 보조 도구로 사용했다. 그 결과만으로 메뉴나 조작을 확인했다고 기록하지 않는다. 원문 자막·영상·표본과 도구 원출력은 프로젝트 내부 근거 폴더에 보관하고 매뉴얼에는 요약과 연결 링크를 싣는다.

여기서 “학습”은 제작 원리를 검토하고 다음 작업에서 재사용할 문서로 정리한 의미다. 모델 가중치 학습이나 실제 지갑 스캔·Blender 구현을 수행한 것은 아니다.

## P1. Meshroom → Blender 전체 흐름

[How to 3D Photoscan Easy and Free! — CG Geek](https://www.youtube.com/watch?v=k4NTf0hMjtY) · 34분 49초

나무 그루터기를 여러 방향에서 촬영해 Meshroom에서 복원한 뒤 OBJ를 Blender로 가져온다. 사진 선택·희소 점군·텍스처 메시를 거쳐 메시 축소, 재질·조명 후처리로 이어진다. 후반의 풀과 배경은 추가 자산이며 사진에서 모두 복원된 형상으로 해석하지 않는다.

| 다시 볼 구간 | 화면에서 확인한 것 | 지갑 작업에서 취할 점 |
| --- | --- | --- |
| [04:22](https://www.youtube.com/watch?v=k4NTf0hMjtY&t=262s)~07:30 | 휴대폰 설정, 사진 선택, Meshroom 입력 | 초점·반사·색의 일관성을 먼저 확보한다. |
| [12:00](https://www.youtube.com/watch?v=k4NTf0hMjtY&t=720s)~13:44 | 점군·카메라, 텍스처 메시, OBJ 가져오기 | 정렬 결과와 메시를 단계별로 검수한다. |
| [15:00](https://www.youtube.com/watch?v=k4NTf0hMjtY&t=900s) | Decimate 비율 0.5가 표시된 Blender 화면 | 숫자는 예시다. 얇은 가죽의 모서리·틈을 보존한다. |
| [19:30](https://www.youtube.com/watch?v=k4NTf0hMjtY&t=1170s)~22:30 | ColorRamp·Bump 등 후처리 | 사진색에서 만든 거칠기·요철을 측정 맵으로 부르지 않는다. |

**적용 판단:** 복원 전체 흐름 입문에 유용하다. 오래된 Blender UI와 그래픽 후처리 값은 그대로 복제하지 않는다. 사진을 키우면 없던 입체 세부가 생긴다는 해석도 채택하지 않는다.

## P2. RealityCapture 입문과 메시 검수

[Photogrammetry Beginner's Tutorial with Reality Capture — David Fletcher](https://www.youtube.com/watch?v=r5dJRac02j0) · 26분 05초

야외 건축물을 촬영하고 사진 정렬, 복원 영역, 메시 생성, 단순화, 텍스처, 내보내기를 보여 준다. 색을 입힌 결과가 형상 결함을 가릴 수 있다는 점이 지갑 작업에도 중요하다. 건물의 사진 수와 수백만 삼각형 목표를 제품 촬영 예산으로 옮기지 않는다.

| 다시 볼 구간 | 화면에서 확인한 것 | 지갑 작업에서 취할 점 |
| --- | --- | --- |
| [01:30](https://www.youtube.com/watch?v=r5dJRac02j0&t=90s)~07:30 | 전체와 세부를 연결하는 야외 촬영 | 전체→중간 거리→세부 사진의 연결을 만든다. |
| [13:14](https://www.youtube.com/watch?v=r5dJRac02j0&t=794s)~15:00 | 카메라·점군·복원 영역 | 영역 설정은 크기 보정과 구분한다. |
| [17:16](https://www.youtube.com/watch?v=r5dJRac02j0&t=1036s)~21:00 | 메시와 단순화·텍스처 작업 | 색을 끄고 실루엣·누락을 먼저 본다. |
| [22:30](https://www.youtube.com/watch?v=r5dJRac02j0&t=1350s) | 메시 내보내기 창 | 메시·재질·이미지를 함께 관리한다. |

**적용 판단:** 정렬부터 전달까지의 작업 순서를 참고한다. 촬영하지 않은 지붕과 뒷면처럼, 지갑의 가려진 내부도 사진색만으로 복원됐다고 판단하지 않는다. 후반 Sketchfab 게시 과정은 이번 작업 범위에 포함하지 않았다.

## P3. 앞뒤 스캔의 결합

[How to 3D Scan All Sides of Objects — William Faucher](https://www.youtube.com/watch?v=3mLBL7T-zgs) · 24분 33초

변형되지 않는 통나무를 뒤집어 촬영한 두 세트를 물체 마스크와 공통점으로 합친다. 배경과 받침을 제거하고 각 사진에서 같은 지점을 확인하는 과정이 핵심이다. 얕은 피사계 심도로 흐려진 부위 때문에 정렬이 어려워지는 사례도 설명한다.

| 다시 볼 구간 | 화면에서 확인한 것 | 지갑 작업에서 취할 점 |
| --- | --- | --- |
| [00:50](https://www.youtube.com/watch?v=3mLBL7T-zgs&t=50s)~03:46 | 변형되는 물체의 제한, 다중 높이 촬영 | 뒤집을 때 휘는 지갑은 자세별로 나눈다. |
| [06:24](https://www.youtube.com/watch?v=3mLBL7T-zgs&t=384s)~10:30 | 시험 메시 정리, 마스크 생성·불러오기 | 배경 대응을 제외하고 마스크 내용을 확인한다. |
| [12:07](https://www.youtube.com/watch?v=3mLBL7T-zgs&t=727s)~22:12 | 공통점 지정, 사진별 위치 확인 | 비슷한 악어무늬를 같은 위치로 오인하지 않는다. |
| [22:12](https://www.youtube.com/watch?v=3mLBL7T-zgs&t=1332s)~24:00 | 묶음 결합과 최종 결과 | 닫힌 메시와 실제 포켓 구조를 구분한다. |

**적용 판단:** 앞뒤 결합의 원리를 배우는 데 가장 직접적이다. 다만 영상에서 성공한 공통점 수나 당시 라이선스·요금 설명을 현재 작업의 보장 조건으로 쓰지 않는다.

## P4. 휴대폰 소형 물체 촬영

[How to 3D Scan Small & Detailed Objects — Polycam](https://www.youtube.com/watch?v=BImnzs-rR_k) · 3분 26초

화분 주변을 위아래로 이동하며 촬영하고 자동·수동 결과를 비교한다. 수동에서는 멈춰서 찍는 방식으로 흔들림을 줄인다. 색을 끈 회색 형상 비교도 보여 준다. 두 결과가 유사한 사례이므로 수동이 언제나 더 좋다는 결론으로 바꾸지 않는다.

| 다시 볼 구간 | 화면에서 확인한 것 | 지갑 작업에서 취할 점 |
| --- | --- | --- |
| [00:30](https://www.youtube.com/watch?v=BImnzs-rR_k&t=30s)~01:30 | 자동 촬영과 높이 변화 경로 | 이웃 사진 겹침과 한 바퀴의 연결을 확보한다. |
| [01:30](https://www.youtube.com/watch?v=BImnzs-rR_k&t=90s)~02:24 | 수동 촬영, 중간 사진 수 표시 | 이동 후 멈추고 초점·흔들림을 확인한다. |
| [02:30](https://www.youtube.com/watch?v=BImnzs-rR_k&t=150s)~03:00 | 텍스처 결과와 회색 메시 비교 | 검은 점처럼 보이는 무늬와 실제 요철을 나누어 본다. |

**적용 판단:** 촬영 동작을 짧게 익히기 좋다. “약 100장”은 화분 예시이며 지갑의 성공 기준이 아니다. 공식 문서의 Object Mode에는 메시와 Splat 선택이 있고 클라우드 처리가 포함된다. 이번에는 사용자 지갑 사진을 업로드하지 않았다. [Polycam 공식 설명](https://learn.poly.cam/hc/en-us/articles/27425185907348-How-to-Use-Object-Mode).

## P5. fSpy + Blender 사진 투사 모델링

[Create Realistic 3D Models from Photos Using Blender & FSpy — Alden Peters](https://www.youtube.com/watch?v=F7PDYoemJvM) · 12분 39초

골목 사진의 소실 방향을 맞춘 뒤 벽·문·차양을 직접 모델링하고, 경로에 두께를 주어 배관을 만든다. 카메라 기반 사진 투사와 UV Project 방식으로 외관을 옮긴다. 사진의 원근을 이용한 수동 제작이며 자동 표면 스캔과 구분한다.

| 다시 볼 구간 | 화면에서 확인한 것 | 지갑 작업에서 취할 점 |
| --- | --- | --- |
| [00:15](https://www.youtube.com/watch?v=F7PDYoemJvM&t=15s)~01:25 | 소실 방향·원점, Blender 카메라 | 직선과 알려진 길이가 유효한지 먼저 판단한다. |
| [01:25](https://www.youtube.com/watch?v=F7PDYoemJvM&t=85s)~07:35 | 면 생성, 돌출, 부품 분리 | 사진을 보며 구조를 직접 만드는 역할을 이해한다. |
| [07:35](https://www.youtube.com/watch?v=F7PDYoemJvM&t=455s)~09:59 | 경로에 두께를 주어 배관 제작 | 곡선 경로 원리는 봉제 경로 설계의 참고가 된다. |
| [10:50](https://www.youtube.com/watch?v=F7PDYoemJvM&t=650s)~11:35 | UV Project와 이미지 종횡비 | 투사 카메라 의존성과 다른 시점의 늘어짐을 확인한다. |

**적용 판단:** 사진 몇 장으로 기존 지갑의 시점과 패턴을 대조할 때 참고한다. 빛이 포함된 사진을 투사하거나 Bump로 연결한 결과를 실측 형상·독립 PBR 재질로 해석하지 않는다.

## 보조 영상 분석의 오류와 교정

Qwen3-VL은 후보 장면을 설명하는 보조 수단이었다. 여러 이미지를 한 번에 입력했을 때 다른 시점의 내용을 섞거나, 보이는 UI에서 조작 완료까지 추정하는 오류가 있었다. 아래는 원출력을 직접 화면·자막과 비교해 배제한 대표 사례다.

| 원출력의 문제 | 직접 확인한 근거 | 채택한 해석 |
| --- | --- | --- |
| P1 06:00의 노드 그래프가 비었다고 설명 | 화면에 기본 파이프라인 노드가 보임 | 사진 목록은 비어 있어도 노드 그래프는 존재한다. |
| P1 15:00에서 Decimate가 적용 완료됐다고 단정 | 원본 화면에 Apply 버튼과 비율 표시가 남아 있음 | 이 시점에서 확인한 것은 설정 화면이다. 실행 완료는 별도 시점과 구분한다. |
| P2 04:27·07:30을 복원 프로그램 장면으로 설명 | 해당 시점은 실제 건물 촬영 장면 | 타임스탬프와 이미지 설명이 섞인 결과를 폐기한다. |
| P3 01:30을 Lightroom, 04:30을 마스크 내보내기로 설명 | 01:30은 변형 물체 제한 표시, 04:30은 Lightroom 사진 목록 | 시점별 직접 화면을 기준으로 다시 기록한다. |
| P4 수동 촬영 화면을 3D 결과 미리보기로 설명 | 촬영 화면에 실제 바닥·발과 사진 수가 표시됨 | 오른쪽은 휴대폰의 촬영 화면이다. 결과 메시는 후반에서 확인한다. |
| P5 02:15의 형상을 단순 큐브로 설명 | 사진에 맞춰 만든 벽면과 카메라 시점이 보임 | 직접 모델링과 투사 단계로 해석한다. |

FrameLens의 장면 수는 편집 구간을 찾아보는 지표일 뿐 복원 성공률이나 지갑 형상 정확도가 아니다. 보조 모델이 읽었다고 한 파일명·미확인 수치·보이지 않는 클릭은 매뉴얼의 작업 지시 근거로 쓰지 않았다.

## 공식 문서 대조와 재사용 순서

강좌에서 변하지 않는 촬영·기하 원리를 추출하고, 버전 영향이 있는 설명은 다음 공식 문서로 대조했다. 문서 확인일은 2026년 11월 1일이다.

- [RealityScan 촬영](https://rshelp.capturingreality.com/en-US/tutorials/takingpictures.htm): 카메라 이동, 공통 표면, 작은 각도 변화와 연결 경로.
- [RealityScan 거리 보정](https://rshelp.capturingreality.com/en-US/tutorials/scaling.htm): 알려진 거리로 절대 스케일을 정하는 방법.
- [RealityScan 공통점](https://rshelp.capturingreality.com/en-US/tools/controlpoints.htm): 같은 위치 확인, 가중치와 독립 점검.
- [Meshroom 촬영](https://meshroom-manual.readthedocs.io/en/latest/capturing/capturing.html): 확산광·고정 초점거리·겹침·초점 확보.
- [Polycam Object Mode](https://learn.poly.cam/hc/en-us/articles/27425185907348-How-to-Use-Object-Mode): 촬영 모드, 겹침, 마스크와 결과 유형.
- [Polycam 기존 사진·영상 처리](https://learn.poly.cam/hc/en-us/articles/30549121659412-How-to-Create-Photogrammetry-and-Gaussian-splats-from-Existing-Images-and-Videos-on-Mobile-and-Web): 사진 입력과 메시·Splat의 구분.
- [fSpy 기본 원리](https://fspy.io/basics/), [설정 예제](https://fspy.io/tutorial/): 소실 방향과 기준 길이, 입력 사진의 한계.

처음에는 P4로 촬영 경로를 익히고, P1 또는 P2로 복원 흐름을 이해한다. 앞뒤 결합이 필요할 때 P3를 다시 본다. 사진 수가 부족한 경우 P5의 카메라 맞춤을 참고하되, 실측과 직접 모델링을 중심으로 진행한다.

최종 적용 원칙은 **실측과 구조는 모델에, 스캔은 검증 가능한 표면 참고에, 미세 가죽 결은 별도 재질 데이터에** 두는 것이다. 이번 작업에서는 새 지갑 모델·텍스처·렌더를 만들거나 외부에 게시하지 않았다.


세부 집계는 [공개 분석 범위](https://github.com/gnogus-ux/PuzzleIsland-Education/blob/main/reports/VideoLearning/20261101_PHOTO3D_COURSES_VERIFICATION.json), 공개 파일 해시는 [정본 파일 목록](https://github.com/gnogus-ux/PuzzleIsland-Education/blob/main/PUBLIC_MANIFEST.json)을 기준으로 한다.
