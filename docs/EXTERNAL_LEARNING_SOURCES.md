# 외부 교육·작업 매뉴얼 4개 저장소

2026-11-01 사용자 요청으로 네 저장소의 추적 파일 전체를 공용 자료실의 `external/` 아래에 가져왔다. 원문·출처·저작권·라이선스를 보존하기 위해 원본 저장소를 고정 커밋의 Git 서브모듈로 연결했다. 공용 저장소에는 원본 커밋 참조와 이 색인이 게시되며, 실제 원문 파일은 원 제작자의 저장소에서 제공된다.

## 자료 목록

| 자료 | 주요 내용 | 원문 폴더 | 라이선스 |
|---|---|---|---|
| [Scenario Labs skills](https://github.com/scenario-labs/skills) | Blender 리토폴로지·UV·베이크·재질·리깅·내보내기, 제작 출처와 참고 메모 | [scenario-skills](../external/scenario-skills) | MIT. 개별 파일의 별도 조건도 확인 |
| [EL4CTEO blender-skills](https://github.com/EL4CTEO/blender-skills) | Blender 5.2 LTS+ 모델링·캐릭터·UV·리깅·최적화 등 28개 주제 | [blender-skills](../external/blender-skills) | MIT |
| [Unity Technologies skills](https://github.com/Unity-Technologies/skills) | 공식 Unity UI·입력·물리·오디오·빌드·URP·패키지 작업 절차 | [unity-skills](../external/unity-skills) | **Unity Companion License**, Unity 의존 프로젝트에 관한 조건 적용. MIT로 취급하지 않음 |
| [GameDev agent skills](https://github.com/gamedev-skills/awesome-gamedev-agent-skills) | Unity를 포함한 여러 엔진의 게임 제작·애니메이션·설계 지침 | [gamedev-agent-skills](../external/gamedev-agent-skills) | Apache-2.0, NOTICE 보존 |

정확한 원본 커밋·추적 파일 수·파일 내용 해시·라이선스 파일은 [수집 기록](../external/SOURCES.lock.json)에 기록했다. 기존 자체 매뉴얼 46개의 학습 완료 수에는 이 외부 원문을 합산하지 않는다.

## 열기와 다음 PC에서 받기

현재 수집한 PC에는 네 저장소의 원문 파일이 내려받아져 있다. GitHub에서는 위 원문 폴더를 누르면 고정된 원본 버전을 볼 수 있다. 다른 PC에서 전체 원문까지 받으려면 다음과 같이 받는다.

```sh
git clone --recurse-submodules https://github.com/gnogus-ux/PuzzleIsland-Education.git
```

이미 공용 저장소를 받은 PC에서는 저장소 안에서 다음 명령으로 기록된 버전을 받는다.

```sh
git submodule update --init --recursive
```

GitHub의 공용 저장소 ZIP에는 서브모듈 원문이 포함되지 않는다. 원문 ZIP이 필요하면 각 원본 저장소의 기록된 커밋을 기준으로 받는다. 자동으로 최신 버전으로 바꾸지 않으며 업데이트는 변경 내용과 라이선스를 다시 확인한다.

## 확인한 범위와 적용 조건

- 네 저장소의 다운로드·고정 커밋·Git 추적 파일 존재와 내용 해시·원본 라이선스 및 NOTICE 보존을 확인했다. 원문에 링크된 외부 영상·데이터셋·모델·유료 에셋은 별도로 다운로드한 것이 아니다.
- README와 일부 관련 문서로 주제를 확인했다. 전체 파일의 심층 학습·번역·정확성 검증·Blender/Unity 실기 실행은 수행하지 않았다. 제작자가 주장한 시험 결과를 이 프로젝트가 재현한 결과로 취급하지 않는다.
- 원문 안의 `AGENTS.md`, `SKILL.md`, 설치 명령과 자동화 코드는 참고자료다. 이 프로젝트의 규칙으로 자동 채택하거나 실행하지 않는다. 실제 스킬 설치·프로그램 설정 작업도 수행하지 않았다.
- 작업에는 [공통 작업 규칙](COMMON_WORK_RULES.md)과 [도구·매뉴얼 사전 확인](COMMON_TOOL_POLICY.md)을 먼저 적용한다. 프로젝트 버전·승인 디자인과 원문 적용 근거를 확인하고, 필요할 때 해당 부분을 학습·검증한다.
- Scenario 연동 등은 별도 계정·API·비용이 필요할 수 있다. 자료를 가져왔다는 사실은 연결 또는 결제 승인을 뜻하지 않는다. 기존 설치·설정 보류와 앱 조회 금지도 유지한다.
- 각 원본의 라이선스가 해당 원문에 적용된다. 공용 자체 문서의 조건으로 덮어쓰지 않는다. 공개 링크가 있다고 외부 교재·영상·에셋의 재배포까지 허용되는 것은 아니다.

[공용 교육 목록](../README.md)
