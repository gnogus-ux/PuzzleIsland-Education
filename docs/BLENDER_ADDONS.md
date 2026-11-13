# Blender 애드온·확장 목록

2026-11-03 확인 · Blender 5.2.2 LTS. 최신 설치 반영: 사용자 설치 **20개**, 기본 제공 **13개**, 합계 **33개**. 마지막으로 저장된 설정에서 활성 **29개**, 비활성 **4개**. 최초 점검은 사용자19/합계32/활성28이며 아래 최신 설치 기록이 이를 갱신한다.

## 확인 범위

- 설치 폴더의 manifest 또는 bl_info와 저장된 Preferences의 모듈 목록을 대조했다. 활성은 **저장된 활성화 설정**을 뜻한다. 열린 창의 미저장 설정·현재 로드 성공·개별 기능 실행 여부는 별도다.
- 격리된 factory-startup 프로세스에서 사용자 애드온 등록을 실행하지 않고 설정을 읽었다. 설정 파일의 전후 해시가 같았으며, 기존 작업창·모델·연결·서비스·설정은 변경하지 않았다.
- 이번 점검에서 추가 설치·활성화 변경·생성 제출·외부 서비스 로그인·유료 호출은 하지 않았다. 모든 항목의 기능 실기 검증은 이번 점검 기준 `NOT_RUN`이다. 기존 작업의 실행 근거는 [프로그램 목록](AVAILABLE_TOOLS.md)과 구별한다.
- 버전은 설치된 파일의 메타데이터이며, 최신 배포 버전이나 Blender 5.2에서의 모든 기능 호환을 보장하지 않는다. 버전이 없는 기본 모듈은 Blender 배포 버전으로 식별한다.

## 후속 설치·실행 확인 — 2026-11-03

- [Mesh Repair Tools 4.0.2](https://extensions.blender.org/add-ons/mesh-repair-tools/)를 공식 확장 배포본으로 추가 설치·저장 활성화했다. GPL-3.0-or-later, Blender 4.2 이상 표기이며 배포 SHA256을 대조했다.
- Blender 5.2.2 LTS의 별도 프로세스에서 로드하고, 새 시험 메시의 중복 정점 5→4개를 실제 제거해 `FINISHED`를 확인했다. 삼각화·사각화·구멍 메우기·법선 수정·교차/잡음 제거를 끈 제한된 구성만 검증했다. 다른 기능 전체의 호환을 뜻하지 않는다.
- 해당 자동 정리 버튼은 화면 다시 그리기를 요구해 background 모드에서는 실행할 수 없다. 화면이 있는 별도 작업 프로세스에서만 이번 기능을 확인했다. 기본 병합 거리는 0.0001 Blender 단위이므로 실제 제품 크기를 고려해야 하며, 포켓·슬롯 입구를 무조건 메우지 않는다.
- 기존 저장 활성 항목은 유지하고 설정 원본은 비공개로 백업했다. 기존 사용자 창 조회·재시작·유료 구매·로그인은 하지 않았다. 아래 최초 점검의 `NOT_RUN`은 새 항목을 제외한 당시 범위에 대한 기록이다.
- [설치·제한 기능 검증 기록](../reports/ToolInventory/20261103_MESH_REPAIR_TOOLS.json)

## 기존 UniV 4.0.0 제한 기능 확인 — 2026-11-03

- [공식 UniV](https://github.com/Oxicid/UniV) 기존 설치·저장 활성을 재사용했다. Blender 5.2.2에서 회전 없는 AABB 직접 실행으로 8K 두 장·1K 한 장·2K 한 장을 패킹하고 각 세트의 겹침 검사를 실행했다. 추가 설치·유료 백엔드 호출은 없었다.
- 가죽 세트에는 경계 접촉·반올림에 따른 기본 검사 경고가 남아 면적 교차를 추가 확인했다. 표시된 후보 삼각형의 교차 면적은 0.0001 픽셀² 허용오차에서 0, 섬 경계상자 교차도 0이었다. 모든 기본 경고가 0이라는 뜻은 아니다.
- 작은 시험 메시의 Normalize는 성공했으나 제품의 밀리미터 이하 작은 섬이 면적 판정에서 제외돼 실제 가죽 밀도 맞춤은 기본 Average Islands Scale을 사용했다. 실은 길이 방향을 따르는 별도 전개를 사용했다. 모든 기능의 호환을 주장하지 않는다.
- Windows의 다른 패킹 경로에는 입력 이벤트 동작이 있어 AABB 직접 실행만 사용했다. 기존 사용자 창은 조회·재시작하지 않았다.
- factory 환경의 활성 목록과 공용 확장 의존성은 분리되지 않을 수 있다. 필요한 확장 로드 전에 기존 저장 활성 목록을 보존한다. 시험 중 영향을 받은 의존성은 기존 설치 wheel과 Blender 관리 기능으로 복구했고 설정 파일 해시는 같았다. 다른 앱 등록·서비스 호출은 하지 않았다.
- [기능 범위·제한·수치 기록](../reports/ToolInventory/20261103_UNIV_UV_VALIDATION.json)

## 사용자 설치 애드온·확장 (20개)

| 이름 | 설치 버전 | 저장 활성 | 용도 | 모듈 |
|---|---|---|---|---|
| ARKit Blendshape Helper | 0.7.5 | 활성 | ARKit 표정 셰이프키 보조 | `bl_ext.blender_org.arkit_blendshape_tools` |
| Auto Mirror | 2.5.4 | 활성 | 대칭 절단·미러 모델링 | `bl_ext.blender_org.auto_mirror` |
| Corrective Shape Keys | 1.0.0 | 활성 | 포즈 보정 셰이프키 | `bl_ext.blender_org.corrective_shape_keys` |
| EasyWeight | 1.1.3 | 활성 | 웨이트 페인팅 보조 | `bl_ext.blender_org.easyweight` |
| Mesh Repair Tools | 4.0.2 | 활성 | 중복 정점 등 메시 정리; 제한 구성 실행 확인 | `bl_ext.blender_org.mesh_repair_tools` |
| LoopTools | 4.7.7 | 활성 | 루프·원형·평탄화 등 메시 정리 | `bl_ext.blender_org.looptools` |
| Mio3 Copy Weight | 1.1.0 | 활성 | 오브젝트 간 정점 웨이트 복사 | `bl_ext.blender_org.mio3_copy_weight` |
| Mio3 Flex | 1.0.4 | 활성 | 경로를 이용한 완만한 메시 변형 | `bl_ext.blender_org.mio3_flex` |
| Mio3 UV | 2.2.0 | 활성 | UV 편집 보조 | `bl_ext.blender_org.mio3_uv` |
| Ucupaint | 3.0.0 | 활성 | Eevee/Cycles 레이어 페인팅 | `bl_ext.blender_org.ucupaint` |
| Vertex Overlap | 1.1.0 | 활성 | 중복 정점 표시 | `bl_ext.blender_org.vertex_overlap` |
| Blender MCP | 1.19.0 | 활성 | MCP 클라이언트와 Blender 연결 | `bl_ext.user_default.blender_mcp` |
| Higgsfield | 1.5.60 | 활성 | Blender 내 Higgsfield 미디어 연동 | `bl_ext.user_default.higgsfield_blender` |
| QRemeshify | 1.1.0 | 활성 | 쿼드 리메시 | `bl_ext.user_default.qremeshify` |
| RetopoFlow 3 | 3.4.11 | 활성 | 리토폴로지 도구 | `bl_ext.user_default.retopoflow` |
| UniV | 4.0.0 | 활성 | UV 편집·정리 | `bl_ext.user_default.univ` |
| UV Mechanic | 1.0.0 | 활성 | UV 정렬·겹침·밀도 보조 | `bl_ext.user_default.uv_mechanic` |
| Zeeks Auto UV Unwrap | 2.0.0 | 활성 | 자동 UV·시임 보조 | `bl_ext.user_default.zeeks_auto_uv_unwrap` |
| Tripo Bridge | 1.0.34 | 활성 | Tripo AI 생성 서비스 연결 | `Tripo3d_Blender_Bridge` |
| Tripo 3D | 0.7.7 | 활성 | Tripo AI 생성 서비스 연결 | `tripo_local` |

## Blender 기본 제공 모듈 (13개)

| 이름 | 설치 버전 | 저장 활성 | 용도 | 모듈 |
|---|---|---|---|---|
| Blender Extensions | 0.0.1 | 활성 | 확장 저장소 관리 | `bl_pkg` |
| Cycles Render Engine | Blender 5.2.2 배포판 | 활성 | Cycles 렌더 엔진 | `cycles` |
| Hydra Storm render engine | 1.0.0 | 비활성 | Hydra Storm 렌더 엔진 | `hydra_storm` |
| BioVision Motion Capture (BVH) format | 1.0.1 | 활성 | BVH 모션 입출력 | `io_anim_bvh` |
| Scalable Vector Graphics (SVG) 1.1 format | Blender 5.2.2 배포판 | 활성 | SVG 커브 가져오기 | `io_curve_svg` |
| UV Layout | 1.2.0 | 활성 | UV 레이아웃 내보내기 | `io_mesh_uv_layout` |
| FBX format | 5.15.0 | 활성 | FBX 입출력 | `io_scene_fbx` |
| glTF 2.0 format | 5.2.40 | 활성 | glTF 입출력 | `io_scene_gltf2` |
| Node Wrangler | 4.1.0 | 비활성 | 노드 편집 보조 | `node_wrangler` |
| Pose Library | 2.0 | 활성 | 포즈 자산 관리 | `pose_library` |
| Rigify | 0.6.10 | 활성 | 자동 리깅 도구 | `rigify` |
| Manage UI translations | 2.1.0 | 비활성 | UI 번역 관리 | `ui_translate` |
| VR Scene Inspection | 0.11.2 | 비활성 | VR 장면 미리보기 | `viewport_vr_preview` |

## 작업 전 활용 기준

1. 작업 목적을 정하고 위 목록에서 기존 기능을 먼저 찾는다. 모델링은 LoopTools·Auto Mirror·Mio3 Flex, 리토폴로지는 RetopoFlow·QRemeshify, UV는 Mio3 UV·UniV·UV Mechanic·Zeeks, 웨이트는 EasyWeight·Mio3 Copy Weight, 리깅/보정은 Rigify·Corrective Shape Keys, 노드 작업은 Node Wrangler가 기능상 후보이다. 실제 선택은 작업의 보존 조건과 호환 확인 후 한다.
2. 설치 파일 존재 → 저장 활성 → 현재 프로세스 로드 → 필요한 기능의 제한된 실행 확인을 구분한다. 이번 목록만으로 실행 성공을 주장하지 않는다. Node Wrangler는 이미 기본 제공되어 있으므로 필요하면 기존 설치를 활성화하고 확인한다.
3. 필요한 애드온이 없으면 [공통 도구 규칙의 상시 승인](COMMON_TOOL_POLICY.md#blender-애드온-사전-확인활용설치-상시-승인)에 따라 추가 승인 없이 설치·활성화·호환 확인·필요 기능 확인까지 수행한다. 불필요한 일괄 설치나 무관한 업데이트를 하지 않는다.
4. Tripo·Higgsfield 같은 외부 서비스용 애드온이 설치돼 있어도 계정 연결·생성 성공·크레딧 사용 승인을 의미하지 않는다. 유료 구매·사용자 직접 로그인·도구의 필수 승인은 별도로 지킨다. Painter 등 기존 조회 금지는 유지한다.

설정상 활성이나 설치 항목이 없는 모듈: **없음**.

[기계 판독 목록](../reports/ToolInventory/20261103_BLENDER_ADDONS.json) · [공통 도구 규칙](COMMON_TOOL_POLICY.md) · [프로그램 목록](AVAILABLE_TOOLS.md)

## QRemeshify·RetopoFlow 제한 확인 — 2026-11-13

기존 설치 QRemeshify1.1.0을 Blender5.2.2 LTS의 별도 백그라운드 프로세스에서 로드·등록하고 독립 큐브로 실행했다. 입력96면, 출력4,704쿼드, `FINISHED`, 약3.35초였다. 일반 쿼드화의 제한된 동작 확인이며 특정 제품의 경계·공유 격자·면 예산을 보장하지 않는다. 이 한 시험이 항상 면 수를 늘린다는 뜻도 아니다. 새 설치·저장 활성화 변경은 없었다.

RetopoFlow3.4.11은 모듈이 로드됐지만 설치 코드가 `bpy.app.background`에서 후속 초기화를 건너뛰었다. 등록 표지만으로 실제 retopo 기능 실행 성공으로 표시하지 않는다. UI 도구·전체 버전 호환은 미검증이다.

같은 환경에서 Blender 기본 메시 API의 독립 쿼드 패치 생성·저장·재열기, 명시적 짧은 대각선 삼각화와 재질/UV 속성 보존을 확인했다. 평가 메시의 임시 재질 ID와 영구 `bpy.data.materials` 참조를 구분하고, 저장 재열기에서 null 슬롯·면별 재질 번호·UV·셰이더 signature를 확인해야 한다. 제품 제작·전체 연결·충돌·UV 전개 완료를 뜻하지 않는다. 사용자 설정 파일은 해시 불변이었다. [제한 실기 기록](../reports/ToolInventory/20261113_QUAD_PATCH_RUNTIME.json).
