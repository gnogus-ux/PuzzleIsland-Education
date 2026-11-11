# SOLIDWORKS 재열기 바디와 WebGL 회전 검토

2026-11-11 · SOLIDWORKS Design Premium 2026 SP4.1, 동봉 PIA 34.4.1.1011, WebGL 2.0

승인된 단일 폐외곽을 네이티브 부품으로 저장하고, 같은 구성으로 읽기 전용 재열기한 솔리드의 면을 브라우저에서 회전해 검토하는 절차다. 스케치, 블라인드 보스, 저장 및 측정에는 앞선 절차를 적용한다. [SOLIDWORKS 폐외곽 시험 부품](SOLIDWORKS_PROFILE_PILOT_MANUAL_KO.md)

## 저장본과 메시 연결

1. 입력은 단위와 원점이 확정된 단일 선분 루프다. 점 순서·끝에서 처음으로 이어지는 닫힘·중복·자가교차·두께와 대상 리비전을 확인한다. Guide에는 유지할 경계, 축 변환, 새 두께 방향, 보존할 문서를 표시한다.
2. 사용자 소유 기존 SOLIDWORKS의 단일 세션을 사용한다. Windows PowerShell 5.1 64비트 STA와 동봉 PIA의 typed COM으로 연결하고 열린 문서 목록 및 활성 문서를 기록한다. 새 경로에 저장한 작업 소유 부품을 닫은 뒤 `OpenDoc6`으로 저장한 구성명을 지정해 읽기 전용 재열기한다. 실제 구성과 읽기 전용 플래그, 단일 솔리드, 외곽 선분, 여섯 극값, 돌출 깊이와 부피를 확인한다.
3. 재열기 솔리드에서 `IBody2.GetTessellation(null)`을 얻는다. `NeedFaceFacetMap`과 `ImprovedQuality`를 사용하고 공유 경계의 facet topology match를 지정한다. `Tessellate` 성공 후 크기를 먼저 검사하고 면의 facet, facet의 fin 세 개, fin의 vertex ID와 XYZ 좌표를 읽는다.
4. 세 fin의 끝점 연결에서 삼각형 순서를 구한다. mm로 변환한 좌표가 유한하고 면적이 양수인지 확인한다. 외적과 `IFace2.Normal`을 대조해 바깥 방향으로 인덱스를 정렬한다. `FaceInSurfaceSense`는 기저 surface 법선과 face 법선의 관계를 설명한다. 면별 삼각형의 합과 CAD 면적, 바디 극값과 메시 경계, 바디 부피와 메시의 부호 있는 부피를 대조한다. 각 CAD facet이 한 번 사용됐는지 확인한다.
5. 소유 문서만 닫고 원래 문서·활성 상태와 프로세스, 저장본 및 템플릿의 보존을 확인한다. 정점·인덱스·mm 경계, 산출물 길이와 해시를 같은 작업의 검증 기록에 연결한다. 해제 상태를 확인한 뒤 완료를 기록한다. 실행이 지연되거나 연결이 끊겼다면 원격 실행이 끝났는지 확인한 뒤 다음 작업을 시작한다.

## 브라우저 검토

1. 응답을 요청 당시 저장 리비전과 현재 선택에 대조한다. 선택이 바뀌면 이전 응답으로 화면을 열지 않는다. 해당 native 파일과 같은 작업에서 검증한 메시의 바이트 길이·해시·단위·유한 좌표·인덱스 범위를 확인한다.
2. WebGL 2.0에서 vertex array, position buffer, index buffer를 만들고 `UNSIGNED_INT` 인덱스로 `drawElements`를 실행한다. 깊이 테스트를 사용한다. 평면 삼각형의 화면 미분으로 계산한 법선을 조명에 사용한다. 모델 경계 중심으로 회전과 확대를 적용하며 카메라 비율은 그리기 영역 크기와 맞춘다.
3. 캔버스에 한정해 포인터 캡처·취소·회전·핀치를 처리한다. 그리기 크기가 양수일 때 DPR 상한을 적용하고 변경이 있을 때 프레임을 요청한다. 뷰를 닫으면 GPU 버퍼·프로그램·입력 리스너·관찰자를 해제한다.
4. 실제 검수에서 기본 등각과 정면, 회전 전후의 화면·카메라 변화, 파일 내려받기의 바이트 대조를 확인한다. WebGL 오류가 있더라도 검증된 네이티브 파일 및 기록은 열거나 내려받을 수 있게 한다. 브라우저 회전은 검토용 카메라의 상태다.

## 공식 자료 열람 범위

- CAD 담당이 설치된 2026 API Help에서 **Tessellate a Body (C#)**의 단일 바디 분기, `IBody2.GetTessellation`의 전체 바디 옵션, `ITessellation`의 면 매핑·facet/fin/vertex 반환형과 품질 설정을 직접 읽었다. 예제의 별도 스케치 편집은 생략한다. fin 연결로 삼각형 순서를 얻은 후 face 법선으로 방향을 확인한다. [Dassault Systèmes C# 예제](https://help.solidworks.com/2026/English/api/sldworksapi/Tessellate_a_Body_Example_CSharp.htm) · [GetTessellation](https://help.solidworks.com/2026/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.IBody2~GetTessellation.html) · [GetFaceFacets](https://help.solidworks.com/2026/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.ITessellation~GetFaceFacets.html)
- CAD 담당이 `IFace2.Normal`, `FaceInSurfaceSense`와 `GetArea`의 평면 법선·방향·제곱미터 면적 정의를 직접 확인했다. `GetArea`는 근삿값이다. 표시용 `GetTessTriangles`의 float 배열과 분석용 바디 테셀레이션의 double XYZ를 구분한다. 설치본의 API 반환 좌표 단위는 같은 솔리드의 독립 극값으로 대조한다. [Face Normal](https://help.solidworks.com/2026/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.IFace2~Normal.html) · [FaceInSurfaceSense](https://help.solidworks.com/2026/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.IFace2~FaceInSurfaceSense.html) · [GetArea](https://help.solidworks.com/2026/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.IFace2~GetArea.html) · [GetTessTriangles](https://help.solidworks.com/2026/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.IFace2~GetTessTriangles.html)
- CAD 담당이 `OpenDoc6`의 구성명·로드 옵션, `IsOpenedReadOnly`의 플래그, `QuitDoc`의 소유 문서 닫기와 `ActivateDoc3`의 재빌드 제어를 직접 읽었다. 빈 구성명은 마지막 사용 구성을 선택한다. 열린 파일은 먼저 작업 소유 문서의 닫힘을 확인해야 디스크 왕복을 대조할 수 있다. [OpenDoc6](https://help.solidworks.com/2026/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.ISldWorks~OpenDoc6.html) · [IsOpenedReadOnly](https://help.solidworks.com/2026/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.IModelDoc2~IsOpenedReadOnly.html) · [QuitDoc](https://help.solidworks.com/2026/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.ISldWorks~QuitDoc.html)
- UI 담당이 Khronos WebGL 2.0 규격의 컨텍스트, 정점 배열 객체, 버퍼 바인딩과 OpenGL ES 3의 인덱스 그리기, 깊이 테스트 및 미분 정의를 직접 읽었다. GLSL ES PDF의 본문은 열람 범위에서 제외했다. [WebGL 2.0](https://registry.khronos.org/webgl/specs/latest/2.0/) · [glDrawElements](https://registry.khronos.org/OpenGL-Refpages/es3.0/html/glDrawElements.xhtml) · [glEnable](https://registry.khronos.org/OpenGL-Refpages/es3.0/html/glEnable.xhtml) · [dFdx·dFdy](https://registry.khronos.org/OpenGL-Refpages/es3.0/html/dFdx.xhtml)
- UI 담당이 MDN의 자원 해제, blocking 호출, 확장과 DPR 관련 절을 직접 읽었다. 입력·복귀·처리 상태는 기존 터치와 화면 전환 지침을 적용한다. [MDN WebGL 모범 사례](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/WebGL_best_practices) · [PC 웹 터치](ANDROID_PC_WEB_CONTROL.md) · [버튼 상태](UI_BUTTON_STATE_FEEDBACK.md) · [작업 공간과 복귀](WORKSPACE_SELECTION_RETURN.md)

## 확인 범위

기존 사용자 문서가 열린 세션에서 네이티브 저장·같은 구성 읽기 전용 재열기·실제 바디 테셀레이션·작업 문서 정상 닫기를 확인했다. 저장 파일과 메시를 별도로 읽어 유한 좌표·유효 인덱스·삼각형 면적·경계·부피 및 공유 모서리 방향을 대조했다. 기존 활성 문서, 프로세스 및 템플릿의 보존을 확인했다. [익명 실기 기록](../reports/ToolInventory/20261111_SOLIDWORKS_REOPENED_MESH_SCOPED_RUNTIME.json)

비대화형 Windows PowerShell 자식 실행에서 `Get-FileHash` 자동 로드에 실패하면 `$PSHOME`의 기본 Utility 모듈을 명시적으로 불러온다. 이 실행 방식에서 해시·JSON·동봉 PIA 컴파일과 형상 검증까지 CAD 연결 전에 확인했다.

### 격리 PC 브라우저 실기

독립 CAD 실기와 다른 저장 부품을 선택하고 생성 버튼을 한 번 눌렀다. 기존 사용자 SOLIDWORKS 세션에서 새 파일을 저장한 뒤 디스크에서 읽기 전용 재열기하고 실제 바디를 테셀레이션했다. 기존 열린 문서와 활성 상태가 복귀했고 작업 점유를 정상 해제했다. 검증된 메시가 PC WebGL 2.0 검토 화면에 자동으로 표시됐다.

드래그 회전과 휠 확대를 화면과 카메라 상태로 대조했다. 정면·등각 전환, 도면으로 돌아가기, 브라우저 새로고침 뒤 저장된 3D 다시 열기를 확인했다. 브라우저에서 내려받은 부품 파일의 해시가 저장본과 일치했다. 파일과 저장 리비전에 연결된 시험 수정 요청 초안을 저장하고 내보냈으며 도면과 이력은 그대로였다.

첫 자동 요청은 자식 Windows PowerShell의 해시 명령 자동 로드가 실패해 COM 연결 전에 끝났다. 원래 영수증을 보존하고 작업 해제를 확인했다. 기본 모듈을 명시적으로 불러오도록 고친 뒤 재요청했으며, 이 재요청이 브라우저에서 실제 CAD를 호출한 한 건이다. 독립 CAD 실기는 별도 실행이다.

지원 범위는 단일 닫힌 선분 외곽의 평면면 솔리드다. 시험 작업기의 부품 식별자는 영문자·숫자·밑줄·하이픈을 지원한다. 다른 형상과 식별자 규칙, 운영 서비스와 외부 TLS·휴대전화, 실물 치수·재료·제조 적합성은 별도 검증 범위다.
