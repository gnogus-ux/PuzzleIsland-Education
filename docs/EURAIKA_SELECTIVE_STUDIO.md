# Euraika 스튜디오 기능 선별 도입 기록

2026-11-04 사용자 지시: Euraika를 사용하되 이미 정한 규칙은 변경하지 않고 쓸만한 규칙만 적용한다. 이 문서는 기존 공통규칙의 개정이 아닌, 별도 보조 스킬의 적용 범위와 검증 기록이다.

## 읽은 원출처

원본은 [Euraika-Labs/Codex-Code-Game-Studios](https://github.com/Euraika-Labs/Codex-Code-Game-Studios/tree/9a182e29f8d9b46394851830ba27213fbe4da950), 고정 commit `9a182e29f8d9b46394851830ba27213fbe4da950`다.

- [README](https://github.com/Euraika-Labs/Codex-Code-Game-Studios/blob/9a182e29f8d9b46394851830ba27213fbe4da950/README.md)와 [설치 가이드](https://github.com/Euraika-Labs/Codex-Code-Game-Studios/blob/9a182e29f8d9b46394851830ba27213fbe4da950/docs/studio/global-install.md): 전체 설치와 선택 적용의 차이, 설치 대상 확인.
- [조율 규칙](https://github.com/Euraika-Labs/Codex-Code-Game-Studios/blob/9a182e29f8d9b46394851830ba27213fbe4da950/docs/studio/coordination-rules.md): 명확한 책임·범위, 유용한 인계, 필요한 맥락만 사용, 상충의 가시화.
- [단계별 검수](https://github.com/Euraika-Labs/Codex-Code-Game-Studios/blob/9a182e29f8d9b46394851830ba27213fbe4da950/docs/studio/director-gates.md): 파일 존재와 실제 다음 작업 준비 상태를 구별.
- 선택한 [project-stage-detect](https://github.com/Euraika-Labs/Codex-Code-Game-Studios/blob/9a182e29f8d9b46394851830ba27213fbe4da950/.agents/skills/project-stage-detect/SKILL.md), [dev-story](https://github.com/Euraika-Labs/Codex-Code-Game-Studios/blob/9a182e29f8d9b46394851830ba27213fbe4da950/.agents/skills/dev-story/SKILL.md), [code-review](https://github.com/Euraika-Labs/Codex-Code-Game-Studios/blob/9a182e29f8d9b46394851830ba27213fbe4da950/.agents/skills/code-review/SKILL.md), [bug-triage](https://github.com/Euraika-Labs/Codex-Code-Game-Studios/blob/9a182e29f8d9b46394851830ba27213fbe4da950/.agents/skills/bug-triage/SKILL.md)의 본문을 읽고 기존 지침과 대조했다.
- [MIT 라이선스](https://github.com/Euraika-Labs/Codex-Code-Game-Studios/blob/9a182e29f8d9b46394851830ba27213fbe4da950/LICENSE): Copyright (c) 2026 Donchitos. 수정한 설치 스킬마다 원출처와 MIT 저작권 고지를 포함했다.

위 자료의 문서 독해·교차 검토와 제한된 설치 검증을 수행했다. 원본의 84개 스킬 전체 학습·50개 에이전트 실행·게임 제작 성능 비교는 수행하지 않았다.

## 설치한 네 기능

| 설치 이름 | 채택한 기능 | 현지화·수정 |
|---|---|---|
| `euraika-stage` | 실제 산출물·검증에 근거한 상태와 다음 준비 조건 파악 | 파일 수·문서 수를 완료율로 간주하지 않음 |
| `euraika-task` | 목표·보존 범위·의존성·완료 기준에 연결한 구현 | 기존 이슈·설계·폴더와 승인 절차 사용 |
| `euraika-review` | 정확성·설계 일치·회귀·검증 가능성 검수 | 실제 결함 우선, 자체 확인과 독립 검수 구별 |
| `euraika-triage` | 버그 영향·긴급도·회귀·다음 최소 조치 정리 | 현재 자료에 없는 일정·용량·배정을 만들지 않음 |

일반 자동 탐색을 허용하되 이 설치본의 적용 대상은 해당 게임 프로젝트로 한정했다. 다른 프로젝트와 독립된 모델 작업에 자동 적용하지 않는다. 새 이름을 사용해 기존 스킬과 충돌을 피했다.

## 제외한 원본 동작

- 루트·하위 AGENTS와 README를 복사하는 전체 bootstrap, 고정 모델·추론·권한 설정, 원본 hooks와 에이전트의 일괄 설치.
- 이미 승인된 작업의 파일별 반복 승인, 자동 담당 생성·위임·외부 메시지.
- 기존 코드를 `src/`로 옮기거나 GDD/TR/ADR/스프린트 파일 이름을 의무화하는 구조 변경.
- 고정 메서드 줄 수·복잡도·파일 개수와 신규 테스트 파일 존재만으로 합격/단계를 결정하는 기준.
- 현재 제품 범위에 없는 Steam 출시 절차 기본 적용.

위 제외 항목을 기존 규칙에 덧붙여 새 금지로 만들지 않았다. 원본에서 가져오지 않은 기능을 기록한 것이다. 현재 사용자 지시와 기존 지침이 계속 적용되며 관련 매뉴얼·참고 확인·3D Guide·정상 점유·검수·비용·앱 제한을 변경하지 않았다.

## 검증 범위

- 공식 Skill Installer로 고정 commit의 네 원본 스킬을 비활성 준비 위치에 가져와 검토한 뒤 수정본을 새 이름으로 설치했다. 전체 upstream 설치 프로그램이나 hooks는 실행하지 않았다.
- Skill Creator의 메타데이터 생성과 quick_validate로 네 스킬 구조를 검사하고 상대 링크·라이선스 고지·설치 파일 해시를 확인했다.
- 검증 도구에 필요한 PyYAML 6.0.3은 작업 전용 의존성 폴더에만 구성했다. 전역 Python 패키지나 모델·권한 설정은 변경하지 않았다.
- 기존 지침·설정·프로젝트 진입 문서 등 보호 대상 8개 파일의 전후 SHA256이 일치했다. 미저장/미커밋 사용자 작업은 보존했다.
- 같은 작성자가 프로젝트 문서와 실제 관련 산출물의 존재를 대조해 상태 확인 절차를 점검했다. 파일 수 기반 단계 판정·새 폴더 이전·앱 실행 없이 다음 검증 범위를 구별했다. 이 확인을 독립 검수나 게임 동작 검증으로 주장하지 않는다.
- 설치된 스킬의 자동 선택은 이 턴에서 관찰하지 않았다. 다음 턴부터 탐색될 수 있으며 실제 자동 호출과 단순 파일 설치는 구별한다. Unity 컴파일·플레이·Android 실기기·외부 서비스·원본 hook 런타임은 미실행이다.

상세 수치와 설치 상태는 [공개 기록](../reports/ToolInventory/20261104_EURAIKA_SELECTIVE.json), 실제 개인 설치 위치·파일별 해시·보존 근거는 담당의 비공개 설치 기록을 따른다.
