# 매치3 · 원 자료 구현 비교와 읽는 법

[통합 매뉴얼](MATCH3_WORKFLOW.md) · [회차별 세부 근거](MATCH3_TAFT_EPISODES.md). 아래는 실제 자료 관찰, 코드 추론과 보완 제안을 구별한 교육 기록이다. 강좌 코드를 프로젝트에 편입하거나 Unity에서 재현하지 않았다.

## Mister Taft Creates · 점진 제작과 후속 정정

[Unity/C# 플레이리스트](https://www.youtube.com/playlist?list=PL4vbr3u7UKWrxEz75MqmTDd899cYAvQ_B)의 실제 65개 항목을 순서대로 학습했다. 2017/2018 Unity 화면·세로 예제다. 기본 Board/각 Dot의 참조와 플래그, coroutine 지연을 바탕으로 기능을 확장하므로 중간편을 최종 코드로 읽지 않는 것이 핵심이다.

| 단계 | 주요 관찰 | 연결해 읽을 후속편 |
|---|---|---|
| Part 0~8 | 아트·보드·스와이프·매치·무효 복귀 | P9~13 배열 빈칸/낙하/입력 해제 |
| 9~15.1 | 제거·nullCount 낙하·리필·연쇄·연출 | P34·50에서 지연/경합 보완 |
| 16~24 | 행/열·색·인접 폭탄과 4/5/T/L 추정 | P21 인덱스/리스트 정정, P34 null, P35 연쇄, P48·50 생성색 |
| 25~32 | 카메라·마스크·젤리·교착·셔플·힌트·리소스 교체 | P30 폭/높이 정정, P52.1 합법 교환/장애물 경로 |
| 33~42 | 점수/배수·바·음향·전환·목표·수/시간·승패 | P36 float, P41 counter0, P42 pause/종료 |
| 43~47·Android | SO 레벨·씬·버튼·진행 파일·해금 | P45 수집값 초기화, P47 Create/Awake/별 refresh |
| 48~53 | 패턴색·애니·해결 루프·lock/concrete/slime | P50 yield break, P52.1 낙하·리필·셔플, P54 폭탄 피해 |
| 54~58 | pause·옵션·시작화면·별·레벨 페이지 | 종료 상태·저장 경계·씬 UI 수명은 별도 검증 |

확인한 정정에는 P8의 좌표 복사 오기, P17의 행 인덱스, P21의 생성 중 리스트 감소, P30의 `j<width`→height, P36의 정수 나눗셈, P41의 이동0 판정, P47의 최초 파일 생성, P52.1의 장애물 제외 누락이 있다. 잔여 위험에는 전역 매치 총수로 특수 분류, 힌트/교환 제약 차이, 재귀 폭탄 순환, 고정 지연의 완료 추정, 열 폭탄 width/height, Slime 경계/증식 반복이 있다. ‘고쳤다’는 시연과 ‘모든 조합이 안전하다’는 주장을 구별한다.

애니메이션 clip을 만드는 동안 보이는 오류·빈 메서드·입력 중 자동완성은 최종 구현으로 전사하지 않았다. 상세 근거는 각 편의 원본 확인 시각과 후속 자막/시연을 나눠 기록했다. 예제의 외부 사탕·GUI·음악은 다운로드/재배포하지 않았다. 당시 ‘무료’ 발화를 현재 가격·권리 확인으로 취급하지 않는다.

## Catlike Coding · 논리와 skin의 단계 계약

Jasper Flick의 [Match 3](https://catlikecoding.com/unity/tutorials/prototypes/match-3/)은 Unity 2022.3.2f1로 작성한 글이다. 본문 시작부터 끝, 코드 설명과 FAQ를 읽었다. 다음은 독립적인 비교·해설이며 원문 번역본이나 코드 모음이 아니다.

| 원문의 구성 | 확인한 구현 | 적용 시 판단 |
|---|---|---|
| Game/Match3Skin/Match3Game | 입력과 진행을 skin에서 조정하고 game에 판정 상태 | 논리도 MonoBehaviour/Unity Random에 의존하므로 엔진 독립과는 구별 |
| Grid2D | 직렬화를 위해 1차원 배열, y×width+x, 인덱서·Swap | 경계 검사·활성 topology·빈칸 계약 추가 필요 |
| TileState/FillGrid | None+7종, 기본8×8, 왼쪽/아래 두 칸 종류를 피함 | 초기 가능한 수를 별도 탐색, 잘못된 정의 재시도 상한 필요 |
| Move/TryMove | 실제 데이터 교환→매치 검사→실패 시 원복 | 화면 ping-pong 동안도 Busy, 외부 명령 검증 경계 명시 |
| FindMatches/ProcessMatches | 행/열 run 기록·None 표시로 고유 제거 | 교차 run 점수와 고유 제거 수는 다른 정책 |
| DropTiles | holeCount로 압축·상단 보충·TileDrop 기록 | 마스크 구간/장애물은 구현하지 않음 |
| TileSwapper/Disappear/Fall | Lerp·sin 깊이, 축소/pool, 거리/속도·최장 busy | 취소/씬 종료/표현 실패 복구를 별도 검증 |
| 점수 표시 | run마다 점수와 multiplier 증가, TMP/pool | 파동당 동일 배수 또는 고유 제거 점수라고 오독하지 않음 |
| Move.FindMove/AutoPlay | 처음 발견한 수를 사용 | 최적 전략·레벨 밸런스 QA가 아님 |
| 교착 | 초기에는 가능한 수가 생길 때까지 재생성, 안정판은 게임 종료 | 보존 셔플 구현으로 부르지 않음 |

pool의 Editor 리로드 관련 설명도 읽었다. Domain Reload를 끈 뒤 파괴 참조가 남으면 pool을 비우고, hot reload로 pool 참조를 잃었을 때 활성 인스턴스를 Destroy한다. 이미 비활성화한 인스턴스가 누적될 수 있다는 원문 한계도 보존한다. 이를 무제한 안전한 pool로 소개하지 않는다.

FAQ는 Unity의 다차원 배열 직렬화 제약, tuple swap, readonly struct, NeedsFilling, 진행 단계의 겹침을 설명한다. private setter가 있는 List도 내용은 외부에서 바꿀 수 있다. 소비자에게 읽기 전용 결과를 주려면 별도 보호가 필요하다.

가능 수 탐색의 `c.y>1`/`c.x>1` 인근 경계 분기는 추가 검증 후보로 기록했다. 이 문서 작업에서 실제 누락을 실행 입증하지 않았으므로 확정 버그로 부르지 않는다. 모든 합법 인접 교환을 시험하는 단순 oracle과 가장자리 fixture로 대조하는 것이 보완안이다.

원문의 [라이선스 페이지](https://catlikecoding.com/unity/tutorials/license/)는 코드/제공 에셋 MIT-0와 강좌 본문·스크린샷·도식 CC BY-NC-SA 4.0을 구별한다. 이 문서에는 원문 본문·스크린샷·전체 코드를 복제하지 않았다. 출처와 해설을 구별하며, 외부 자료의 권리를 이 저장소의 일괄 권리로 바꾸지 않는다.

## Winterbolt Games · UI와 연결 덩어리 규칙

[Creating a Match 3 Game in Unity](https://www.youtube.com/watch?v=9i_sktmLg30), 80:41. Unity 2021.1.9f1과 DOTween 설정 화면을 확인했다. Canvas 1280×720, 정사각 보드 FitInParent, 세로 LayoutGroup 안에 가로 행들을 둔다. 자식 icon의 raycast를 끄고 Tile Button에서 선택을 받는다. 예제는 5×5이며 UI 배치는 규칙과 분리해 배운다.

Row의 Tile 배열 순서가 y를 정하고 위쪽이 작은 y다. Item ScriptableObject는 sprite와 value를 보유하고 Tile.Item setter가 icon을 갱신한다. ItemDatabase는 BeforeSceneLoad에서 Resources의 Item을 읽는다. 행 최대 길이를 폭으로 삼아 모든 행을 그 길이로 조회하므로 가변 길이 행을 자동 지원하지는 않는다. 빈 자원·누락 참조·배열 길이는 보완 검증 대상이다.

Swap은 두 icon의 이동 tween을 Sequence.Join으로 묶어 기다린 뒤 parent·icon 참조·Item을 교환한다. **await 자체는 입력 잠금이 아니다.** 마지막 Select 화면도 async void와 공유 selection을 쓰며 busy 가드가 보이지 않는다. 추가 클릭 재진입·씬 종료 취소는 미검증 위험으로 남긴다.

핵심 검출은 같은 Item의 상하좌우 이웃을 재귀로 모으는 flood fill이다. 방문 목록을 공유해 다시 방문하지 않는다. 연결된 세 칸의 작은 ㄱ도 제거된다. `Skip(1).Count>=2`는 시작 칸을 제외한 두 이웃 이상이라는 의미다. Pop의 처음 `<2` 조건으로 두 칸이 지워지는 문제가 생겨 후반에 정정된다.

제거는 icon 축소→**같은 칸 Item 무작위 교체**→확대다. 위 조각이 내려오는 낙하가 아니다. 앞서 지나간 칸에 새 연결이 생겨 남는 문제를 loop 재시작으로 보완한다. 안정화 반복·상한·입력 소유권은 별도 설계가 필요하다. 전체판 CanPop은 기존 무관 그룹 때문에 유효 교환을 잘못 허용할 수 있다는 점도 코드 추론으로 남긴다.

점수는 그룹 Item.value×개수, UI setter로 표시하고 2D OneShot을 넣는다. 마지막 후첨부 구간에서 Neighbours 검사로 아무 칸 교환을 인접 교환으로 제한한다. 초기 랜덤 매치·교착·목표·이동 제한·레벨·저장·특수·장애물은 완성하지 않는다. 음향을 연속 전 구간 청취한 것은 아니다.

## git-amend · grid, 입력 추상화와 단일 해결 흐름

[Part 1](https://www.youtube.com/watch?v=ErHEZ5YGQ5M), [Part 2](https://www.youtube.com/watch?v=s6lqTI8dOQ4), [Part 3](https://www.youtube.com/watch?v=SThzZ_5-erM), 그리고 [공개 제작자 저장소](https://github.com/adammyhre/Match3)를 대조했다. 조회한 저장소의 Unity는 2022.2.14f1, Input System 1.5.1, URP 14.0.7이며 DOTween을 쓴다. 읽은 C# 파일 7개는 grid·grid object·gem type·gem·input reader·audio manager·match3다.

GridSystem2D<T>의 converter로 XY/XZ 평면 변환과 셀 중심/floor를 분리한다. default(T) 반환과 범위 검사, 변경 이벤트·debug 선/TMP 라벨이 있다. Part1 설명란은 09:20의 타입명을 Grid2D가 아닌 GridSystem2D로 정정한다.

Part2는 GemType SO를 SpriteRenderer에 연결하고 무작위 초기판을 만든다. PlayerInput의 Select pointer 위치·Fire 이벤트를 InputReader에서 읽어 Match3가 구독/해제한다. 동일 칸 해제·범위·비어 있음 검사를 추가하고 두 번째 선택에서 교환 coroutine을 시작한다. 인접성·busy·무효 교환 반환은 최종 소스에도 없다.

Part3는 가로·세로 길이3 창을 HashSet에 추가해 고유 좌표로 만든다. `Gem.GetType()`은 작성자가 정의한 GemType 반환 메서드다. C# CLR 형식 비교라고 읽지 않는다. 제거/효과, 빈칸 위 첫 조각 낙하, 빈칸 생성, 음향을 각각 분리한다. 최종 RunGameLoop는 **Swap→Find→Explode→Fall→Fill→Deselect 한 번**이다. 보충 후 연쇄 재검사는 없다.

고정 대기와 tween 길이가 다르며 `DOLocalMove`에 world 중심을 넣는 부모 transform 가정도 확인 대상이다. AudioSource pitch용 전역 Random이 게임 재현에 영향을 주지 않도록 분리하는 것은 보완 제안이다. score·gameover·menu·leaderboard·music·pool은 TODO/향후 주제이며 구현 완료로 기록하지 않는다.

조회한 tree에서는 LICENSE 파일을 찾지 못했다. 원문 전체 코드·에셋을 이 저장소나 게임으로 복사하지 않았다. 소개된 ‘무료’ 자원을 설치하거나 현행 가격·권리 확인을 한 것도 아니다.
