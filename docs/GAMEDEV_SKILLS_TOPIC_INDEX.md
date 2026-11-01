# GameDev agent skills · 78개 주제 색인

2026-11-01 · 원문 고정 커밋 `19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9`. router 1 + 작업 77 본문 전체를 읽었다. 각 항목은 관찰 요약·적용 시 확인 기준·정적 검토 한계이며 실행 성공을 뜻하지 않는다. 행 범위와 전체 파일 해시는 `GAMEDEV_SKILLS_STUDY_VERIFICATION.json`에 있다. 선택 references 14개 외의 보충자료/코드/영상은 미검토 목록을 따른다.

원 자료: Abhishek Barali 및 기여자, awesome-gamedev-agent-skills, Apache-2.0. 재구성 매뉴얼: `GAMEDEV_SKILLS_WORKFLOW.md`.

## 01. router

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/router/SKILL.md) · 본문 1–266행 전체 읽음 · SHA-256 `bf41c3ebc0db5e893135f166771b6fd43cbda07c7fa5bfff5e5dcbbef101d3e7`

- 핵심: 프로젝트 증거로 엔진 하나를 고르고 엔진 API→공통 원리→장르→배포 순으로 최소 문서를 조합한다.
- 검수: 프로젝트 메타데이터·잠금 버전과 선택 근거를 기록하고 없는 기능은 공백으로 표시한다.
- 한계·교정: 새 프로젝트 기본 Godot 제안은 이 원문의 정책이며 기존 Unity 프로젝트 전환 승인이나 스킬 설치 지시가 아니다.

## 02. ai-behavior-trees-utility-ai

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/disciplines/ai-behavior-trees-utility-ai/SKILL.md) · 본문 1–177행 전체 읽음 · SHA-256 `2eb3dc95a34c780952ffd314d7945e3c47296b08671bfbe79996a88e79365a9e`

- 핵심: Blackboard와 Success/Failure/Running 계약을 먼저 정하고 메모리형·반응형 BT와 Utility 점수 선택을 구분한다.
- 검수: 중단 후 Reset·재개·쿨다운 보존·조건 재평가·점수 정규화와 동률 진동을 확인한다.
- 한계·교정: C# 예시는 Unity Vector 이름에 의존하며 다른 엔진으로 그대로 복사할 수 없다. 재시작 문제는 잎의 상태와 반응형 정책까지 봐야 한다.

## 03. audio-design

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/disciplines/audio-design/SKILL.md) · 본문 1–190행 전체 읽음 · SHA-256 `b537036014f7765712d1035f3da314c8ff898ac492e491c6e82a488d03417db5`

- 핵심: Master와 Music/SFX/Voice 등의 버스, 별도 덕킹, 변주·동시 발음 제한과 오디오 시계 기반 박자를 구성한다.
- 검수: 슬라이더 0 음소거·소스의 믹서 우회·음성 명료도·재생 지연·동시 음원 수를 청취로 확인한다.
- 한계·교정: LUFS·dBTP 숫자는 원문이 인용한 특정 권고와 시작값이다. 실제 청취·플랫폼 요구 확인 없이 프로젝트 사양으로 고정하지 않는다.

## 04. camera-systems

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/disciplines/camera-systems/SKILL.md) · 본문 1–163행 전체 읽음 · SHA-256 `3c590facf57b2110c59d9e245b3078c0d4c20ebbfe723507914575c4cb36f9ee`

- 핵심: 프레임 독립 보간·데드존·예측 위치·화면 경계·충돌 카메라와 별도 흔들림 오프셋을 조합한다.
- 검수: 서로 다른 프레임률·벽·구석·텔레포트에서 떨림과 화면 밖 노출을 확인한다.
- 한계·교정: 경계는 카메라 중심만이 아니라 화면 반크기를 고려한다. Cinemachine 3와 다른 버전 API를 섞지 않는다.

## 05. create-game-assets

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/disciplines/create-game-assets/SKILL.md) · 본문 1–137행 전체 읽음 · SHA-256 `c7c6da3d7bd528ff79934ac7556097cca4288fb321449d5acfa8e45fbba88b20`

- 핵심: 기존 승인 방향과 기술 프레임을 기록하고 대표 기준→같은 계열 제작→정규화→엔진 문맥 검수로 진행한다.
- 검수: 팔레트·관점·피벗·알파·반복·해상도·출처/권리·실제 게임 크기 가독성을 확인한다.
- 한계·교정: 원문 생성/검사/설치 명령은 실행하지 않았다. 생성 결과나 자동 크기 검사만으로 제작 완료를 판정하지 않는다.

## 06. dialogue-systems

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/disciplines/dialogue-systems/SKILL.md) · 본문 1–182행 전체 읽음 · SHA-256 `d1d8017c461df157a870723d530ee2cd9c9606c775992e3802a84a528a3a7279`

- 핵심: 대화 노드·선택·조건·변수·줄 ID를 분리하고 전이의 비용/효과와 저장·현지화를 연결한다.
- 검수: 분기 종료·막힌 노드·재방문 중복 지불·선택 직전 조건·번역 텍스트 길이를 확인한다.
- 한계·교정: Ink/Yarn 도입이나 임의 표현식 실행 승인이 아니다. 사용자 입력이나 외부 저장을 평가할 인터프리터 경계는 별도 검증한다.

## 07. game-ai

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/disciplines/game-ai/SKILL.md) · 본문 1–179행 전체 읽음 · SHA-256 `34d199045a44226ce6ed0cc7e3f4e0b29d862fe12033a5f4a65c155acf81a2e3`

- 핵심: 의사결정·경로탐색·조향을 분리하고 이동 그래프에 맞는 A* 휴리스틱과 경로 재계산 주기를 고른다.
- 검수: 경로 표시와 상태 전환을 보며 코너·시야 상실·목표 이동·막힘 타임아웃을 검수한다.
- 한계·교정: 4방향과 대각 이동의 비용 가정이 다르다. 개념 예제를 완성된 내비게이션 엔진으로 취급하지 않는다.

## 08. game-feel

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/disciplines/game-feel/SKILL.md) · 본문 1–174행 전체 읽음 · SHA-256 `67900d0e41630914e1a45b55aced3321550f87b26d34e439d3952dd803e9c842`

- 핵심: 게임 규칙 위에 중요도별 소리·파티클·흔들림·일시 정지·이징 피드백을 얹고 휴식 상태로 돌아오게 한다.
- 검수: 반복 트리거·겹친 hit-stop·일시 정지·입력 버퍼·감소 옵션·시뮬레이션 분리를 확인한다.
- 한계·교정: Unity 짧은 예시는 겹침 보호가 없고 timeScale=1 복원은 기존 일시정지/슬로 모션을 덮을 수 있다. 자동 승인된 제품 연출이 아니다.

## 09. game-ui-ux

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/disciplines/game-ui-ux/SKILL.md) · 본문 1–167행 전체 읽음 · SHA-256 `8916cd1da6df6e53cf316e9024657c5c178f7e7750e79eeea93bfd44cf9acd54`

- 핵심: 앵커·레이아웃·안전영역·초기 포커스·화면 스택과 이벤트 기반 HUD로 화면 상태를 분리한다.
- 검수: 화면비·번역 길이·글자 확대·터치 및 패드 단독 조작·뒤로가기를 검수한다.
- 한계·교정: 1920×1080과 글자 크기는 예시·특정 접근성 안내다. 프로젝트 화면 방향·실제 픽셀밀도에 맞춰 확인한다.

## 10. input-systems

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/disciplines/input-systems/SKILL.md) · 본문 1–211행 전체 읽음 · SHA-256 `70112718392e1e0a62cd335a5fe8c6272128e18728b1e40c6f8a75001bbef9b4`

- 핵심: 물리 키를 의미 있는 액션에 연결하고 순간 입력·유지 입력·데드존·재바인딩·저장을 나눈다.
- 검수: 키 충돌·취소·초기화·장치 교체·메뉴 접근 보존·버퍼 1회 소비를 확인한다.
- 한계·교정: 코요테 타임과 점프 버퍼는 플랫폼 장르 예시이며 퍼즐 신규 동작 요구가 아니다. 엔진 입력 모듈별 API 대조가 필요하다.

## 11. level-design

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/disciplines/level-design/SKILL.md) · 본문 1–169행 전체 읽음 · SHA-256 `51e8368cc1a78faae3467ee73ec03c7c7aae7e45991639a09441832aca9694d2`

- 핵심: 이동 실측→그레이박스→주 경로와 잠금 조건→학습·연습·시험→플레이 관찰→아트 순서다.
- 검수: 통로·도달거리·시야·소비성 열쇠·일방통행·복원 후 경로를 검수한다.
- 한계·교정: 포물선 공식은 이상 모델이며 실제 컨트롤러로 측정한다. 단조 증가 열쇠 집합 예시는 소비성 자원과 재잠금을 해결하지 않는다.

## 12. performance-optimization

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/disciplines/performance-optimization/SKILL.md) · 본문 1–172행 전체 읽음 · SHA-256 `9c68d80b13943b246b0e1b8c35747ab4de700d3deb1ce2a0d3f65eba1b8da731`

- 핵심: 재현 장면과 프레임 예산을 정한 뒤 CPU·GPU 병목 하나를 측정하고 변경 전후를 비교한다.
- 검수: 동일 기기·장면·빌드의 시간·GC·드로콜·메모리·최악 구간을 기록한다.
- 한계·교정: 풀 예시는 숨김·일반 처리만 중지하므로 물리·콜라이더·타이머·이벤트 초기화가 별도로 필요하다. 드로콜 비용은 CPU 제출과 GPU 양쪽을 구분한다.

## 13. physics-tuning

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/disciplines/physics-tuning/SKILL.md) · 본문 1–164행 전체 읽음 · SHA-256 `b0ff90eb85509cfa3ca9e27f989b637160903479e57daa2011be9101cbd4913c`

- 핵심: 고정 물리 스텝·표시 보간·CCD·질량비·감쇠·수면·충돌 행렬을 분리해 조정한다.
- 검수: 낮은 FPS·얇은 벽·고속 물체·스택·텔레포트·보간 중복을 확인한다.
- 한계·교정: 고정 스텝만으로 플랫폼 간 결정성을 보장하지 않는다. 레이어/마스크의 양방향 조건은 엔진과 질의 종류에 따라 다르다.

## 14. procedural-gen

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/disciplines/procedural-gen/SKILL.md) · 본문 1–173행 전체 읽음 · SHA-256 `6a58c287b7c656a63912f7a5ca32a96be274ba7d9525c7b9670235356403583b`

- 핵심: 전용 RNG·데이터 생성·연결성 검사·시도 상한·고정 씨드 비교와 여러 씨드 분포 검사를 구성한다.
- 검수: 생성기 버전·현재 RNG 상태·안전한 스폰·출구 연결·빈/음수 가중치·끝점 경계를 확인한다.
- 한계·교정: 씨드만 같아도 라이브러리·호출 순서가 바뀌면 결과는 달라진다. 커스텀 PRNG 제작이나 임의 패키지 설치는 승인 범위가 아니다.

## 15. save-systems

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/disciplines/save-systems/SKILL.md) · 본문 1–191행 전체 읽음 · SHA-256 `14bfd8e49c2c7ceead27d22ec6b6ee7a5cfe661386d2f12d8627f6fd701da437`

- 핵심: 순수 데이터 스냅샷·스키마 버전·임시 쓰기·백업·순차 마이그레이션·검증 후 복원을 분리한다.
- 검수: 완전 종료 후 복구·이전 버전·미래 버전·손상/백업·디스크 실패·연속 저장을 확인한다.
- 한계·교정: 원문도 Windows 이름변경과 fsync 부재를 한계로 명시한다. 임시 파일만으로 전원 차단 내구성을 보장하지 않는다. 씨드와 RNG 현재 상태도 구분한다.

## 16. shader-programming

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/disciplines/shader-programming/SKILL.md) · 본문 1–170행 전체 읽음 · SHA-256 `0c6f870c73b8ede7d01bdc8d5c66045cc0ded80293bc28962d72d763daa33485`

- 핵심: 정점/픽셀 단계와 좌표계·UV·정규화·시간·텍스처 읽기를 구분해 효과를 설계한다.
- 검수: 실제 렌더 경로·언어 방언·모바일 정밀도·smoothstep 순서·alpha/깊이/오버드로를 확인한다.
- 한계·교정: GLSL/HLSL/TSL은 그대로 교환되지 않는다. discard 대신 블렌딩이 항상 빠르다는 뜻도 아니며 하드웨어에서 측정해야 한다.

## 17. ebitengine-game

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/ebitengine/ebitengine-game/SKILL.md) · 본문 1–213행 전체 읽음 · SHA-256 `fdbb3f6cb791f70becf00f8bedf8b302a1d8e5e02c4a824906b6bd4fca5831ab`

- 핵심: Ebitengine은 고정 Update에서 입력·규칙을 처리하고 Draw는 표시만, Layout은 논리 화면과 입력 좌표를 정한다.
- 검수: 동일 tick의 상태와 화면·재시작·실입력·브라우저 오디오·폰트·요청한 플랫폼의 실제 실행을 확인한다.
- 한계·교정: 2.10.5/Go1.25는 원문의 고정 예시다. 검사기/스타터는 실행하지 않았고 GPU 없는 규칙 검사·교차 빌드만으로 플레이 품질을 보장하지 않는다.

## 18. card-game

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/genres/card-game/SKILL.md) · 본문 1–138행 전체 읽음 · SHA-256 `55cb3ab85d2ab66f787eddb2001805e641d70a7822b8a9f7f174b9174d5eea02`

- 핵심: 카드 인스턴스는 한 영역에만 두고 비용·타깃 검증 후 영역 이동과 효과를 정해진 순서로 처리한다.
- 검수: 중복 카드·덱 소진·셔플 범위·취소 후 자원·동시 효과 순서·RNG 복구를 확인한다.
- 한계·교정: 자동 재셔플·손패 제한은 게임 규칙 선택이다. 비용 선검증만으로 예외·네트워크까지 포함한 완전한 트랜잭션이 되지는 않는다.

## 19. fps-shooter

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/genres/fps-shooter/SKILL.md) · 본문 1–123행 전체 읽음 · SHA-256 `eb74c6f841f65dee5a44feb07c9f082c667c34b516d260e6787365f76b9ac64d`

- 핵심: 시점·입력·히트스캔/투사체·탄약·피해·AI를 분리하고 HP·피해량·발사율로 TTK를 함께 조절한다.
- 검수: 자기 콜라이더 제외·트리거 규칙·무기 원점과 조준점·탄 수명·프레임별 감도를 확인한다.
- 한계·교정: 마우스 delta와 스틱 각속도의 dt 처리는 다르다. 범위·헤드샷 값은 예시이고 온라인 판정은 별도 권위 모델이 필요하다.

## 20. platformer

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/genres/platformer/SKILL.md) · 본문 1–153행 전체 읽음 · SHA-256 `1d5c688c33a9ca4562070878b84c88cc687681dcfea842c121d25a0620f74cba`

- 핵심: 점프 높이·정점 시간으로 초기 중력을 정하고 버퍼·코요테·벽/공중 점프 우선순위를 조합한다.
- 검수: 고정 tick의 실측 거리·낮은 천장·단방향/이동 발판·중복 플랫폼 속도·재생성을 확인한다.
- 한계·교정: 3~4타일·시간 수치는 시작 예시다. 가변 프레임 의사코드는 실제 고정 물리 루프에 맞춰야 한다.

## 21. puzzle

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/genres/puzzle/SKILL.md) · 본문 1–143행 전체 읽음 · SHA-256 `2923586901c4998a5bc5deb2235038e6161e7f927d45b8e8ea6b4c7c7327a384`

- 핵심: 보드 모델을 권위 상태로 두고 유효 이동→매치→제거→중력→보충→연쇄 안정화와 표시를 분리한다.
- 검수: 빈칸 sentinel·RNG 상태·목표/턴수·입력 잠금·마스크 중력·막힌 구간·무한 연쇄를 검수한다.
- 한계·교정: has_valid_move는 다음 수 존재만 보이며 목표까지 풀림을 증명하지 않는다. 0이 색이면 truthy 검사는 틀릴 수 있다. Undo·지수 배점은 장르 예시이고 제품 승인 사항이 아니다.

## 22. roguelike

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/genres/roguelike/SKILL.md) · 본문 1–142행 전체 읽음 · SHA-256 `52e1d3ce27ac16ed84da23c9588d2456a8cbb0938d35ca3b13d5b396e65a0332`

- 핵심: 턴 스케줄러·생성 맵·가시/탐험 상태·드롭·런과 프로필 저장을 분리한다.
- 검수: 모든 배우의 에너지 지급·양수 속도·가시성 대칭·연결성·사망 후 프로필 보존을 확인한다.
- 한계·교정: 빈 배우 목록이나 모두 행동 불가인 경우 예시의 while True는 종료하지 않을 수 있다. 영구 사망 저장 삭제는 제품별 명시 규칙이 필요하다.

## 23. rpg

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/genres/rpg/SKILL.md) · 본문 1–141행 전체 읽음 · SHA-256 `370d9b73048f8760576595bdb14924f14f8fe48e2c17853a4e5c87d3b24877c5`

- 핵심: 기본 능력치와 수정자·파생치, 퀘스트 상태·보상·대화 플래그를 데이터로 구성한다.
- 검수: 장비 해제 복원·중첩 버프·연속 레벨업·보상 1회·퀘스트 중간 저장을 확인한다.
- 한계·교정: 성장식·피해식·치명타율은 장르 설계 선택이며 기존 게임 경제를 바꾸는 승인이 아니다.

## 24. survival-crafting

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/genres/survival-crafting/SKILL.md) · 본문 1–148행 전체 읽음 · SHA-256 `174e15b32251a31feab0c1edf81240d6327eba974ae78f2a1e0e9f16f93a3420`

- 핵심: 수집→제작→건설→요구 관리의 진행 사다리와 레시피·시설·기술·월드 상태를 연결한다.
- 검수: 재료 소비 전 결과 공간·가득 찬 가방에서 확보되는 칸·중복 채집·저장 복구를 확인한다.
- 한계·교정: 검사 후 소비 예시는 단일 스레드 의사코드다. 서버/동시 요청/실패 복구의 원자성은 별도 설계해야 한다.

## 25. tower-defense

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/genres/tower-defense/SKILL.md) · 본문 1–124행 전체 읽음 · SHA-256 `09f6f329e7178ff853b4a4dc0ef148f121fc5296c2a942585fdfe1b3cc502d8c`

- 핵심: 웨이브 데이터·경로 진행도 기반 표적·배치·경제·누수/생명 조건을 묶는다.
- 검수: 설치 후 스폰과 현재 적 모두의 경로·코너 잔여 이동량·발사 주기·처리 완료를 확인한다.
- 한계·교정: DPS×사거리 체류시간은 예비 산식이다. 여러 적·과잉 피해·광역/방어·차단의 실제 전투 결과를 보장하지 않는다.

## 26. visual-novel

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/genres/visual-novel/SKILL.md) · 본문 1–153행 전체 읽음 · SHA-256 `c777292dd2032f6eec2eb0e75afaa3303a399e4f6caa0d01499b81af127c2d87`

- 핵심: 대화 실행기와 화면 표시를 분리하고 전체 문장 배치 후 글자 노출·읽음 기록·선택·저장을 관리한다.
- 검수: 즉시 노출 후 다음 줄의 입력 분리·번역/마크업 줄바꿈·미독 스킵 방지·정확한 재개를 확인한다.
- 한계·교정: Ink의 위치 저장과 Yarn의 노드 재개 범위를 구분한다. Ren'Py 예시는 원문 버전 전제이며 프로젝트 교체 지시가 아니다.

## 27. godot-2d-movement

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/godot/godot-2d-movement/SKILL.md) · 본문 1–154행 전체 읽음 · SHA-256 `33c8ba750530ee12bb71ea49fd077db495dc7ae6b1e1076786c5fb9661c74502`

- 핵심: CharacterBody2D의 velocity를 설정하고 고정 스텝에서 인수 없는 move_and_slide로 이동·접촉 결과를 얻는다.
- 검수: 중력과 이동의 dt 중복·바닥 방향·경사 스냅·탑다운 floating·접촉 결과 시점을 확인한다.
- 한계·교정: 3.x 호출 형식은 다르다. 예시 감속의 고정 스텝 의존과 버퍼/코요테 소비 정책은 실제 조작에서 검수해야 한다.

## 28. godot-3d-essentials

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/godot/godot-3d-essentials/SKILL.md) · 본문 1–140행 전체 읽음 · SHA-256 `34cefc1451b6f1ccac3cd60e8f8b4ec453af1e834d6466bd7c1e8506e2bbc556`

- 핵심: Node3D의 로컬/글로벌 변환·현재 카메라·조명·WorldEnvironment·재질·GridMap을 조립한다.
- 검수: 카메라 선택·검은 화면·look_at 특이점·비균일 스케일·MeshLibrary·렌더러 기능을 확인한다.
- 한계·교정: 카메라 lerp(rate×dt)는 지수 보간과 동일한 프레임 독립 해법이 아니다. Godot 4.7 추가 기능 주장은 원문 전제다.

## 29. godot-animation

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/godot/godot-animation/SKILL.md) · 본문 1–130행 전체 읽음 · SHA-256 `92007692a8956c31bded0552c804c49c10efc8c0cff9444ef026605db279f40c`

- 핵심: AnimationPlayer의 클립, AnimationTree의 전이/블렌드, Tween의 단발 속성 변화에 소유권을 나눈다.
- 검수: Tree 활성·파라미터 경로·같은 트랙 경쟁·루프 완료 대기·Container 자식 변환을 확인한다.
- 한계·교정: 모든 애니메이션 종료 신호가 요청한 클립의 완료라는 보장은 없다. 취소/전환과 반복 클립 처리도 필요하다.

## 30. godot-audio

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/godot/godot-audio/SKILL.md) · 본문 1–125행 전체 읽음 · SHA-256 `720da9054685670c09787b69ea893e4cddc292860ebf4d601605f9102f09926a`

- 핵심: 비위치/2D/3D 플레이어와 버스·dB·동시 재생·두 트랙 전환·출력 지연 보정 시계를 나눈다.
- 검수: 버스 -1·0 음량·SFX 끊김·루프 가져오기·청취 위치·오디오 시계의 시작 구간을 확인한다.
- 한계·교정: 교차 페이드는 중첩 요청·기존 Tween 취소·슬라이더 보존까지 보완해야 하며 이번에는 청취하지 않았다.

## 31. godot-csharp

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/godot/godot-csharp/SKILL.md) · 본문 1–172행 전체 읽음 · SHA-256 `8d62d7e94020608bcf253c19d3f227b14088563a801fa7a11b6d1449221a0725`

- 핵심: .NET 빌드의 partial C# 클래스·PascalCase 콜백·double delta·Export·Signal·GDScript 호출을 연결한다.
- 검수: SDK/타깃·생성된 이벤트명·Vector 값형 복사·해제 객체·플랫폼 내보내기를 확인한다.
- 한계·교정: Godot C#와 Unity C#의 타입/API는 교환되지 않는다. 웹·모바일 지원은 원문 버전 제약이고 설치/빌드 검증은 미실행이다.

## 32. godot-export

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/godot/godot-export/SKILL.md) · 본문 1–129행 전체 읽음 · SHA-256 `095177a5322056fbf8949b38213717c9e6f5b1f92e080fd40851a50a56afbe46`

- 핵심: 엔진과 일치하는 export template·preset·파일 포함·플랫폼 인증과 실제 대상 빌드를 나눈다.
- 검수: preset 이름·누락 JSON·user 경로 쓰기·웹 HTTP와 스레드 헤더·디버그/릴리스 출력을 확인한다.
- 한계·교정: 헤드리스 빌드는 GUI/오디오/입력 검증이 아니다. 템플릿 설치·서명·배포 명령은 실행하지 않았다.

## 33. godot-gdscript

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/godot/godot-gdscript/SKILL.md) · 본문 1–135행 전체 읽음 · SHA-256 `a46809d73f9071cdc211f444726b60139519cb8cea776444fb05bc44655cbab4`

- 핵심: 정적 타입·export/onready·ready/process/physics 콜백·Callable 신호·await를 역할별로 쓴다.
- 검수: 노드 준비 시점·정수 나눗셈·전역 타입 충돌·3.x 문법·모든 반환 경로를 확인한다.
- 한계·교정: 주석의 4.7 변화는 원문 주장으로 표시하고 이전 프로젝트에 무조건 적용하지 않는다.

## 34. godot-gdscript-headless-testing

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/godot/godot-gdscript-headless-testing/SKILL.md) · 본문 1–201행 전체 읽음 · SHA-256 `22f5403f3d27e6ad11ccc975fac6107f5a08de4b1f640b5cf58d6e02c47ee5c7`

- 핵심: SceneTree 테스트 러너는 실패를 집계하고 명시적 비정상 종료코드·import·timeout·양쪽 로그를 갖춘다.
- 검수: 일부러 실패하는 검사·런타임 오류·끝나지 않는 await·fresh checkout 자원 로딩을 확인한다.
- 한계·교정: 원문이 검증했다고 쓴 Godot 실행은 이번 수행 결과가 아니다. 테스트 코드와 CI도 실행하지 않았다.

## 35. godot-multiplayer

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/godot/godot-multiplayer/SKILL.md) · 본문 1–167행 전체 읽음 · SHA-256 `62bdf9fa9dfb89f546c4ce1c25c9192cca6875dab016addd703d4a324d439083`

- 핵심: ENet 연결·RPC 권한·노드별 authority·스폰/동기화와 서버 검증을 분리한다.
- 검수: 호스트/클라이언트·sender ID·동일 NodePath·서명·연결 실패·재접속·공개 가시성을 확인한다.
- 한계·교정: 클라이언트가 직접 이동하는 예시를 완전한 서버 권위 시뮬레이션으로 부르지 않는다. 호스트 로컬 sender 처리는 추가 검증이 필요하다.

## 36. godot-nodes-scenes

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/godot/godot-nodes-scenes/SKILL.md) · 본문 1–136행 전체 읽음 · SHA-256 `03cb03554281e0e424a4127607c6799d6f05f27d273bf1c55ba2de164c5f5b2c`

- 핵심: 작은 재사용 scene을 합성하고 PackedScene 생성·트리 진입·autoload·지연 해제와 참조 수명을 관리한다.
- 검수: 부모 변환 아래 좌표·ready 이전 접근·씬 교체 뒤 오래된 참조·해제 객체를 확인한다.
- 한계·교정: 외부 경로 검사기는 실행하지 않았다. 고유 이름도 실제 이름 변경과 저장/소유권 문제를 자동 해결하지 않는다.

## 37. godot-physics

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/godot/godot-physics/SKILL.md) · 본문 1–177행 전체 읽음 · SHA-256 `61a90d986b667c71547fc555f61d8df487732ba868d4612d6411ae8c04eaed72`

- 핵심: 2D/3D 바디 종류와 Area 질의·레이어/마스크를 나누고 3D 물리 백엔드를 먼저 확인한다.
- 검수: 단방향 감지·monitoring/monitorable·ray 갱신·자기 RID 제외·Jolt 접촉/관절/경계 차이를 확인한다.
- 한계·교정: 물리 공통 문서의 양방향 마스크 단정과 충돌한다. 감지와 물리 충돌을 엔진별로 구분한다.

## 38. godot-resources

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/godot/godot-resources/SKILL.md) · 본문 1–126행 전체 읽음 · SHA-256 `3bd20b0230943ce4822552488c85fc6e9014f553e1ee1bff5470ba39789844d8`

- 핵심: Resource는 공유 데이터이며 preload/load·복제·user 저장과 threaded loading의 용도를 나눈다.
- 검수: 공유 원본 변형·외부 하위 Resource 복사 범위·순환 참조·쓰기가능 경로·반환 Error를 확인한다.
- 한계·교정: .tres 등 엔진 자원 로딩은 임의 사용자가 바꾸는 순수 데이터 저장과 다르다. 공유 객체를 플레이어 저장 파일로 오해하지 않는다.

## 39. godot-shaders

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/godot/godot-shaders/SKILL.md) · 본문 1–148행 전체 읽음 · SHA-256 `18494fa2491b87cbe5c84c2c8922fbab2e22da8bc6196a00c070b2fa6192d1cd`

- 핵심: canvas_item/spatial의 출력·uniform 색 해석·TIME/UV·화면 텍스처를 구분한다.
- 검수: 투명 패스·깊이/그림자·샘플러 반복·시간 rollover·정밀도·색 변환을 확인한다.
- 한계·교정: ALPHA를 쓰는 경로와 discard의 비용은 렌더러/기기에 따라 다르다. 호환 컴파일과 실제 화면은 미검증이다.

## 40. godot-signals-groups

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/godot/godot-signals-groups/SKILL.md) · 본문 1–134행 전체 읽음 · SHA-256 `0892fd50b91f93a6dc5f7750587fa51d1389cd334d4039bfa2c8fb9720b39868`

- 핵심: 자식은 신호를 보내고 부모가 연결하며 typed 이벤트·bind·one-shot·그룹 브로드캐스트를 구분한다.
- 검수: 중복 연결·캡처된 해제 객체·인수 개수·전역 그룹 충돌·무시되는 메서드명을 확인한다.
- 한계·교정: 그룹 호출의 조용한 누락과 신호 수명 처리는 계약으로 검수한다. 원문의 자동 ready 재호출 설명은 노드 재준비 정책과 함께 확인한다.

## 41. godot-tilemap

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/godot/godot-tilemap/SKILL.md) · 본문 1–134행 전체 읽음 · SHA-256 `021b561343b79f6606ed178b307ad85120588bf1e608319144b4b15df2e6ff6d`

- 핵심: TileMapLayer 하나당 한 층으로 TileSet의 충돌·내비게이션·사용자 데이터·terrain을 배치한다.
- 검수: 카메라 이동/줌 뒤 입력 좌표·빈 셀·미완성 peering·지연 업데이트와 국소 갱신을 확인한다.
- 한계·교정: 오래된 다층 TileMap API와 혼용하지 않는다. 셀의 화면 표시만으로 보드 규칙이나 이동 가능성을 보장하지 않는다.

## 42. godot-ui-control

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/godot/godot-ui-control/SKILL.md) · 본문 1–131행 전체 읽음 · SHA-256 `e2e05419a2e902448992050ceae1e45013b7c9d1eb54371b6fdd1b3214154bad`

- 핵심: Control 앵커/offset과 Container 소유 레이아웃·Theme·초기 포커스·mouse_filter를 조합한다.
- 검수: 창 크기·번역 길이·컨트롤러 포커스·장식 패널 입력 차단·테마 상속을 확인한다.
- 한계·교정: Container 자식의 직접 위치 제어와 레이아웃이 경쟁할 수 있다. 최신 offset_transform 사용은 원문 전제 버전을 확인한다.

## 43. bevy-ecs

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/other-engines/bevy-ecs/SKILL.md) · 본문 1–232행 전체 읽음 · SHA-256 `b34e88dcdfc5b4e385487e70a17b47b4fad9a7547938fc76bc2d23cd0d9dc11d`

- 핵심: ECS의 Component/Resource·Query·지연 Commands·스케줄 순서를 분리하고 실제 Cargo 고정 버전을 먼저 읽는다.
- 검수: 겹치는 가변 Query, With/Without/ParamSet, 체인과 지연 적용 경계, 광범위 despawn의 자원 엔티티 포함 여부를 확인한다.
- 한계·교정: Bevy 0.20의 Messages·On·필수 컴포넌트 예시는 이전 버전과 다르며 컴파일하지 않았다.

## 44. defold-core

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/other-engines/defold-core/SKILL.md) · 본문 1–265행 전체 읽음 · SHA-256 `d5a27593e3fa2c786501076c359ce082ea56cc6e9c98066a2805c6ade78fc41e`

- 핵심: Defold의 collection/game object/component·self 상태·메시지 URL·factory/proxy 로드를 구분한다.
- 검수: 컴파일된 경로 접미사, 입력 포커스 스택, proxy 비동기 로드 후 init/enable/unload, fixed_update 설정을 확인한다.
- 한계·교정: Bob/JDK/검사기 실행과 설치는 하지 않았다. game.project만으로 엔진 버전을 고정했다고 주장하지 않는다.

## 45. love2d-core

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/other-engines/love2d-core/SKILL.md) · 본문 1–150행 전체 읽음 · SHA-256 `32601d08ba09afa80ef5dee8dbdf40bf31bd97b165177b5243196b6ea2182c71`

- 핵심: LÖVE의 load/update(dt)/draw와 키 누름·유지 입력, conf.lua 초기 설정, 화면 스택을 나눈다.
- 검수: 초 단위 dt, 대각선 속도, 전역 색 복원, push/pop 시 수명과 창 입력을 검수한다.
- 한계·교정: LÖVE 11.5 전제이며 화면 실행·입력은 미검증이다. 버전 경고가 강제 버전 잠금은 아니다.

## 46. pygame-core

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/other-engines/pygame-core/SKILL.md) · 본문 1–192행 전체 읽음 · SHA-256 `908ff45097ab34da9fa734cf0d6095361b8910524a3e145d4daff8420f92a343`

- 핵심: pygame-ce 이벤트→갱신→그리기→flip 루프에 초 단위 dt와 부동소수 좌표·Rect 충돌을 연결한다.
- 검수: display 생성 후 convert_alpha, 0벡터 정규화, 정수 반올림과 멈춤 dt 정책을 확인한다.
- 한계·교정: pygame와 pygame-ce는 같은 import 이름을 쓰므로 임의 동시 설치/교체하지 않는다. Rect 접촉은 픽셀 충돌 해결이 아니다.

## 47. roblox-characters

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/other-engines/roblox-characters/SKILL.md) · 본문 1–168행 전체 읽음 · SHA-256 `12349b54046cec0aec4e441f5a1f7d7517bbe3e622497b7916a8e4a2a93e9bb1`

- 핵심: Player와 교체되는 Character 수명을 분리하고 기존 캐릭터·재생성·도구·애니메이션 연결을 관리한다.
- 검수: 대기 전후 세대 검사, timeout, R6/R15 계약, 이전 연결과 트랙 정리, 서버 게임판정을 확인한다.
- 한계·교정: 물리 소유권이나 애니메이션 마커가 게임 권한을 주지 않는다. 베타·rolling API는 실제 대상 확인이 필요하다.

## 48. roblox-datastores

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/other-engines/roblox-datastores/SKILL.md) · 본문 1–211행 전체 읽음 · SHA-256 `19d59117873bc1cb758c221514b9995c91731672ac68e974a6e582b023e90aa1`

- 핵심: 서버 전용 저장에서 성공한 로드 표시를 저장 전제조건으로 삼고 UpdateAsync 재시도·종료 예산을 나눈다.
- 검수: 로드 중 이탈, 저장 실패, 콜백 비양보·순수성, 다중 세션, 불명확한 증가 쓰기의 중복 적용을 확인한다.
- 한계·교정: 예시 UpdateAsync가 old를 무시하고 newData를 반환하므로 세션 충돌 방지를 보장하지 않는다. 세션 잠금/버전 병합이 추가로 필요하다.

## 49. roblox-luau

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/other-engines/roblox-luau/SKILL.md) · 본문 1–212행 전체 읽음 · SHA-256 `13cd9260eab1e7672fb27691600f68d4b65114064fff4f69f15261a258f3f6df`

- 핵심: Luau 서비스·Instance·ModuleScript·이벤트를 실행 위치와 RunContext에 맞춰 배치하고 Parent를 마지막에 설정한다.
- 검수: 서버/클라이언트 상태 분리, 연결 정리, 서버 가격 산정, 전역/플레이어별 debounce 의도를 확인한다.
- 한계·교정: Script 클래스만으로 서버 실행을 단정하지 않는다. Luau 진단·Rojo·LSP 실행은 하지 않았다.

## 50. roblox-networking

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/other-engines/roblox-networking/SKILL.md) · 본문 1–213행 전체 읽음 · SHA-256 `e71b671d160fa85ace13075cf4b920d0dd565d96513ae0acaa79b00b3d837440`

- 핵심: 클라이언트 요청·서버 확정 사실·교체 가능한 장식을 구분하고 Remotes에서 값과 권한을 검증한다.
- 검수: 유한수·클래스·부모 경로·거리·쿨다운·빈도, 첫 yield 전 점유, streaming 누락과 대상별 발송을 확인한다.
- 한계·교정: 이벤트 시작 순서가 yield 뒤 완료 순서를 보장하지 않는다. 서버 권위 모드 전환·rolling 한도는 자동 적용하지 않는다.

## 51. roblox-physics

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/other-engines/roblox-physics/SKILL.md) · 본문 1–160행 전체 읽음 · SHA-256 `2d16e2a9bb6c7aa40b0df0a546a85ba861abab83457ce384deff97c4d5a7e745`

- 핵심: 물리 시뮬레이션·캐릭터 조작·권위 있는 히트 질의·장식 이동을 나누고 assembly 단위 힘/충격을 쓴다.
- 검수: CanCollide/CanTouch/CanQuery, query 필터와 중복 모델 제거, anchored 전환·질량·network owner를 확인한다.
- 한계·교정: Bounds overlap는 정확 형상 판정이 아니다. Workspace 충돌그룹 등 최신 API 주장은 원문 전제로 별도 확인하며 실행하지 않았다.

## 52. roblox-simulator-economy

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/other-engines/roblox-simulator-economy/SKILL.md) · 본문 1–198행 전체 읽음 · SHA-256 `2879ce1c168ff9ab6b5c357a1b69d9e9a6393b1a210da3c7d9726add33028836`

- 핵심: 경제 수치를 페이싱 표로 먼저 정하고 서버에서 ID 기반 구매·차감·지급을 yield 없이 처리한다.
- 검수: 개별 내림 가격 합과 기하급수 근사 차이, buy-max 상한, 숫자 정밀도·NaN, 오프라인 시간 상한을 확인한다.
- 한계·교정: Lune 계산기는 실행하지 않았다. 자동 손상값 0 보정은 실제 유료 자산 복구 정책과 별개이며 결제·확률 정책은 최신 원문 재확인이 필요하다.

## 53. roblox-studio-workflow

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/other-engines/roblox-studio-workflow/SKILL.md) · 본문 1–183행 전체 읽음 · SHA-256 `c58a8188db279f5499332e6a670f1240fbc38687988fcc9410d6c699af19fd38`

- 핵심: Studio/Rojo 중 각 하위 트리의 정본을 정하고 기존 모듈·remote·태그를 재사용하며 편집 가능한 계층을 보존한다.
- 검수: 정적→단일 실행→수명→다중 클라이언트→기기→실패 검수 단계를 구분하고 양쪽 Output을 기록한다.
- 한계·교정: MCP 사용은 선택사항이다. 연결·앱 조회·자동화·외부 모델 삽입을 이번 학습에서 수행하지 않았다.

## 54. roblox-ui

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/other-engines/roblox-ui/SKILL.md) · 본문 1–254행 전체 읽음 · SHA-256 `ed177f5e06c6414a11cfaaeb6e6a0ead645a884b87901eeada3b389175a8635b`

- 핵심: ScreenGui/PlayerGui의 수명, 반응형 레이아웃·안전 영역·Activated·모달 포커스·감소된 모션을 함께 설계한다.
- 검수: 재생성 뒤 참조, 스크롤/텍스트/터치 영역, 입력 장치 전환, 포커스 복원, 트윈 중단과 연결 해제를 확인한다.
- 한계·교정: 예시 트윈은 연속 열기/닫기 경쟁을 완전히 해결하지 않는다. 700px 분기점·스타일은 프로젝트 고정값이 아니다.

## 55. unity-animation

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/unity/unity-animation/SKILL.md) · 본문 1–131행 전체 읽음 · SHA-256 `dcb5f95b8ccf8ffdd7be4d4443a2b72aec2031fda5da5b8603bfced5b7870ad2`

- 핵심: Animator 파라미터·Blend Tree·레이어/Avatar Mask·Root Motion 책임과 Humanoid IK 조건을 구분한다.
- 검수: 트리거 소비·미소비 잔류·전이 중 다음 상태·루트 이동 중복·IK Pass를 확인한다.
- 한계·교정: 직접 상태 진입은 명시적 피격 등 예외로 구분한다. clip length 대기는 속도·블렌드에 따라 실제 완료와 다를 수 있다.

## 56. unity-build-pipeline

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/unity/unity-build-pipeline/SKILL.md) · 본문 1–169행 전체 읽음 · SHA-256 `b32c708ecfc53a7d3a34f771b296ab03349faec15e1dd9e1e79f196fe26282ee`

- 핵심: 빌드 프로필별 장면 목록·타깃·백엔드·스트리핑·Addressables 콘텐츠와 BuildReport를 함께 관리한다.
- 검수: 선택 프로필·시작 장면·실패 종료코드·반사 코드 보존·실제 플레이어 실행을 검수한다.
- 한계·교정: 원문의 CI 명령은 읽기 자료다. 설치·CLI 실행·프로덕션 배포 승인으로 취급하지 않는다. IL2CPP가 항상 더 빠르다는 성능 보장은 피한다.

## 57. unity-csharp-scripting

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/unity/unity-csharp-scripting/SKILL.md) · 본문 1–159행 전체 읽음 · SHA-256 `a729afd3f73eb8c92841ef60c2c3aac16be4264706af5caaf6f83635a59cd57d`

- 핵심: Awake 캐시·OnEnable 구독·Update 입력·FixedUpdate 물리·LateUpdate 카메라·OnDisable 해제를 역할별로 나눈다.
- 검수: 비활성화/재활성화·코루틴 중단·async 취소·직렬화·스크립트와 meta/GUID 연결을 확인한다.
- 한계·교정: 본문의 외부 검사 스크립트는 실행하지 않았다. GetComponent 비용을 무조건 병목으로 단정하지 않고 측정한다.

## 58. unity-input-system

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/unity/unity-input-system/SKILL.md) · 본문 1–180행 전체 읽음 · SHA-256 `8327b121793429b9b4d47813d81170fefa5e401de0020bcb05e026fab0a0c5ed`

- 핵심: Input Actions 자산·액션맵·프로젝트 공용 액션·PlayerInput·수동 액션의 소유와 활성화를 구분한다.
- 검수: 메뉴 중 게임 입력 차단·구독 중복·취소/완료 Dispose·Composite 부위·재바인딩 저장을 검수한다.
- 한계·교정: 1.20은 원문의 패키지 전제이며 설치 버전으로 간주하지 않는다. 버튼의 지속 상태와 클릭의 edge를 용도에 따라 고른다.

## 59. unity-navmesh

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/unity/unity-navmesh/SKILL.md) · 본문 1–165행 전체 읽음 · SHA-256 `e5c5788a9869fe53a4ce596f60489e8942f765cfdd471d723c7a036c41e43157`

- 핵심: NavMeshSurface의 베이크와 NavMeshAgent 실행을 분리하고 에이전트 규격·동적 장애물·분리 섬 링크를 확인한다.
- 검수: 완전/부분/무효 경로·생성 위치·Warp 결과·문 상태·반경/경사·물리 이동 소유를 검수한다.
- 한계·교정: 짧은 HasArrived 예시는 경로 존재와 완전 경로·NavMesh 위 여부까지 보장하지 않는다. 매 프레임 SetDestination 예제와 타이머 권고를 구분한다.

## 60. unity-physics

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/unity/unity-physics/SKILL.md) · 본문 1–189행 전체 읽음 · SHA-256 `e69d408d84a8706813553356d5b9ec49665489dc51689d8b9a0f1c5fbd71646e`

- 핵심: 3D PhysX와 2D 물리를 나누고 고정 스텝의 힘/속도·콜라이더·트리거·레이어·쿼리 정책을 설계한다.
- 검수: 동적/키네마틱 접촉·트리거 포함·레이 시작 위치·고속 통과·수면·복합 콜라이더의 Rigidbody 수를 확인한다.
- 한계·교정: CCD는 모든 형상/움직임 문제의 해결이 아니며 이동 발판에 탑승체가 안정적으로 따라오는지도 실기 확인해야 한다.

## 61. unity-scriptableobjects

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/unity/unity-scriptableobjects/SKILL.md) · 본문 1–143행 전체 읽음 · SHA-256 `5be71efab64b8f1e299f521083bb93a863d231add03c45038b576a317e4f828b`

- 핵심: ScriptableObject는 공유 설정·이벤트·런타임 집합이고 개체별 상태나 저장 파일과 분리한다.
- 검수: 플레이 재진입·Domain Reload 꺼짐·이벤트 해제·런타임 생성 SO 해제·집합 잔류를 검수한다.
- 한계·교정: 뒤에서 순회해도 콜백이 다른 리스너를 제거/추가하면 완전한 재진입 안전성을 보장하지 않는다. 저장 복구 수단으로 오해하지 않는다.

## 62. unity-tilemap-2d

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/unity/unity-tilemap-2d/SKILL.md) · 본문 1–131행 전체 읽음 · SHA-256 `72dc9d553e2e6a831ee286d196c881a128f2e515851c848d9ceb78364065890d`

- 핵심: Grid/Tilemap의 셀 좌표·표시 레이어·대량 쓰기·CompositeCollider2D·규칙 타일을 구분한다.
- 검수: WorldToCell 변환·코너/충돌 틈·활성 레이어·국소 갱신·패키지 존재를 확인한다.
- 한계·교정: 타일맵은 보드 논리의 대체가 아니며 3D 모듈러 배치를 자동 해결하지 않는다. 원문 패키지 설치 단계는 실행하지 않는다.

## 63. unreal-behavior-trees

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/unreal/unreal-behavior-trees/SKILL.md) · 본문 1–125행 전체 읽음 · SHA-256 `bb8a490dd3400a7e895243a000876519e28688dfb9805e1227577e69adc59229`

- 핵심: UE의 Blackboard 기억·Decorator 조건·Service 갱신·Task 작업을 분리하고 AIController가 BT를 시작한다.
- 검수: Observer Aborts, latent 완료/취소, NavMesh, 공유 task의 NPC별 메모리, Blackboard 키 타입을 확인한다.
- 한계·교정: 기존 StateTree에 BT를 자동 추가하지 않는다. UE5.8 API와 PIE 실기는 미검증이다.

## 64. unreal-blueprints

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/unreal/unreal-blueprints/SKILL.md) · 본문 1–124행 전체 읽음 · SHA-256 `96e3cec8fba81a3d845b9e404d6ff8d025cc26c4622a88d36778d5da6cf9350e`

- 핵심: 재사용 Blueprint Class와 레벨 전용 그래프를 나누고 Cast/Interface/Dispatcher를 결합도에 맞춰 선택한다.
- 검수: 중복 바인딩·하드 참조·Tick 필요성·재호출되는 Construction Script·변수 이름 충돌을 확인한다.
- 한계·교정: Construction Script를 오직 편집기에서만 실행한다고 단정한 원문은 부정확하다. 런타임 스폰의 구성 단계도 고려하고 게임 초기화는 BeginPlay로 구분한다.

## 65. unreal-cpp-gameplay

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/unreal/unreal-cpp-gameplay/SKILL.md) · 본문 1–150행 전체 읽음 · SHA-256 `e737ee0d2ba69cbdeb50d10190595eb83848b0b571a93b088b08d426598e38d5`

- 핵심: UE C++ 리플렉션·generated.h·기본 컴포넌트·Gameplay Framework·Build.cs 의존성을 연결한다.
- 검수: UHT 헤더 순서, GC 강/약 참조 의도, 구조 변경 뒤 재인스턴싱, 기본 클래스와 링크 모듈을 확인한다.
- 한계·교정: 모든 UObject 포인터를 강한 UPROPERTY로 바꾸는 것이 정답은 아니다. 약한 참조·노드 메모리 등 수명 계약을 따르고 빌드는 미실행이다.

## 66. unreal-enhanced-input

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/unreal/unreal-enhanced-input/SKILL.md) · 본문 1–133행 전체 읽음 · SHA-256 `f74e82daf48faf94f72f7d16a7b383e5247855dc1c1c68a1bd98fca983c79bad`

- 핵심: Enhanced Input의 IA 값 타입·IMC 우선순위·Modifiers·Triggers를 소유 클라이언트에 연결한다.
- 검수: BeginPlay 이전/이후 possession, respawn, Started/Triggered/Completed 의미, 컨텍스트 제거와 중복 등록을 확인한다.
- 한계·교정: BeginPlay에서 Controller가 항상 있다는 예시 가정은 취약하다. legacy/Combo 폐기 주장은 대상 버전 문서 재확인이 필요하다.

## 67. unreal-niagara

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/unreal/unreal-niagara/SKILL.md) · 본문 1–128행 전체 읽음 · SHA-256 `dfc686f43b5742830ab507aa110fdf00f315151a85d89b2a3a9692082c799246`

- 핵심: Niagara System/Emitter/Module의 실행 순서와 User 노출 파라미터·월드/소켓 스폰·수명을 나눈다.
- 검수: null 반환, CPU/GPU 역할, Fixed Bounds, 루프 종료·auto-destroy·성능·가시성을 확인한다.
- 한계·교정: User는 의도된 외부 제어 인터페이스라는 범위로 이해한다. 모든 내부 파라미터 접근이 절대 불가능하다는 일반 명제나 실행 성공을 주장하지 않는다.

## 68. unreal-packaging

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/unreal/unreal-packaging/SKILL.md) · 본문 1–129행 전체 읽음 · SHA-256 `da853ea07267c6bc98b80bffbcd7b91cbd175eafe151b9887cc5d153c91702d5`

- 핵심: UE 빌드·cook·stage/package·독립 실행을 분리하고 Game Default Map과 포함 자산을 정한다.
- 검수: 실제 패키지 시작맵, 간접 참조 자산, Development/Shipping 차이, 대상 SDK와 staging 산출물을 확인한다.
- 한계·교정: 성공 cook는 실제 플레이 증거가 아니다. UE5.8 Zen/Arm/SDK·로깅 기본값은 프로젝트 설정과 공식 버전 근거 재확인 대상이다.

## 69. phaser-arcade-physics

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/web-engines/phaser-arcade-physics/SKILL.md) · 본문 1–194행 전체 읽음 · SHA-256 `7de2d1bab06517b39cb2bb4d386ae540abaa5a4e57e42f74abea34e79a52d80d`

- 핵심: Phaser Arcade의 직사각/원 바디·속도·collider/overlap·정적 그룹·풀을 나눈다.
- 검수: dt 중복 적용, 정적 바디 이동 후 동기화, 대각선 속도, 지속 collider 재등록, 터널링·풀 회수를 확인한다.
- 한계·교정: Matter와 Arcade 바디는 상호작용하지 않는다. 점프 유지 예시는 착지 즉시 반복 점프하므로 눌림 단발/버퍼 정책과 구분한다.

## 70. phaser-core

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/web-engines/phaser-core/SKILL.md) · 본문 1–204행 전체 읽음 · SHA-256 `889febef63e0c6f11a46f1cc58d11af0dabd63c33ae19c203fc136a928114ebf`

- 핵심: Phaser Scene의 init/preload/create/update·전역 cache·registry·start/launch/sleep/wake를 수명에 맞춰 사용한다.
- 검수: 재시작 초기화, shutdown 연결 정리, 중복 HUD/캔버스, 지연된 Scene 명령과 키업 누락을 확인한다.
- 한계·교정: Phaser3를4로 자동 이관하지 않는다.4.2.1 renderer/키보드 특이사항은 원문 주장이고 브라우저 실행은 하지 않았다.

## 71. pixijs-rendering

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/web-engines/pixijs-rendering/SKILL.md) · 본문 1–225행 전체 읽음 · SHA-256 `7ee0879e02bf239f62770c0d3b3a1db4649e8d84d087fede3659646f469ba0ab`

- 핵심: PixiJS8은 비동기 Application.init와 Assets 로드 후 Container·Sprite·ticker·포인터를 구성한다.
- 검수: deltaTime 배율과 deltaMS 단위, globalpointermove와 바깥 release, backend 실제 선택·공유 텍스처 수명을 확인한다.
- 한계·교정: global 좌표를 중첩 부모의 local position에 그대로 복사하는 드래그 예시는 변환이 필요하다. render group는 화면을 비트맵 캐시하는 것과 다르다.

## 72. threejs-gltf-loading

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/web-engines/threejs-gltf-loading/SKILL.md) · 본문 1–202행 전체 읽음 · SHA-256 `2f1402981f10cc3942eeaf79f10f7a953da4a06b76790bcd9c904a7fcea51c61`

- 핵심: GLTFLoader 비동기 결과·한 루트의 AnimationMixer·압축 decoder와 파일 계층을 연결한다.
- 검수: 클립 0개, 올바른 초 단위 dt, async 실패/취소, decoder 버전·호스팅, 복제 스켈레톤·변환을 확인한다.
- 한계·교정: 장면 문서의 Timer 보정과 달리 본문은 timer.update(time)을 써 내부 차이가 있다. 클립 없는 모델에서 clipAction(undefined)을 피해야 한다.

## 73. threejs-materials-lighting

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/web-engines/threejs-materials-lighting/SKILL.md) · 본문 1–178행 전체 읽음 · SHA-256 `f49abc7e7384600fbe2c084748e327d4d87c028eadcae80e16e00e17de027d7d`

- 핵심: three.js PBR/비조명 재질·직접광/IBL·그림자 스위치·색 공간·출력 변환을 분리한다.
- 검수: albedo sRGB와 데이터맵 NoColorSpace, glTF 자동 설정, shadow frustum, 후처리 OutputPass·과노출을 확인한다.
- 한계·교정: 광원 강도·해상도 숫자는 시작 예시이며 지갑 가죽/금속 수치를 증명하지 않는다. 시각 렌더 검증은 미실행이다.

## 74. threejs-scene-setup

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/web-engines/threejs-scene-setup/SKILL.md) · 본문 1–231행 전체 읽음 · SHA-256 `f6194a390d6a05fd9990db17bcd75e4b2a963c79ce0dff8289dd8deb6e139047`

- 핵심: Scene/Camera/Renderer·import 해석·단일 루프·리사이즈·Timer·해상도 예산을 구성한다.
- 검수: aspect 갱신, 음수/정지 dt, DPR 변화·dispose, WebGL/WebGPU와 GLSL/TSL 호환을 확인한다.
- 한계·교정: Timer/Clock와 backend API는 r186 전제다. dt 상한은 초과시간을 버리므로 현실 시계/저장 만료 계산에는 쓰지 않는다.

## 75. game-jam

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/workflows/game-jam/SKILL.md) · 본문 1–156행 전체 읽음 · SHA-256 `ba3fd961e683dda3d50002fe556b95120d246c4b3849f1200628e1b04c06e7f0`

- 핵심: 잼의 실제 마감·규칙을 확인하고 하나의 핵심 행동→짧은 전체 루프→출하 버퍼로 범위를 제한한다.
- 검수: 시간대·AI/기성자산 허용·라이선스·독립 실행·페이지와 잼 제출 완료를 각각 확인한다.
- 한계·교정: 행사별 규칙·기간·AI정책은 원문 당시 예시다. 읽은 것만으로 최신 규칙/참가 승인/제출 성공을 주장하지 않는다.

## 76. itch-publish

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/workflows/itch-publish/SKILL.md) · 본문 1–162행 전체 읽음 · SHA-256 `906d14fefbc3ef1da60ce96be5cb27aa328bcd3c33449f8a7779a2a67c74cfff`

- 핵심: itch의 페이지/공개 상태와 플랫폼별 채널·portable 빌드·butler 차등 업로드를 구분한다.
- 검수: index.html 위치·대소문자·상대 URL, 실제 실행한 OS 태그, 동일 채널/버전, 공개 전 내용·라이선스를 확인한다.
- 한계·교정: butler 설치/로그인/업로드하지 않았다. 용량/AI공개/결제 정책·명령 지원은 현재 공식 자료 재확인 전 운영 기준으로 확정하지 않는다.

## 77. prototype-fast

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/workflows/prototype-fast/SKILL.md) · 본문 1–119행 전체 읽음 · SHA-256 `35491f7f6c1e94a535098fd40c678369ea94f60905f6f8803b30496f7954881e`

- 핵심: 프로토타입에서 한 질문·시간 제한·관찰 가능한 유지/폐기 기준과 폐기/재사용 의도를 먼저 정한다.
- 검수: 처음 보는 플레이어 행동, 조작/목표/재시작의 작은 루프, 실험 자산 격리와 결과 기록을 확인한다.
- 한계·교정: 무조건 전체 재작성·자동 삭제는 보편 규칙이 아니다. 원본 보존과 실제 승인 범위를 우선하고 이번 실험은 수행하지 않았다.

## 78. steam-publish

[고정 원문](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/19d93f97c9c1ea0f8b306e77aa81e0d3e352d3e9/skills/workflows/steam-publish/SKILL.md) · 본문 1–247행 전체 읽음 · SHA-256 `f3526feceeb5a034102770abe7956f8a1c128def4d10727331ec6e482042111c`

- 핵심: Steam의 페이지 심사·빌드/Depot·Package·분기 공개·최종 출시는 별도 단계로 관리한다.
- 검수: App/Depot ID·실행 경로·보유 패키지·파일 매핑·실제 OS 실행·비공개 베타와 공개 상태를 확인한다.
- 한계·교정: 수수료·대기일·심사·인증·AI공개·SetLive 정책은 당시 원문 주장이다. 비밀번호 명령행 예시는 노출 위험을 보완해야 하며 로그인/업로드/구매는 미실행이다.
