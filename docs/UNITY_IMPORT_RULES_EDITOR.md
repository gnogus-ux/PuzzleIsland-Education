# Unity 가져오기 규칙 에디터 확장 — AssetPostprocessor·ModelImporter·TextureImporter·URP Lit·EditMode 테스트

2026-11-22 · Claude 작성. 블렌더·Painter에서 만든 모델과 텍스처를 Unity에 넣을 때 축·크기·이름·텍스처 설정·URP 재질 연결을 자동으로 맞추는 **에디터 확장**을 만들 때 쓰는 매뉴얼이다. [Blender→Unity 인계](MODULAR_MAP_BLENDER_UNITY.md)(수동 왕복 점검), [Unity 공식 SKILL 학습](UNITY_OFFICIAL_SKILLS_WORKFLOW.md)(CLI·패키지 실행 경계)와 함께 본다.

**상태:** Unity 공식 문서 3종을 읽고 쓴 학습본에, 내부용 도구 제작 중 실제 Unity 6000.3/6000.6에서 확인한 내용('실기 기록')을 더했다. 실기 기록에 없는 것은 미검증이다.

## 1. 적용 환경

- 문서 기준: Unity **6000.6.7f1** 설치본에 들어 있는 오프라인 문서(`Editor/Data/Documentation/en/`). 6000.3에는 오프라인 문서가 설치돼 있지 않아 같은 API가 있는지는 **컴파일로 확인**한다.
- 렌더 파이프라인: URP만 다룬다. Unity 7에서 Built-in이 빠지고 HDRP가 종료 예정이므로 새 도구는 URP 전용으로 만든다.
- 블렌더 FBX의 실제 축·크기 값(예: 루트 −90°, 100배)은 파일마다 다를 수 있다. 문서에는 블렌더별 수치가 없으므로 **실제 파일을 넣어 보고 확인**한다.

## 2. 가져오기 단계와 어디서 무엇을 하나

`AssetPostprocessor`를 상속한 클래스는 가져오기 전·후에 불린다. 모델을 가져올 때 순서는 다음과 같다.

| 순서 | 함수 | 여기서 할 일 | 하면 안 되는 일 |
|---|---|---|---|
| 1 | `OnPreprocessModel` | `ModelImporter` 설정 바꾸기(축 굽기, 크기, 재질 방식, 충돌체) | 다른 자산 만들기 |
| 2 | `OnPostprocessMeshHierarchy` | 계층(이름·부모) 바꾸기 | |
| 3 | `OnAssignMaterialModel` | 렌더러에 붙일 재질 고르기. **저장된 재질 자산만** 돌려줄 수 있음(임시 재질은 오류). `null`이면 기본 동작 | 새 재질 자산 만들기 |
| 4 | `OnPostprocessGameObjectWithUserProperties` | FBX 사용자 속성 읽기 | |
| 5 | `OnPostprocessModel(GameObject root)` | 만들어진 오브젝트·메시·컴포넌트 고치기(충돌체·LODGroup 추가 등). 여기 객체는 가져오기 동안만 살아 있다 | 이 메시를 참조하는 다른 프리팹 파일 만들기 |
| 끝 | `static OnPostprocessAllAssets(...)` | **자산 만들기·불러오기·옮기기·지우기가 안전한 곳.** 재질 자산 생성, 다른 자산 다시 가져오기 | 무조건 다시 가져오기(다시 불리므로 무한 반복 주의) |

텍스처는 `OnPreprocessTexture`(설정: sRGB, 종류, 최대 크기, 압축), `OnPostprocessTexture`(압축 직전 픽셀)에서 다룬다. `OnPostprocessMaterial`은 `materialImportMode`가 `ImportStandard`일 때만 불린다.

### 규칙을 바꾸면 다시 가져와지게 하기

- 가져오기 결과는 같은 입력이면 항상 같아야 한다(공식 문서 "Importer Consistency"). 후처리 코드의 결과가 바뀌면 `GetVersion()` 값을 올린다. 값이 바뀌면 관련 자산이 다시 가져와진다. 단 `OnPreprocessAsset`만 있는 클래스는 버전을 올려도 다시 가져오지 않는다.
- 규칙을 별도 파일(예: 폴더별 규칙 ScriptableObject)에 두면, 가져오기 중 `context.DependsOnSourceAsset(규칙파일경로)`(원본 파일 의존) 또는 `DependsOnArtifact`(가져오기 결과 의존, 옮겨도 유지되도록 GUID 권장)를 등록한다. 그래야 규칙을 고쳤을 때 해당 모델·텍스처가 다시 가져와진다.
- 시간·난수·폴더 탐색 순서처럼 매번 달라지는 값을 결과에 넣지 않는다. 확인은 자산 우클릭 **Reimport**(불일치 시 Console 경고) 또는 `-consistencyCheck` 명령줄 인자로 한다.

## 3. 모델 설정 (ModelImporter)

| 속성 | 뜻 | 블렌더 모델에 쓰는 법 |
|---|---|---|
| `bakeAxisConversion` | 축 변환을 정점·애니메이션 데이터에 굽는다. 끄면 루트 Transform을 돌려 흉내 낸다 | 켜면 루트 회전(−90°)을 메시에 넣는 효과. **실기로 결과 확인** |
| `useFileScale` / `fileScale`(읽기 전용) | FBX 단위를 미터로 바꾸는 배율 적용 | `fileScale`로 파일 단위를 읽고 기록한다 |
| `globalScale` | 전체에 곱하는 배율("Scale Factor") | 1 m = 1 unit 이 되게 맞춘다 |
| `materialImportMode` | `None` / `ImportStandard` / `ImportViaMaterialDescription` | 외부 재질로 바꿔 끼울 계획이면 슬롯 이름이 남는 방식을 쓴다 |
| `AddRemap(SourceAssetIdentifier, Object)` | 모델 속 재질 이름을 바깥 재질 자산으로 연결 | 연결 후 `WriteImportSettingsIfDirty` + `ImportAsset(ForceUpdate)`. 같은 자산 안의 객체는 못 씀. 형식이 안 맞으면 오류 없이 무시 |
| `RemoveRemap`, `GetExternalObjectMap()` | 연결 해제, 현재 연결 사본 읽기(사본을 고쳐도 반영 안 됨) | 되돌리기에 쓴다 |
| `SearchAndRemapMaterials` | 이름 규칙·검색 범위로 재질 자동 연결 | |
| `addCollider` | 모든 메시에 MeshCollider | 특정 이름만 충돌체로 쓰려면 끄고 후처리에서 직접 붙인다 |

블렌더 파일에 대해 공식 문서가 밝힌 한계: 텍스처와 기본색은 **자동으로 연결되지 않는다**. 그래서 텍스처 이름 규칙으로 재질을 만드는 도구가 필요하다.

### LOD 이름

메시 이름 끝에 `_LOD0`, `_LOD1` …을 붙여 FBX로 내보내면 Unity가 LOD Group을 자동으로 만든다(최대 8단계, LOD0이 가장 자세함). 블렌더가 붙이는 `.001` 같은 꼬리가 있으면 이름 규칙이 깨질 수 있으므로, 이름 정리를 LOD 판정보다 먼저 한다. 자동 LOD **생성**(Mesh LOD 생성기)은 다른 기능이며 이 매뉴얼 범위 밖이다.

## 4. 텍스처 설정 (TextureImporter)

| 속성 | 쓰는 곳 |
|---|---|
| `sRGBTexture` | 색 그림(BaseColor·Emission)은 켬. 노멀·거칠기·금속·AO·높이 같은 데이터 그림은 끔. Linear 색 공간 프로젝트에서만 의미가 있다 |
| `textureType = NormalMap` | 노멀맵. 데이터로 취급된다 |
| `flipGreenChannel` | DirectX식(초록 반대) 노멀을 Unity(OpenGL식)에 맞출 때 |
| `maxTextureSize` | 기본 플랫폼 설정만 바뀐다. 플랫폼별은 `SetPlatformTextureSettings` |
| `isReadable` | CPU에서 픽셀을 읽어야 할 때만. 메모리를 더 쓴다 |

## 5. URP Lit 재질

- Workflow는 Metallic. **Base Map**은 색(알파는 투명·잘라내기에 씀), **Metallic Map**은 금속도. Smoothness 출처는 기본 **Metallic Alpha**(금속 그림의 알파)이고, 슬라이더 값이 곱해진다.
- 금속·매끄러움·AO를 한 장으로 합칠 수 있다: **R=금속, G=AO, B=안 씀, A=매끄러움.** 이 그림은 sRGB를 끄고 **Metallic과 Occlusion 칸 둘 다**에 넣는다.
- Painter·블렌더의 Roughness(거칠기)는 Unity의 Smoothness(매끄러움)와 반대이므로 `매끄러움 = 1 − 거칠기`로 바꿔 A 채널에 넣는다.
- Normal Map·Height Map·Occlusion Map 칸이 따로 있다. 기능을 켤 때마다 셰이더 변형이 늘어 SRP Batcher 묶음이 늘 수 있으니 쓰지 않는 맵은 비운다.
- 스크립트에서 넣을 때의 셰이더 속성 이름(`_BaseMap` 등)과 키워드는 공식 페이지에 적혀 있지 않다. **설치된 URP 패키지의 Lit 셰이더 파일에서 이름을 확인**하고(아래 실기 기록), 넣은 뒤 재질에 실제로 연결됐는지 본다.

## 6. 패키지 구조와 EditMode 테스트

- 도구는 UPM 패키지(`Packages/com.<회사>.<이름>/`)로 두고 `Editor`와 `Tests/Editor` 어셈블리 정의를 나눈다. 테스트 어셈블리는 `nunit.framework.dll`, `UnityEngine.TestRunner`, `UnityEditor.TestRunner`를 참조해야 테스트 어셈블리로 인식된다(`UnityEditor.TestRunner`는 EditMode 전용).
- 프로젝트의 `Packages/` 폴더 안에서 개발하는 패키지는 테스트를 따로 켤 필요가 없다. 폴더 밖 패키지는 프로젝트 manifest의 `testables`에 이름을 넣어야 한다.
- 명령줄 실행: `Unity.exe -batchmode -projectPath <프로젝트> -runTests -testPlatform EditMode -testResults <결과.xml>`. 결과는 NUnit XML이다. **테스트 실행 중에는 `-quit`을 지원하지 않는다**(테스트가 끝나면 스스로 닫힌다). 특정 어셈블리만 돌리려면 `-assemblyNames "이름"`, 이름 필터는 `-testFilter`.
- 종료 코드의 공통 정의가 없다고 문서에 적혀 있으므로, 통과 여부는 결과 XML의 합계와 Editor 로그로 판정한다.
- 테스트가 만든 임시 자산은 테스트 끝에 지운다. 원본 시험 자료는 사본으로만 쓴다.

## 7. 검수 기준

1. 컴파일 오류 0을 지원하는 모든 Unity 버전에서 따로 확인한다(문서가 최신판 기준일 수 있다).
2. 실제 블렌더 FBX를 넣어 루트·자식의 회전·크기·메시 경계 크기를 **수치로** 기록하고, 같은 카메라로 넣기 전/후 화면을 비교한다. 스케일 값이 1이라는 것만으로 실제 크기가 맞다고 판정하지 않는다.
3. 재질은 맵 연결 수치뿐 아니라 실제 화면에서 색·광택이 Painter/블렌더와 크게 다르지 않은지 본다. 맵 연결 성공을 참고 외관 일치로 처리하지 않는다([PBR·조명·렌더 절차](BLENDER_SKILLS_WORKFLOW.md)).
4. 규칙을 바꾼 뒤 다시 가져오기, 되돌리기 후 원래 설정으로 돌아오는지 확인한다.

## 8. 출처와 실제 학습 범위

모두 Unity Technologies 공식 문서, 6000.6.7f1 설치본 동봉 오프라인 HTML(2026-11-22 열람). 같은 내용의 온라인 주소는 `https://docs.unity3d.com/6000.6/Documentation/…`이며 온라인 판은 열지 않았다.

| # | 자료 | 실제 읽은 페이지 |
|---|---|---|
| 1 | Unity Manual·Scripting API — 에셋 가져오기 | `ScriptReference/AssetPostprocessor`(본문·메시지 표), `OnPreprocessModel`, `OnPostprocessModel`, `OnPostprocessAllAssets`, `OnAssignMaterialModel`, `OnPostprocessMaterial`, `OnPreprocessTexture`, `GetVersion`, `AssetImportContext.DependsOnSourceAsset/DependsOnArtifact`, `ModelImporter`의 `bakeAxisConversion/useFileScale/fileScale/materialImportMode/addCollider`, `AssetImporter.AddRemap/GetExternalObjectMap`, `TextureImporter`의 `sRGBTexture/textureType/maxTextureSize/isReadable/flipGreenChannel`; `Manual/ImporterConsistency`, `FBXImporter-Model`, `HOWTO-ImportObjectsFrom3DApps`(블렌더 절), `lod-group-configure`(LOD 가져오기 절) |
| 2 | URP 매뉴얼(Unity 6 Manual 내 `urp/`) | `urp/lit-shader`(전체), `urp/shaders-in-universalrp-channel-packed-texture`(전체) |
| 3 | Unity Test Framework 매뉴얼 | `test-framework/reference-command-line`(전체), `run-tests-from-command-line`, `workflow-create-test-assembly`, `cus-tests`(패키지 테스트 켜기 절) |

교차 확인: 1번의 "블렌더 텍스처 자동 연결 안 됨"과 2번의 채널 합치기 규칙을 합쳐 Painter 이름 기반 재질 생성 근거로 삼았다. 3번의 `-quit` 미지원은 [Unity 공식 SKILL 학습](UNITY_OFFICIAL_SKILLS_WORKFLOW.md)의 "`-quit`로 비동기 작업이 끝나기 전 종료" 주의와 같은 방향이다.

읽지 않은 것·미확인: 6000.3판 문서 본문, URP Lit 셰이더 속성 이름(셰이더 파일 확인 필요), Painter 내보내기 프리셋 공식 이름 목록(Adobe 문서 미열람 — 실제 내보낸 파일 이름으로 판단), 블렌더 FBX 내보내기 기본값(블렌더 문서 미열람).

## 실기 기록 (2026-11-22, Unity 6000.3.27f1 / URP 17.3.0 · 6000.6.7f1 / URP 17.6.0, 배치 모드)

내부용 가져오기 규칙기 0.1.0을 만들며 실제로 확인한 것이다. 제작자 자체 확인이며 독립 검수(2026-11-22부터 별도 Claude 검수 창) 전이다. 에디터 창 클릭은 하지 않았다.

- **블렌더 5.2 기본 내보내기 FBX(실제 파일 3개):** 축 설정은 이미 Y-위(UpAxis 1, FrontAxis 2)이고, 단위 cm(UnitScaleFactor 1)에 **물체마다** Lcl Rotation X −90, Lcl Scaling 100이 들어 있다. Unity 기본 가져오기에서 회전 270.02°(−89.98°), 크기 100으로 보인다. 'FBX Units Scale'로 내보낸 파일은 단위 배율 100, 크기 1, 회전 −90이었다.
- **Bake Axis Conversion은 이 문제를 풀지 않는다:** 켜도 회전 270.02° → 89.98°로 바뀔 뿐이다(파일이 이미 Y-위라서 −90은 축 변환이 아니라 물체 회전이다). 그래서 OnPostprocessModel에서 각 물체의 회전·크기를 메시(정점·노멀·탄젠트·블렌드셰이프)에 굽고, 자식 위치·회전·크기를 넘겨받게 했다. 보이는 모양과 크기는 그대로이고 Transform은 회전 0·크기 1이 된다. 0.1° 안쪽으로 어긋난 직각은 정확한 직각으로 맞춘다. 음수 크기는 삼각형 방향을 뒤집는다. 뼈대 메시·축마다 다른 크기+자식·공유 메시는 굽지 않는다.
- **크기 100 자체가 단위 실수인 파일도 있다:** 손 스캔 FBX는 cm 값에 크기 100이 겹쳐 18.3 m로 들어왔다. 자동으로 판단하지 말고 폴더 규칙의 Scale Factor(0.01)로 맞추고, 한 메시 10 m 초과는 가져오기 경고로 알린다.
- **이름에 `.001`이 붙어도** Unity는 루트에 LOD Group을 만들었다. 이름 정리 후 LOD 단계를 다시 맞추는 편이 안전하다. 단일 물체 파일은 루트가 파일 이름이 되고 `.001`은 메시 이름에만 남는다.
- **첫 가져오기 설정 저장:** `importSettingsMissing`일 때 OnPreprocessModel/Texture에서 바꾼 가져오기 설정과 `userData`는 .meta에 저장됐다. 이후 가져오기는 .meta만 보고 같은 결과를 내므로(ForceUpdate 재가져오기 결과 동일), 사용자가 Inspector에서 바꾼 값이 유지된다.
- **재질:** 재질 자산 생성과 Remap은 OnPostprocessAllAssets에서 했다(AddRemap → WriteImportSettingsIfDirty → ImportAsset). 재질 칸이 없는 FBX는 OnPostprocessModel에서 렌더러에 재질 자산을 직접 넣고 DependsOnArtifact로 의존성을 등록했다. URP Lit 속성 이름은 설치된 `Lit.shader`에서 확인: `_BaseMap`, `_BaseColor`, `_BumpMap`(`_NORMALMAP`), `_MetallicGlossMap`(`_METALLICSPECGLOSSMAP`), `_Smoothness`, `_SmoothnessTextureChannel`, `_OcclusionMap`(`_OCCLUSIONMAP`), `_ParallaxMap`(`_PARALLAXMAP`), `_EmissionMap`/`_EmissionColor`(`_EMISSION`). 17.6에는 화면 공간 반사 속성 2개가 더 있다.
- **Painter 내보내기 이름 실례:** Blender 프리셋 UDIM 프로젝트는 `DefaultMaterial_BaseColor.1001.png`처럼 `.1001`이 붙고 Normal은 16비트 PNG였다. `Texture2D.LoadImage`로 16비트 PNG를 읽어 합치기가 됐다. 맵 연결 뒤 색·광택은 Painter 맵 그대로라 블렌더에서 따로 섞은 최종 외관과 달랐다 — 연결 성공과 외관 일치는 따로 판정한다.
- **같은 경로에 지웠다 다시 넣은 파일은 예전 GUID를 재사용**했다. GUID로 작업 기록을 관리하면 삭제 기록을 지우고, 만든 파일이 실제로 있는지까지 확인해야 한다.
- **테스트:** `-runTests -testPlatform EditMode -assemblyNames … -testResults …`(‑quit 없이)로 두 버전 56/56 통과. 프로젝트 `Packages/` 안 패키지는 `testables` 없이 테스트가 잡혔다. 6000.6에서는 내장 패키지가 URP 17.6.0, Test Framework 1.8.0으로 해석됐다(manifest의 17.3.0 무시). 같은 프로젝트를 두 버전으로 열지 않도록 6.6 시험은 사본에서 했다.
- **배치 모드 렌더:** `-nographics` 없이 실행하면 URP에서 `Camera.Render()`로 RenderTexture 캡처가 됐다.

[교육 목록](../README.md) · [공통 작업 규칙](COMMON_WORK_RULES.md)
