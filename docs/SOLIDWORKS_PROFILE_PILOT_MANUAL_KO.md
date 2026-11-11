# SOLIDWORKS 2026 폐폴리라인 시험 부품 검증 절차

2026-11-11 · SOLIDWORKS API Help 2026 SP05 직접 열람 · 현지 실행 대상 Design Premium 2026 SP4.1

## 사전 점검

공용 자료실의 기존 읽기 검사에서 ROT 연결과 동봉 PIA의 typed 호출 근거를 확인했다. 형상 생성, native 저장, 재열기 및 치수 측정은 아래 Dassault Systèmes 원문에서 관련 정의, 매개변수, 반환값, Remarks와 필요한 예제를 읽고 적용했다. [기존 세션 읽기 검증](SOLIDWORKS_READONLY_API_VERIFICATION.md) · [공용 도구 목록](AVAILABLE_TOOLS.md)

1. 입력은 단위와 축이 명시된 순서형 폐루프 한 개, 출처 리비전/해시, 양수인 시험 두께를 가진다. 스케치와 같은 좌표계에서 원점, 축, 단위를 확정하고 가이드를 작성한다. 정점 수·루프 닫힘·중복/자가교차·면적·최소 변 길이·경계 치수를 입력 바이트에서 계산한다. 디지털 치수와 실물/제조 검증을 구분한다.
2. 사용자 소유 기존 SOLIDWORKS가 단일 정상 프로세스일 때 Windows PowerShell 5.1 64비트 STA에서 `Marshal.GetActiveObject`로 붙는다. 동봉 `sldworks` 및 `swconst` PIA의 typed 인터페이스를 사용한다. 기존 문서 수와 활성 상태를 먼저 확인한다. 문서 생성에는 기존 `.PRTDOT` 절대 경로를 `NewDocument`에 명시하고, 사용자 템플릿 설정과 원본 문서를 유지한다.
3. 기본 평면은 현지화된 이름에 의존하지 않고 참조 평면의 transform으로 식별한다. 활성 스케치의 model-to-sketch 변환을 사용한다. `CreateLine`은 활성 스케치에서 선분을 만든다. `AddToDB`로 자동 스냅을 차단하여 입력 좌표를 보존하고, `DisplayWhenAdded`로 중간 표시를 줄인다. 두 속성은 `finally`에서 원래 값으로 되돌린다. 선분을 마지막 점에서 첫 점까지 연결한다.
4. `FeatureExtrusion3`은 스케치 평면에서 시작하는 단방향 블라인드 보스로 지정한다. D1은 미터 단위다. 드래프트 및 시작 오프셋을 끄고, 평면의 실제 법선에 따라 의도한 +Z 방향을 확인한다. 돌출 기능과 단일 솔리드, 스케치 선분 좌표, 여섯 방향 극값, 돌출 깊이를 파일 저장 전에 대조한다. 검수의 기하 허용차는 디지털 입력 대조용이다.
5. 활성 문서가 소유 시험 문서인지 확인하고 선택을 비운 뒤 `.SLDPRT` 신규 경로로 `SaveAs3`를 실행한다. 반환값과 오류/경고 마스크를 기록한다. 저장 API는 기존 경로를 덮어쓸 수 있으므로 미존재 파일만 받는다. 시험 문서만 이름과 경로를 확인하여 닫고, 경로가 더 이상 열린 문서에 없음을 확인한다. 동일 파일을 `OpenDoc6`으로 디스크에서 읽기 전용 재열기하고 같은 검사를 시행한다. 검수 완료 후 소유 시험 문서를 닫고 기존 세션 상태와 파일 해시를 다시 대조한다.
6. 재열기 부품에 대해서만 정면과 등각 보기를 설정하고 `SaveBMP`를 실행한다. 저장 그림은 실제 SOLIDWORKS 뷰로 표기한다. 입력 폴리라인으로 생성한 Guide는 출처 도식으로 표기한다. 출력 이미지의 디코딩과 실제 형상을 확인한다.

## 직접 읽은 원문과 대조

- 스케치 세션 및 `CreateLine`의 활성 스케치 요구, `AddToDB`와 스냅 우회. 공식 C# 연결 예제는 객체를 새로 만들고 구형 돌출 메서드를 사용한다. 실기에서는 기존 ROT 연결과 `FeatureExtrusion3`를 적용한다. [연결 C# 예제](https://help.solidworks.com/2026/English/api/sldworksapi/Connect_to_SOLIDWORKS_Session_CSharp.htm) · [CreateLine](https://help.solidworks.com/2026/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.ISketchManager~CreateLine.html) · [AddToDB](https://help.solidworks.com/2026/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.ISketchManager~AddToDB.html) · [ModelToSketchTransform](https://help.solidworks.com/2026/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.ISketch~ModelToSketchTransform.html)
- 보스 생성의 방향, 블라인드 종료, API 미터 단위와 반환 Feature. 깊이 정의와 솔리드의 정확한 축별 외곽을 서로 대조한다. [FeatureExtrusion3](https://help.solidworks.com/2026/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.IFeatureManager~FeatureExtrusion3.html) · [GetDepth](https://help.solidworks.com/2026/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.IExtrudeFeatureData2~GetDepth.html) · [GetBodies2](https://help.solidworks.com/2026/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.IPartDoc~GetBodies2.html) · [GetExtremePoint](https://help.solidworks.com/2026/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.IBody2~GetExtremePoint.html)
- 신규 명시 템플릿, native 저장의 활성 문서/오류·경고/덮어쓰기 주의, 재열기 옵션과 이미 열린 메모리 문서의 동작. `CloseDoc` 문서는 숨은 비활성 문서도 닫을 수 있다고 명시한다. 기존 열린 문서가 0이고 소유 시험 문서 하나만 열렸음을 확인한 경우 이 메서드를 사용할 수 있다. [NewDocument](https://help.solidworks.com/2026/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.ISldWorks~NewDocument.html) · [SaveAs3](https://help.solidworks.com/2026/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.IModelDocExtension~SaveAs3.html) · [OpenDoc6](https://help.solidworks.com/2026/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.ISldWorks~OpenDoc6.html) · [CloseDoc](https://help.solidworks.com/2026/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.ISldWorks~CloseDoc.html) · [QuitDoc](https://help.solidworks.com/2026/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.ISldWorks~QuitDoc.html)
- 현재 뷰의 실제 BMP 출력, 파일명·크기와 성공 반환. 모델 표시 단위는 `GetUnits`로 읽고 API에서 측정한 좌표는 SI 스케일을 확인해 별도로 mm로 변환한다. 솔리드 질량 속성 배열의 인덱스 3은 부피이며, 출처 외곽 면적×두께와 대조한다. [SaveBMP](https://help.solidworks.com/2026/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.IModelDoc2~SaveBMP.html) · [BMP C# 예제](https://help.solidworks.com/2026/English/api/sldworksapi/Save_Model_as_Bitmap_Example_CSharp.htm) · [GetUnits](https://help.solidworks.com/2026/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.IModelDoc2~GetUnits.html) · [GetMassProperties](https://help.solidworks.com/2026/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.IBody2~GetMassProperties.html)

실제 설치 PIA에서 `SaveAs3`, `OpenDoc6`, `ActivateDoc3`의 오류·경고 인수는 in/out이다. typed C#의 `ref`를 적용하고 초기값을 지정한다. 온라인 C# 표기의 `out`을 그대로 복제하면 해당 설치 PIA로 컴파일하지 못한다. 공식 페이지 열람에는 ego-browser의 동일 TaskSpace에서 3라운드를 사용했으며 마지막 라운드에서 정상 종료했다.

## 오류와 범위

소유 문서 식별, 스케치·보스 생성, 단일 솔리드/경계 검사, 저장, 닫힘, 재열기 중 선행 조건이 실패하면 다음 단계로 진행하지 않는다. 반환값·HRESULT와 진행 중 문서/디스크 상태를 기록하고 정상 해제를 확인한다. 연결 종료 상태가 불명확하면 중복 CAD 실행을 보류한다. 사용자 직접 사용권·보안·로그인 단계는 앱의 정상 절차를 따른다. 문서 기반 절차와 현지 실기 결과를 별도 기록한다. 범위는 단일 폐폴리라인, native 솔리드, 재열기 및 디지털 치수 대조다.

## 2026-11-11 현지 실기 범위

- Design Premium 2026 SP4.1 / API Revision 34.4.1 / 동봉 PIA 34.4.1.1011에서 단일 기존 사용자 제어 세션을 사용했다. 저장 시작 전 열린 문서 수는 0이었다. PowerShell 5.1 64비트 STA의 typed 호출을 검증했다.
- 출처 폐폴리라인을 한 스케치로 구성하고 단방향 블라인드 보스와 솔리드 한 개를 만들었다. 저장 전과 디스크에서 읽기 전용으로 재열기한 뒤 모든 스케치 선분의 끝점, 모델 표시 단위 mm, 6방향 극값, 피처 깊이, 부피를 대조했다. 저장과 재열기 오류 및 경고 마스크는 각각 0이었다. native 파일 원바이트 해시는 재열기 전후 동일했다.
- 재열기 부품의 정면과 등각 뷰를 `SaveBMP`로 생성하고 실제로 두 이미지를 열어 확인했다. 저장·재열기 때 각 시험 문서만 닫았고 기존 앱 세션과 템플릿을 보존했다. 사용자 문서가 함께 열린 상황의 `QuitDoc` 분기, 다른 SOLIDWORKS 버전, 다중 부품·스플라인, 실물 치수·재료·제조 적합성은 별도 검증 범위다.

## 격리 PC 검토

브라우저 검수에서 재열기한 모델의 실제 CAD 미리보기가 검토 화면에 표시됐다. 내려받은 native 파일은 SOLIDWORKS 저장본과 SHA256이 같았고 검증 기록도 다운로드됐다. 검토자가 선택한 도면 리비전과 외곽, CAD 파일 지문을 참조하는 수정 요청 초안 1건을 저장하고 내보냈다. 요청은 미처리·미전달 상태이며 자동 CAD 생성과 수정 적용은 실행 범위 밖이다. 격리 PC 시험으로 한정했고 운영 환경과 휴대전화는 이 시험에 사용하지 않았다. [익명 실기 기록](../reports/ToolInventory/20261111_SOLIDWORKS_PROFILE_PILOT_SCOPED_RUNTIME.json)
