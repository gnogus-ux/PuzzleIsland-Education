# 매치3 · Unity 6 적용 전 호환 대조

[통합 매뉴얼](MATCH3_WORKFLOW.md) · 2026-11-01. **현재 상태: 강좌/프로젝트 정적 대조 완료, Unity 6.3 공식 웹 문서 재확인 대기, Editor·Android 실행 미실행.** 이 페이지를 ‘Unity 6.3에서 실행 검증된 이식 가이드’로 사용하지 않는다.

## 확인한 기준

학습 시 적용 대조 대상으로 정한 환경은 Unity `6000.3.27f1`/URP `17.3.0`이다. 각자의 프로젝트에서 고정 버전·화면 방향·보드 크기를 다시 확인한다. 강좌는 Taft의 Unity2017/2018, Catlike의2022.3.2f1, Winterbolt 화면의2021.1.9f1, git-amend 저장소의2022.2.14f1이다. 오래된 SDK/JDK 다운로드·InputManager·패키지 버전·씬 설정을 그대로 적용하지 않는다.

이번 공개본에서는 현행 공식 웹 문서의 재대조를 완료하지 못했다. 해당 문서를 읽었다고 기록하지 않았다. 아래 표는 **완료된 공식 호환 판정이 아닌 확인 목록**이다.

## 항목별 대조표

| 강좌에서 확인한 것 | 프로젝트에 적용할 때 확인할 것 | 이번 작업의 판정 |
|---|---|---|
| OnMouseDown/Up, Input.mousePosition | 현재 Active Input Handling, Collider/카메라 조건, UI 위 월드 입력, 터치 취소 | 강좌 관찰 완료 / 현행 API·기기 미검증 |
| git-amend PlayerInput 1.5.1 Select/Fire | 현재 고정 패키지의 API·Actions·UI 입력 모듈·구독/해제 수명 | 강좌/저장소 확인 / 새 패키지 설치 없음 |
| ScreenToWorldPoint, XY/XZ converter | z 깊이, ray-보드 평면 교차, RectTransform/Canvas/Safe Area | 좌표 원리 정리 / 실제 화면 변환 미실행 |
| FindObjectOfType·FindWithTag | 해당 Unity 버전의 지원/대체 API, 일회 주입·참조 검증 | 자동 일괄 치환 안 함 |
| Awake/OnEnable/Start 초기화 | 같은 객체와 다른 객체의 호출 순서, 씬 로드·inactive·singleton | P43 발화와 P47 초기화 문제 기록 / 공식 대조 대기 |
| ScriptableObject Level/Goal/Item | 원본 정의와 세션 상태 복사, Editor 변경과 플레이어 저장의 차이 | P45 수집값 잔류 관찰 / 현재 엔진 동작 미실행 |
| coroutine/WaitForSeconds | 주 스레드·재진입·시간배율·씬 종료, 실제 완료 신호 | ‘별도 스레드/자동 busy’ 설명 배제 / 현행 문서 대기 |
| DOTween Sequence/AsyncWaitForCompletion | 사용하는 버전의 완료/kill/cancel·autoPlay·autoKill·UI 모듈·IL2CPP | 두 강좌의 서로 다른 설정 확인 / 설치·실행 안 함 |
| BinaryFormatter/persistentDataPath | 현행 .NET/Unity 지원·보안·대체 직렬화, 필드 검증·원자 저장 | 예제 방식을 새 저장 설계로 채택 안 함 / 공식 근거 대조 대기 |
| OnDisable/OnApplicationQuit 저장 | 앱 중단·프로세스 종료·저장 완료·실패 복구 | 종료 콜백만 의존하지 않는 설계 제안 / 기기 미검증 |
| 수동 Android Studio/JDK8/SDK 경로 | Unity Hub의 해당 Editor Android 모듈·SDK/NDK/JDK·지원 API/ABI | 2018 절차를 현행 설치법으로 소개하지 않음 |
| Android external write 설정 | app-specific 저장 경로·실제 권한·백업/재설치 동작 | 권한 추가 요구 안 함 / Android 공식 대조 대기 |
| Resources.LoadAll·pool·Unity Random | 빈 리소스·빌드 포함·리로드·메모리·결정적 PRNG 분리 | 강좌 구현과 한계 문서화 / 프로파일링 없음 |
| Sprite/Particle/Material | 현재 URP 셰이더·정렬·투명도·sprite atlas·기기 비용 | 예제 자산 편입/렌더 검증 없음 |
| 구식 UI Text·Canvas 값 | 현재 TMP/UGUI 버전·폰트·레이아웃·Safe Area·가로 Rect | 고정 세로 카메라 비율을 재사용하지 않음 |

## 공식 문서에서 확인할 질문

- [Unity 6.3 매뉴얼](https://docs.unity3d.com/6000.3/Documentation/Manual/index.html): 이벤트 호출 순서, coroutine, ScriptableObject/직렬화, Android 환경 설정과 입력.
- [Unity Input System 공식 문서](https://docs.unity3d.com/Packages/com.unity.inputsystem@latest/): 실제 프로젝트의 고정 패키지 버전으로 들어가 PlayerInput·UI 연동·pointer/touch 정책 대조. latest만 보고 버전 적합을 확정하지 않는다.
- [Microsoft BinaryFormatter 보안 안내](https://learn.microsoft.com/en-us/dotnet/standard/serialization/binaryformatter-security-guide): 현재 권고와 마이그레이션 범위 확인. 이 링크는 이번 브라우저 오류 뒤 본문 열람에 성공하지 못한 **대조 대상**이다.
- [DOTween 공식 문서](https://dotween.demigiant.com/documentation.php): 프로젝트가 선택한 버전의 Sequence·completion·kill·async 지원 확인.

위 링크는 확인 대상을 지정한 것이며 새로 읽은 근거로 인용한 목록이 아니다. 대조를 재개하면 실제 URL·문서 버전·확인 시점·지원하는 주장·미검증 경계를 보고서에 추가한다.

## 실행 검증은 별도다

공식 API 문서와 코드가 일치해도 실제 컴파일·프리팹 참조·애니메이션·터치·저장·IL2CPP 동작은 미입증이다. 필요한 변경이 승인되면 격리 후보에서 좁은 컴파일/규칙 검사→Editor 장면→대상 Android 순으로 확인하고, 실제 실행 결과를 이 교육 기록과 분리한다. 이번 문서 작업을 이유로 Unity를 켜거나 패키지를 올리거나 저장 형식을 바꾸지 않았다.
