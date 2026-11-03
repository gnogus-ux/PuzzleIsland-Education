# Blender 애드온·확장 목록

2026-11-03 확인 · Blender 5.2.2 LTS. 사용자 설치 **19개**, 기본 제공 **13개**, 합계 **32개**. 마지막으로 저장된 설정에서 활성 **28개**, 비활성 **4개**.

## 확인 범위

- 설치 폴더의 manifest 또는 bl_info와 저장된 Preferences의 모듈 목록을 대조했다. 활성은 **저장된 활성화 설정**을 뜻한다. 열린 창의 미저장 설정·현재 로드 성공·개별 기능 실행 여부는 별도다.
- 격리된 factory-startup 프로세스에서 사용자 애드온 등록을 실행하지 않고 설정을 읽었다. 설정 파일의 전후 해시가 같았으며, 기존 작업창·모델·연결·서비스·설정은 변경하지 않았다.
- 이번 점검에서 추가 설치·활성화 변경·생성 제출·외부 서비스 로그인·유료 호출은 하지 않았다. 모든 항목의 기능 실기 검증은 이번 점검 기준 `NOT_RUN`이다. 기존 작업의 실행 근거는 [프로그램 목록](AVAILABLE_TOOLS.md)과 구별한다.
- 버전은 설치된 파일의 메타데이터이며, 최신 배포 버전이나 Blender 5.2에서의 모든 기능 호환을 보장하지 않는다. 버전이 없는 기본 모듈은 Blender 배포 버전으로 식별한다.

## 사용자 설치 애드온·확장 (19개)

| 이름 | 설치 버전 | 저장 활성 | 용도 | 모듈 |
|---|---|---|---|---|
| ARKit Blendshape Helper | 0.7.5 | 활성 | ARKit 표정 셰이프키 보조 | `bl_ext.blender_org.arkit_blendshape_tools` |
| Auto Mirror | 2.5.4 | 활성 | 대칭 절단·미러 모델링 | `bl_ext.blender_org.auto_mirror` |
| Corrective Shape Keys | 1.0.0 | 활성 | 포즈 보정 셰이프키 | `bl_ext.blender_org.corrective_shape_keys` |
| EasyWeight | 1.1.3 | 활성 | 웨이트 페인팅 보조 | `bl_ext.blender_org.easyweight` |
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
