# SOLIDWORKS 기존 세션 읽기 전용 API 확인

2026-11-11. Windows/SOLIDWORKS 2026 대상의 제한 확인 절차. 문서 열람·설치 확인·실제 앱/API 응답을 분리한다.

## 목적과 사전 확인

설치/서명·COM 등록, 실제 편집기 진입, 외부 프로그램의 읽기 전용 COM 응답을 구별한다. 사용자 지시 없이 새 문서·모델/도면 변경·저장·종료·설정/레지스트리 변경·사용권 활성화·로그인·설치/수리를 하지 않는다. Windows 앱 조작에는 computer-use의 실제 반환 창과 최신 상태를 사용한다.

1. 해당 SOLIDWORKS의 기존 프로세스/창 유무를 먼저 확인한다. 실행 중이면 같은 세션을 사용하며 중복 실행하지 않는다.
2. 사용자가 설치한 실행 파일의 버전/서명을 확인하고 정상 시작한다. 보안/인증/사용권·개인정보 동의가 작업을 막으면 사용자 직접 처리를 요청한다. 등록·설정 변경으로 우회하지 않는다.
3. 단일 실제 편집기가 준비된 뒤 Windows PowerShell/.NET Framework의 STA 프로세스에서 `Marshal.GetActiveObject("SldWorks.Application")`로 ROT에 있는 실행 객체만 얻는다. 생성자를 호출해 두 번째 서버를 만들지 않는다.
4. 설치본의 `api/redist/SolidWorks.Interop.sldworks.dll`을 참조한 C#의 `ISldWorks` 형식으로 `RevisionNumber()`와 `GetDocumentCount()`를 읽는다. 첫 메서드는 설치 버전 문자열, 두 번째는 해당 세션의 열린 문서 수다. OS의 단일 SOLIDWORKS 프로세스와 화면/버전을 대조한다. 다중 인스턴스면 첫 객체를 임의 선택하지 않는다. 외부 패키지/새 SDK 설치는 필요하지 않았으며 제공된 PIA만 사용했다.
5. COM 참조만 해제하고 앱/문서는 그대로 둔다. 결과에는 버전, 성공/실패, 문서 수, 필요한 프로세스 식별만 기록하고 파일 내용·사용권 번호·인증정보를 수집하지 않는다.

## 적용 근거와 실제 열람 범위

아래 공식자료의 직접 열람과 실기는 기존 API 확인 담당이 수행했다. 후속 게시 담당은 저장된 결과와 이 매뉴얼을 대조했으며 새 앱/API 실행이나 추가 원문 학습을 수행하지 않았다.

- [Connect to SOLIDWORKS Session, C# / 2026](https://help.solidworks.com/2026/English/api/sldworksapi/Connect_to_SOLIDWORKS_Session_CSharp.htm): 연결 예제와 STA/ISldWorks 사용 부분을 읽었다. 예제의 스케치·돌출·선택 코드는 읽기 검사에 적용하지 않는다. 예제는 새 객체를 생성하므로 기존 세션 연결에는 아래 ROT 근거를 사용한다.
- [RevisionNumber / ISldWorks / 2026](https://help.solidworks.com/2026/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.ISldWorks~RevisionNumber.html): 정의·반환형·버전 해석 Remarks를 읽었다. 파일 빌드 번호와 API 버전 문자열은 별도 기록한다.
- [GetDocumentCount / ISldWorks / 2026](https://help.solidworks.com/2026/English/api/sldworksapi/SOLIDWORKS.Interop.sldworks~SOLIDWORKS.Interop.sldworks.ISldWorks~GetDocumentCount.html): 정의·정수 반환·열린 문서 수 의미와 가용성을 읽었다. 문서를 열거나 파일 경로를 전수 조회하는 호출은 하지 않는다.
- [Microsoft Marshal.GetActiveObject / .NET Framework 4.8.1](https://learn.microsoft.com/en-us/dotnet/api/system.runtime.interopservices.marshal.getactiveobject?view=netframework-4.8.1): ROT 연결 정의, 미등록 객체 예외, ProgID/CLSID 해석을 읽었다. 기본 PowerShell의 런타임 차이를 가정하지 않고 .NET Framework 제공 Windows PowerShell을 사용한다.

공식 API 페이지는 2026 SP05 문서이며 실제 설치 서비스팩/빌드는 현지 결과로 확인한다. 문서 열람은 실제 앱/API 성공을 뜻하지 않는다. 형상 생성·저장/재열기·교환 파일·애드인·메이 제품 연동·제조 적합성은 이 제한 검사에서 검증하지 않는다.

## 2026-11-11 한정 실기와 해석

실제 화면은 SOLIDWORKS Design Premium 2026 SP4.1, 실행 파일/동봉 PIA는34.4.1.1011이었다. Windows PowerShell5.1/.NET Framework의64bit STA에서 기존 객체를 얻고 형식 지정된 `ISldWorks`의 두 getter를 호출해 버전34.4.1·열린 문서0을 확인했다. 앱/문서는 열어 둔 채 COM 참조만 해제했다.

초기 실행 도구는 대상 창을 얻지 못했고 직접 실행도 splash 이후 종료됐다. 종료 원인과 종료코드는 미확인이다. 사용자가 메인 화면을 연 뒤 실제 화면과 단일 프로세스를 확인해 연결을 재개했다. 자동 시작의 안정성까지 통과로 주장하지 않는다.

실행 세션이 없을 때 `GetActiveObject`는0x800401E3으로 실패했다. 실행 후 객체 연결은 성공했지만 PowerShell 기본 late binding의 첫 getter는0x8002802B로 실패했다. 같은 세션에 대해 동봉 PIA를 참조한 C# typed 호출은 성공했다. 이 관찰은 레지스트리/라이선스 손상이라는 단정 근거가 아니며 등록 재작성이나 수리를 하지 않았다.

형식 지정 호출의 핵심은 다음과 같다. 공식 예제의 모델링/새 객체 생성 부분은 포함하지 않는다.

```csharp
ISldWorks app = (ISldWorks)Marshal.GetActiveObject("SldWorks.Application");
string version = app.RevisionNumber();
int count = app.GetDocumentCount();
```

프로브 컴파일 임시 폴더는 해당 검사 프로세스에만 지정했다. 시스템/사용자 전역 TEMP·설정은 변경하지 않았다. 새 COM 서버 생성·문서 열기/수정/저장/종료·라이선스/레지스트리 변경은0이다. 이 결과는 기본 외부 읽기 COM 접속이며 MAY 서비스의 실제 모델 생성 연동이나 CAD 내보내기 성공이 아니다.

[익명 범위별 실행 기록](../reports/ToolInventory/20261111_SOLIDWORKS_READONLY_API_SCOPED_RUNTIME.json) · [공용 도구 목록](AVAILABLE_TOOLS.md)
