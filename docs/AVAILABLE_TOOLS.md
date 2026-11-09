# 공통 사용 프로그램 목록

## Euraika 선택 기능 설치 — 2026-11-04

사용자 개별 지시로 [Euraika 고정 원본](https://github.com/Euraika-Labs/Codex-Code-Game-Studios/tree/9a182e29f8d9b46394851830ba27213fbe4da950)에서 진행 상태·작업 수행·코드 검수·버그 분류를 수정한 보조 스킬4개를 새 이름으로 설치했다. 기존 공통/프로젝트 규칙·모델·권한 설정은 보존하고 전체 bootstrap·원본 hooks·50개 에이전트 일괄 설치는 하지 않았다. 네 스킬 구조·링크·보호 파일8개 해시와 문서/산출물 상태 확인을 검증했다. 실제 자동 선택·게임 제작·Unity/기기·원본 hooks 런타임 검증과 구별한다. [도입 매뉴얼](EURAIKA_SELECTIVE_STUDIO.md) · [제한된 검증 기록](../reports/ToolInventory/20261104_EURAIKA_SELECTIVE.json).

2026-11-01 확인. 여러 프로젝트가 공유하는 PC 환경의 도구 목록이다. 설치 유무, 실제 실행 근거, 남은 조건을 구별한다. 다른 PC에도 같은 프로그램이 설치되어 있다고 가정하지 않는다. [도구 확인 공통 규칙](COMMON_TOOL_POLICY.md)을 먼저 따른다.

이 목록은 확인 담당이 제공한 설치/실행 근거를 정리한 문서다. 사용자 개별 재개 지시로 Stable Fast 3D의 모델 다운로드/CPU 생성, RealityScan의 공식 설치/첫 작업 화면, Materialize 기존 설치의 정상 작업 UI를 확인했다. 다른 도구의 설치 보류·조회 금지는 그대로 유지한다.

## Blender 애드온 점검 (2026-11-03)

[애드온 목록](BLENDER_ADDONS.md): 사용자 설치19개·기본 제공13개, 합계32개. 저장 활성28개/비활성4개. 설치 메타데이터와 마지막 저장 설정만 확인했으며 이번에 개별 기능 실행·열린 창 조회·설정 변경·추가 설치는 하지 않았다. 작업 전 필요한 애드온을 먼저 확인·활용하고, 없으면 [공통 상시 승인](COMMON_TOOL_POLICY.md#blender-애드온-사전-확인활용설치-상시-승인)에 따라 추가 승인 없이 설치·활성화·호환/기능 확인한다. 이 범위만 기존 설치 보류의 예외이며 새 유료 구매·필수 인증·다른 앱 조회 금지는 유지한다.

후속 갱신: Mesh Repair Tools 4.0.2 추가 설치로 사용자20개·기본13개·합계33개·저장활성29개다. Blender 5.2.2의 별도 화면 프로세스에서 중복 정점 제거만 제한 검증했다. background 버튼 실행 불가·다른 복구 기능 미검증을 [기록](../reports/ToolInventory/20261103_MESH_REPAIR_TOOLS.json)에 구분했다. 기존 32개 점검 결과는 당시 스냅샷이다.

기존 UniV 4.0.0으로 Blender 5.2.2의 별도 화면 있는 작업 프로세스에서 8K·8K·1K·2K UV 패킹과 겹침 확인을 실행했다. 작은 섬 정규화와 기본 경고의 제한, 공용 확장 의존성 보존은 [검증 기록](../reports/ToolInventory/20261103_UNIV_UV_VALIDATION.json)을 따른다. 추가 설치 없이 설치33개·저장활성29개를 유지했다.

## 최근 실행 근거가 있는 도구

2026-11-05 추가 확인: Sampler 6.0.2에서 별도 Cloth Weave·Coating/Paint 두 재질의 SSA 저장과 4K OpenPBR 18채널 출력을 확인했다. 앱 종료 후 기존 실행 파일 재실행·저장 SSA 복구도 이번에는 확인했으며 종료 원인은 미확정이다. Blender 5.2.2에서는 DX 노멀의 실제 convention 속성·새 UV·별도 재질 연결과 정지 Cycles 접사를 검수했다. Height 출력 보관과 실제 변위 연결은 구별한다. [마감 매뉴얼](SAMPLER_THREAD_EDGE_FINISH.md)의 제한된 실행 절을 따른다. 아래 이전 기록은 당시 검증 범위다.

| 프로그램 | 버전·구성 | 용도 | 확인 근거와 범위 |
|---|---|---|---|
| Chili3D | 0.8.0 로컬 소스 설치 / 문서 0.7.1 | 제품 치수·단면의 CAD 검토 | 2026-11-04 개별 설치·사용 승인으로 독립 폴더에 공식 소스 설치. 의존성 설치·컴파일/형식 검사·ego-browser WASM/UI 실행·검토용 선 형상 10개 저장/재열기·STEP 출력 확인. Blender 원본 보존. AI API·유료 Pro·STEP 재수입·제조 검증은 미실행. 후속 전체 참고 메시 문서 표시·IndexedDB 저장/재열기·앱 좌표/삼각 인덱스 해시 일치 확인. 원래 PBR·UV·리그·정밀 CAD 이력 이관은 제외. [매뉴얼](CHILI3D_LOCAL_CAD.md) · [제한 검증 기록](../reports/ToolInventory/20261104_CHILI3D_LOCAL.json) |
| Blender | 5.2.2 LTS | 모델링·UV·재질·리깅·렌더 | 기존 프로젝트 실제 작업/저장·실행 창 근거. 2026-11-02 기존 실행 파일의 격리된 백그라운드 프로세스에서 별도 가이드·부품 생성/저장과 Workbench 정지 미리보기 출력을 확인했다. 새 프로세스는 순차 종료했고 기존 제품 파일·실행 중 창·전역 설정은 변경하지 않았다. 이 근거가 응답 없는 라이브 연결의 복구나 모든 애드온·동작 테스트 성공을 뜻하지는 않음 |
| FreeCAD | 1.1.4 / 20260928 (기존 실기 기록) | 파라메트릭 CAD·2D 형상과 교환 검토 | **초기 2D 제한시험 이력:** 2026-11-06 기존 기록 대조: 사용자 설치본의 CLI/GUI, 완전구속 2D Sketch·유한 선분 기반 평면 face와 홀, FCStd 저장·재열기, STEP 면 내보내기·재수입을 실제 실기 및 독립 파일 검수에서 확인했다. 일반 DXF LINE 경계 왕복도 확인했으나 **검증 예제 solid는0**이다. 3D 폐실체 Boolean·원함수 법선 두께·동적 fit·MD9 AAMA/ASTM 패턴 DXF 수신은 미검증이다. 이번 목록 반영은 기존 보고 대조이며 새 설치·실행·업데이트를 하지 않았다. **별도 후속 한정 실기:** FreeCAD 1.1.4 / OpenCascade 7.8.1에서 국부 진단용 valid/closed solid2개와 후면270개 독립 face를 확인했다. CLI/GUI에서 FCStd 저장·재열기, STEP 내보내기·재수입과 소유 프로세스 정상 종료를 검증했다. 후면 face는 연결된 전체 shell이 아니며, 전체 공유 상부는 solid0/PARTIAL이다. 제품 적용·원함수 정확 재현·최소 벽두께·전역 fit은 미검증이다. 이 후속 갱신도 최종 실기 기록 대조이며 게시 담당의 새 설치·앱 실기는0이다. [공식 배포](https://github.com/FreeCAD/FreeCAD/releases) · [저장소](https://github.com/FreeCAD/FreeCAD) · [LICENSE: LGPL 2.1](https://github.com/FreeCAD/FreeCAD/blob/main/LICENSE) · [공식 문서](https://wiki.freecad.org/Getting_started) |
| Claude Desktop | 기존 설치, UI Opus 5.5·Sonnet 5.5 / 높음 확인 | 사용자가 개별 재개한 3D 모델링·제작 코드 작성 | 2026-11-02 초기 작업에서 사용량 100%·한도 도달 및 같은 날 15:20 KST 초기화 표시를 확인하고 전담 Codex가 안전 인수했다. 이후 Sonnet 5.5·높음 UI에서 허용된 폴더의 인계서·가이드 정지 화면을 읽고 제작 코드를 실제 작성·저장한 결과를 확인했다. 해당 세션에는 로컬 Blender 실행 도구가 없어 실제 격리 실행·저장·정지 검토는 Codex가 맡았다. 최근 UI는 주간 한도 임박 표시이며 잔여량·다음 초기화 시각은 미확인. 코드 작성과 앱 실행을 구별하며 추가 결제·한도 우회·설치/전역 설정·권한 변경·승인 밖 조회와 Painter 조회 금지는 유지 |
| Materialize | 1.78 공식 ZIP 기존 설치 | 이미지에서 높이·노멀·금속·매끄러움·AO 등 재질 맵 제작 | 기존 실행 창을 정상 선택/활성화해 작업 메뉴·저장/미리보기 UI 표시 확인. 이전 흰 화면은 현재 재현되지 않음. 중복 다운로드/재설치 없이 기존 환경 사용. 실제 이미지 로딩·맵 생성·저장은 이번 확인에서 미실행 |
| Adobe Substance 3D Sampler | 6.0.2 | 사진에서 PBR 맵 추정·출력 | 2026-11-04 기존 앱에서 원본 가죽 Crop→AI Leather/Shiny→별도 SSA·OpenPBR PNG 5채널 출력 확인. 후속 별도 후보에서 Make It Tile·3×3/Offset 검사, OpenGL Normal 출력 후 원 DirectX 설정 복원, Blender 5.2.2 시험 평면 좌우 Cycles 확대 렌더·실제 ±0.04mm 변위 확인. 후속 후보는 Height/Normal/Roughness 16비트, 색/금속 8비트, 2048². 약400px 표본 확대·16mm 반복 크기 가정이며 패치 밀도 차이/흐림이 남는다. 완전한 실측 복원·제품 최종 합격·Sampler 완전 재기동은 미검증. 신규 설치·결제·인증 대행 없음. [매뉴얼](SAMPLER_PHOTO_PBR.md) · 2026-11-05 후속: 넓은 참조 재구성·Upscale4×·4K 원맵 출력 및 Blender 부품별4K32맵 재베이크/재패킹/실제 변위·별도 저장·재열기 확인. 접사 원본 부드러움과 거친 일부 변위 격자·영상 최종 승인 한계 유지. [제한 실기](../reports/ToolInventory/20261104_SAMPLER_RUNTIME.json) |
| RealityScan | 2.2.0.119430, 공식 Epic Games Launcher 설치 | 여러 사진·레이저 스캔으로 3D 복원 | 런처 다운로드/설치 검증 완료, Epic Games 유효 디지털 서명 및 새 프로젝트 작업 화면 확인. 무료 사용 조건·연령 확인은 사용자가 직접 완료. 실제 사진 정합·메시 생성·내보내기는 미실행. 사진 한 장에서 원본 모델/노드의 정확 복구로 해석하지 않음 |
| Stable Fast 3D | 공식 소스 ff21fc4, Python 3.10 / PyTorch 2.5.1 / CPU 베이커·UV 확장 | 이미지 한 장에서 새로운 텍스처 포함 3D 후보 생성 | 공식 모델 다운로드 및 SHA256/config Git blob 검증. 공식 chair1 CPU 생성 160.11초·256×256 GLB 재로딩 통과(20,028 삼각면·UV·PBR). 로컬 Gradio 업로드→생성→512×512 GLB·3D 미리보기 확인. UI 호환: Pydantic 2.10.6 / FastAPI 0.112.2 / Starlette 0.38.6. GPU 베이커 미빌드·GPU 실행 미검증. 원본 모델/노드/제작 설정의 정확 복원 또는 리깅용 토폴로지 보장 아님 |
| PhotoCraft | 0.18.0 | 사진·가죽 텍스처·높이 맵 편집 | 기존 텍스처 작업 및 열린 문서 근거. 사진→3D 자동 복원 도구로 분류하지 않음 |
| Qwen3-VL | 4B Instruct, Ollama 로컬 모델 | 이미지 해석·영상 추출 프레임 분석 | 실제 로컬 분석 JSON과 최근 교육 분석. 형상·시점·문자 오독은 원본 대조 필요 |
| FrameLens AI | 로컬 Python 환경 | 컷·대표 프레임·색상·움직임 분석 | 실제 분석 JSON·최근 교육 분석. 의미 해석 필드가 비어 있으면 의미 분석 완료로 보지 않음 |
| FFmpeg / FFprobe | 도구 전용 설치, FFmpeg 9.0.2 실행 확인 | 영상 정보·프레임·클립·인코딩 | 버전 실행 및 기존 추출 결과. 시스템 PATH에 없어도 설치되어 있음 |
| Python | 3.10.6 및 도구별 독립 환경 | 자료 처리·스크립트·로컬 분석 | 실제 실행·의존성 설치·모듈 검사. 다른 환경 패키지를 전역 덮어쓰기 금지 |
| uv | 0.6.14 | 독립 Python 환경·패키지 관리 | 버전 실행 및 전용 환경 구성 기록 |
| Git | 2.53.0.windows.1 | 변경 추적·저장소 관리 | 버전 실행·정상 커밋/푸시 기록 |
| GitHub CLI | 2.102.0 | 저장소 조회·게시 검증 | 버전·저장소 권한 조회 실행. 다른 계정/PC 권한을 가정하지 않음 |
| .NET SDK | 10.0.401 | C# 빌드·Unity 독립 코어 검사 | 현재 버전 실행 및 기존 코어 검사 기록. Unity/Android 실행 검증과 구별 |
| Visual Studio C++ 도구 | Community 2026, MSVC 14.51 | Windows 네이티브 확장 빌드 | 이번 CPU 베이커·UV 확장 빌드 성공. CUDA Toolkit 설치를 뜻하지 않음 |
| ego-browser | 설치된 CLI·브라우저 | 웹 조사·자료 페이지 확인 | 실제 브라우저 작업 기록. 별도 승인 없이 다른 브라우저 자동화로 바꾸지 않음 |

## 설치는 확인했지만 용도별 실행 확인이 필요한 도구

2026-11-05 Marvelous Designer 9 Enterprise 실행 프로세스·창 제목·파일 ProductVersion `5, 1, 381, 28577`을 확인했다. 사용자에게 이미 열려 있던 프로그램이며 새 설치/실행은 하지 않았다. 화면 내 메뉴·패턴 편집·봉제·시뮬레이션·저장/재열기·라이선스 상태는 확인하지 않았다. [공식 문서 10개 학습 및 적용 한계](MARVELOUS_WALLET_PATTERN_WORKFLOW.md)와 [확인 범위](../reports/ExternalLearning/20261105_MARVELOUS_WALLET_STUDY.json)를 따른다. 아래 설치 당시 Adobe 기록과 구분한다.

2026-11-05 후속 GUI 진단에서는 기존 MD9 창의 정상 응답을 확인하고, 최소화 상태로 실패했던 캡처를 창 복원·재선택 후 성공시켰다. 사용자에게 허용된 창 제목 목록 1회 조회에서 대상만 선택했으며 다른 앱 화면·연결은 열지 않았다. 실제 주 화면과 2D Pattern·Sewing·Script 메뉴 응답, Script의 Python 항목을 확인했다. 접근성 트리는 대부분 이름 없는 custom 항목이어서 키보드 메뉴 이동과 현재 스크린샷을 병행했다. 현재 창에서 화면 좌표와 클릭 입력의 비율 차이를 무해한 두 메뉴로 보정·확인했으나, 이를 다른 창·모니터의 보편 배율로 고정하지 않는다. 전용 MD MCP 연결, Python 콘솔 실행 결과, 패턴 작성·절개·봉제·시뮬레이션·저장/재열기·라이선스 검증은 여전히 미실행 또는 미확인이다. 신규 설치·브리지·인증/네트워크/디스플레이 설정 변경은 하지 않았다.

2026-11-04 사용자 Adobe 설치 확인 요청으로 등록 정보와 해당 실행 파일을 대조했다. 설치 당시에는 실행·로그인·라이선스·사진 맵 생성은 확인하지 않았다. 이후 Sampler만 위 최근 실행 근거와 같이 제한 실기를 확인했으며 나머지 앱은 설치 확인 범위를 유지한다. [설치 당시 조회 범위](../reports/ToolInventory/20261104_ADOBE_INSTALLED.json).

| 프로그램 | 설치 정보 | 사용 전 확인 |
|---|---|---|
| Python SSL·기존 JDK/ADB 전송 검수 경로 | 기존 Python3.10/JDK17/SDK·ADB; 신규 도구 설치 없음 | 초기 공식 학습·shell native fixture11건과 후속 Windows 로컬 검수를 구분한다. 실제 전용 TLS 키/PEM 로드·표준 IP SAN/TLS1.3·무인증401, 배포69파일 대조·기존189/원본475 불변을 확인했다. 제작자 시나리오의 Windows 재실행은124/124+symlink미실행1, PC e2e54/54이며 root작성 잠금/만료 재현은 별도 PASS다. APK 동일서명 업데이트 versionCode2/r17-1·제한 UI만 확인. 그 초기 기록에서 실제 앱 pairing/송수신·LAN·포트전달·방화벽·이동통신·전체 공개 준비는 미검증이었으며 게시 담당의 추가 실행0. r16 근거와 Cloudflare/VPN 금지를 유지한다. [로컬/설치 범위](../reports/ToolInventory/20261109_R17_LOCAL_DEPLOYMENT_APK_REVIEW.json) · [native11](ANDROID_NATIVE_TLS_PROBE.md) · [TLS 설계](DIRECT_TLS_FILE_EXCHANGE.md) 후속 앱 전송 확인: 검수 담당이 승인된 단일 포트 전달·좁은 Windows 수신 규칙을 실제 적용하고 설치 앱 versionCode3 / r17-ui1에서 인증 목록·작업 다운로드/열기·결과 업로드/PC 접수 확인을 수행했다. 같은 Wi-Fi의 공인 IPv4 NAT loopback 경로이며 독립 외부/셀룰러 성공이 아니다. 인증서 검증 유지·무인증401·PC 적용0·원측정/보호 원본 불변을 확인했다. 기기에 모바일 인터넷이 없어 이동통신 왕복은 미검증이다. 새 선택 UI나 전체 공개 운영 준비 판정과 구분하며 게시 담당의 새 실행은0이다. [범위별 후속 기록](../reports/ToolInventory/20261109_R17_NAT_LOOPBACK_APP_TRANSFER.json). **2026-11-10 후속 사진 등록:** 검수 담당의 제품별 사진 폴더 TLS 계약24/24·저장/정리 동시실패 재시작 반례 해소와 실제 폰의 두 제품3사진 등록·원본 SHA/바이트 보존을 저장 근거로 확인했다. 새 사진 전송은 같은 Wi-Fi 공인주소 NAT loopback이며 이동통신은 미검증, PC 형상 적용0이다. 기존 원본·서비스의 정상 전환 보존을 확인했고 게시 담당 새 실행0이다. [사진 업로드 범위](../reports/ToolInventory/20261110_ANDROID_DIRECT_PHOTO_UPLOAD_SCOPED_RUNTIME.json). **2026-11-10 별도 셀룰러 후속:** 기존 앱5/r18-photo1에서 제품 폴더를 명시 생성/선택해 합성 PNG1장 등록·같은 파일 중복 억제를 확인한 저장 근거를 대조했다. 전후 기본 CELLULAR/VALIDATED이고 Wi-Fi 꺼짐, 네트워크·서버·인증서 설정 변경0·TLS USB reverse0·새 빌드/설치0이다. 기존 PC선택·7프로젝트 요약 보존, 이 폰의 작은 PNG/중복 범위만 통과이며 다른 통신사·로밍·장시간·셀룰러 JPEG/WebP는 미검증이다. [셀룰러 후속 범위](../reports/ToolInventory/20261110_ANDROID_CELLULAR_PHOTO_UPLOAD_SCOPED_RUNTIME.json). |
| Android Java APK 빌드 도구 | 기존 API35 revision2, Build Tools35.0.1, Temurin17.0.20.1+1 | 검수 담당의 aapt2 2.19-12874835·D8 8.6.2-dev·apksigner0.9 및 java/javac 버전 확인, android.jar·zipalign 파일 존재 확인. Gradle은 PATH에서 발견되지 않음. 후속 중간 후보에서 기존 도구 패키징·정렬·수동 서명 v2/v3·설치 및 실제 SAF 파일 왕복이 확인됐다. 후속 동시 rollback 독립 재시험과 수정 Windows 전체 빌드(기존키 재사용/별도 시험키 최초 생성)가 통과했다. 기존키 APK 업데이트 후 초안 보존도 확인했다. 수정 PC 실행기도 AI 서버 없이 파일 교환 화면 시작·원본 복사 보존·재실행 보존이 통과했다. 독립 판정은 이 PC와 S24의 오프라인 파일 교환 범위 통과이며 전체 제품·스토어 출시는 별개다. 회전·실제 다중손가락·비행기모드 미시험. [범위별 실기와 해결 기록](../reports/ToolInventory/20261109_ANDROID_OFFLINE_SCOPED_ROUNDTRIP.json). 후속 r17 빌드도 기존키 v2/v3로 통과하고 같은 서명 업데이트 설치를 완료했다(versionCode2/r17-1). 당시 연결 메뉴 표시만 확인했으며 실제 앱 pairing/송수신은 미검증이었다. [후속 제한 기록](../reports/ToolInventory/20261109_R17_LOCAL_DEPLOYMENT_APK_REVIEW.json). 버튼 UI 후속 실제 빌드는 --replace-version/최종badging versionCode3/r17-ui1·기존키 v2/v3·같은서명 설치/편집기 로드가 확인됐다. native12/360CSSpx웹4 범위만 통과했으며 큰글씨/회전/TalkBack/내보내기 성공·취소/외부 연결은 미검증. [UI 범위별 검수](../reports/ToolInventory/20261109_UI_BUTTON_STATE_SCOPED_RUNTIME.json). 추가 도구 설치/다운로드 없음. [직접 빌드 절차](ANDROID_OFFLINE_APK_BUILD.md) · [확인 범위](../reports/ToolInventory/20261109_ANDROID_OFFLINE_BUILD_TOOLS.json) **2026-11-10 후속 빌드:** 기존 도구·키로 실제 Windows versionCode5/r18-photo1 빌드·v2/v3·INTERNET만·동일서명 업데이트 설치와 기존 초안/페어링 보존을 검수 담당이 확인했다. Windows native124/124·fix01 34/34·launcher50 통과, symlink조건1건 미검증이다. 새 도구 설치/다운로드0이며 [실기 범위·한계](../reports/ToolInventory/20261110_ANDROID_DIRECT_PHOTO_UPLOAD_SCOPED_RUNTIME.json)를 따른다. |
| Android SDK Platform-Tools / adb | 기존 설치본 Platform-Tools 37.0.1, ADB CLI 1.0.41 | 2026-11-09 초기 읽기 전용 기기 확인 후 사용자가 현재 폰의 별도 USB 로컬 시험을 명시했다. 후속 독립 검수에서 실제 확대·점 선택·원본 사진 한 픽셀 미세 이동·저장·Chrome 메뉴 재로드 후 좌표/revision 유지와 PC 전체 구성의 의도한 변경만 일치를 확인했다. 게시 담당은 저장 보고를 대조했으며 추가 기기 조작 없음. 전체 프로그램/실제 다중 터치 통과는 아니며 외부 인증 저장 문제는 미해결·이동통신 검수는 보류다. 사용자 계속 사용 지시로 시험 탭과 소유 reverse를 유지했으며 USB/ADB 연결에 의존한다. Wi-Fi·VPN·보안·인증 설정 변경 없음. [USB 검수 절차](ANDROID_USB_EXISTING_PAGE_REVIEW.md) · [제한 실기 기록](../reports/ToolInventory/20261109_ANDROID_USB_SCOPED_REVIEW.json) · [공식5자료 학습 범위](../reports/ExternalLearning/20261109_ANDROID_USB_EXISTING_PAGE_STUDY.json) **2026-11-10 후속 설치 앱:** 사용자 승인된 업데이트 뒤 실제 시스템 사진 선택 취소·제품별 생성/선택·PNG/JPEG 업로드·동일제품 중복 억제·다른제품 별도 등록과 PC 표시를 확인했다. 기존 초안·페어링·PC선택 상태를 보존했고 전송은 같은 Wi-Fi의 NAT loopback으로서 USB reverse나 새 사진의 이동통신 성공이 아니다. WebP는 fixture만, TalkBack/프로세스 kill은 미검증이며 게시 담당 기기 조작0이다. [제품별 사진 등록](../reports/ToolInventory/20261110_ANDROID_DIRECT_PHOTO_UPLOAD_SCOPED_RUNTIME.json). **2026-11-10 별도 셀룰러 후속:** USB 승인은 사용자가 직접 완료했고 제어/검수 파일 전달에만 사용했다. 기존 APK5/r18-photo1의 실제 시스템 선택·제품별 PNG등록1·동일 파일 중복1/활성1 유지와 앱 페어링·PC기존 상태 보존을 확인한 보고를 대조했다. 전송은 CELLULAR이며 TLS reverse가 아니다. 임시 페어링 PC/폰 사본과 폰 검수 사진 정리를 확인했고 새 설치·네트워크설정·게시 담당 기기 조작은0이다. [별도 실제 셀룰러 기록](../reports/ToolInventory/20261110_ANDROID_CELLULAR_PHOTO_UPLOAD_SCOPED_RUNTIME.json). |
| cloudflared | 과거 2026.10.7 Windows 포터블 확인; **현재 사용 금지·실행파일 부재** | 2026-11-09 최신 사용자 지시로 Cloudflare를 사용하지 않는다. 독립 검수 담당은 기존 포터블 EXE 부재·소유 프로세스 부재를 관찰했으며 직접 삭제했다고 주장하지 않는다. 앞선 version/help 및 익명 차단 시험은 역사적 근거이며 현재 준비 완료가 아니다. 신규 외부 경로를 열지 않고 오프라인 앱의 수동 파일 교환으로 전환한다. [최신 제한 상태](../reports/ToolInventory/20261109_ANDROID_OFFLINE_BUILD_TOOLS.json) · [이전 제한 실기 기록](../reports/ToolInventory/20261109_CLOUDFLARED_PROTECTED_MAY_REVIEW.json) |
| Tailscale / Serve | 1.104.5 공식 유효 서명 설치, CLI/기기 연결 및 비공개 HTTPS 프록시 활성 | 2026-11-04 사용자 직접 관리자 승인·PC/Android 로그인·HTTPS 동의 완료. 온라인 Android 피어, Serve 배경 연결, 실제 HTTPS 모바일 화면/문서 200 및 임의 Host 403 확인. 휴대폰 이동통신에서 실제 모델 표시·성능은 확인 요청 중. [설치·연결 기록](../reports/ToolInventory/20261104_TAILSCALE_INSTALL.json) · [접속 매뉴얼](CHILI3D_LOCAL_CAD.md#외부-휴대폰-접속의-준비와-승인-경계) |
| Unity Editor | 확인한 기본 설치 폴더 6000.6.7f1 | 프로젝트가 요구하는 정확한 Editor/URP/빌드 모듈과 일치하는지 확인. 과거 프로젝트 기록의 6000.3.27f1과 혼동 금지. 현재 Editor 실행은 미검증 |
| GIMP | 3.0.8.2 | 이미지 편집. 설치 기록 확인, 이번 작업에서 앱 실행/플러그인 검사 안 함 |
| Adobe Substance 3D Designer | 16.0.4 | 설치 등록·실행 파일 버전 일치. 재질 그래프·맵 제작 도구이며 이번 실행/기능 검증 없음 |
| Adobe Photoshop 2026 | 등록 27.8.0.13 / 실행 파일 27.8 | 사진 표본·복구·심리스 편집용 설치 확인. 기존 Beta 설치 기록과 구별하며 실행·계정·플러그인 미점검 |
| Adobe Substance 3D Modeler | 등록 1.22.7 / 실행 파일 1.22.7.1239 | 설치 파일 확인. 이번 모델링 기능/실행 검증 없음 |
| Adobe Substance 3D Stager | 3.1.8 | 설치 등록·실행 파일 버전 일치. 이번 배치·렌더 기능/실행 검증 없음 |
| Photoshop Beta | 28.0.0.3709 | 이미지 편집. 설치 기록 확인, 실행·로그인·라이선스 상태 미점검 |
| AnythingLLM | 1.17.0 | LLM 클라이언트·문서/도구 연결. 현재 제공자·잔액·연결 상태 미점검 |
| Ollama | 0.40.8 | 로컬 모델 실행. Qwen 전용 모델 저장소·포트와 기본 설치를 구별. 기본 모델 목록이 비어 있어도 전용 모델 부재로 단정하지 않음 |

## 설치·실행 미완료 및 사용 보류

| 프로그램 | 현재 상태 | 남은 조건 |
|---|---|---|
| VideoReverse | 소스·독립 환경 설치 | 외부 AI API 미연결. mock 시연만 확인, 실제 내용 역분석에 사용 가능하다고 보고하지 않음 |
| Substance 3D Painter | 기존 연결·사용 기록은 있음 | 사용자의 별도 지시 전 상태·사용량·연결·실행·재시작 확인 금지. 이번 Claude 개별 재개로 Painter 조회를 재개하지 않음 |

## 작업별 먼저 확인할 조합

2026-11-01 저장 위치 이동 확인: Stable Fast 3D·Materialize 데이터와 Qwen 전용 모델은 UE 보조 볼륨으로 전환하고 기존 경로 연결을 유지했다. 36,231개 파일 사본의 전체 크기·SHA256 대조 통과. Qwen은 실제 새 모델 위치를 지정한 뒤 생성 응답 통과, SF3D 서버 재기동·구성 API 통과, Materialize는 재실행 프로세스 확인(이동 후 UI 재캡처 미완료). RealityScan은 폴더 권한 문제와 관리자 승인 취소로 기존 설치 위치를 유지하며 검증 사본만 준비됐다. 안전 백업 정리는 실행 차단으로 미완료여서 기존 볼륨 공간 회수와 네 도구 전체 이동 완료를 주장하지 않는다. 정확한 위치·백업·오류는 비공개 설치 기록을 따른다.

- 영상 내용·제작 과정 분석: FFmpeg/FFprobe → FrameLens → Qwen → 원본 직접 검토.
- 이미지·표면 무늬 분석/편집: Qwen + PhotoCraft, 필요 시 설치된 이미지 편집기의 실제 사용 가능 여부 확인.
- 모델·UV·재질 제작: Blender + 승인된 참고자료·제작 가이드. 사진 한 장에서 원본 노드/제작 이력을 정확 복구한다고 가정하지 않음.
- 게임 제작: 프로젝트와 맞는 Unity Editor·모듈 확인, .NET 독립 검사는 별도 활용.
- 게시·공유: Git/GitHub CLI와 이 공용 자료실의 편집 규칙.

일반 설치·설정 작업은 사용자 지시로 보류 중이며 Stable Fast 3D·RealityScan·Materialize만 개별 지시로 재개했다. 추가 설치가 필요하면 [공통 규칙](COMMON_TOOL_POLICY.md)에 따라 요청한다. 공개 목록에는 개인 PC 절대 경로·인증정보·제품 내부 파일을 싣지 않는다.

Claude는 별도의 개별 모델링 지시로 기존 설치의 조회·사용만 재개했다. 설치·전역 설정·사용량 추가 구매를 재개한 것은 아니며, 다른 작업의 기존 보류와 Painter 조회 금지는 그대로 유지한다.


## 2026-11-05 MD9 제한 기능 실기 후속

기존 MD9에서 독립80×50mm 시험판 두 장,20×2mm 닫힌 내부 홀 변환,50/50/80mm 세 변 봉제와 상단 개방, 별도 프로젝트 저장·재열기 및Thin/mm100%/Multiple Objects OBJ 출력을 확인했다. 원래 빈 문서는 별도 보존 후 재열었다. 독립 파일 검수에서54정점·70삼각면·두 판·홀 하나의 경계와 유효한UV 참조를 확인했다. 판 높이 최대 잔차+0.002197mm, 홀 폭 잔차+0.001221mm를 기록했으며 제품 허용오차를 정한 것은 아니다. UV는 판별 중첩·0~1범위 밖이어서 텍스처 전달 전 패킹이 필요하다. 시뮬레이션 시작·정지는 실행했지만 지지물 없는 판이 시야 밖으로 이동하여 형태 안정성은 미검증이다. 제품의 수납·가죽 물성·단면·제조 품질, 외부MD MCP/Python API·라이선스 검증은 포함하지 않는다. 앞의 미실행 기록은 당시 시점의 상태다. [적용 매뉴얼](MARVELOUS_WALLET_PATTERN_WORKFLOW.md)을 따른다.

순수 캐시의 드라이브 이전은 실행 환경·설정 전체 이동과 구별한다. [Windows 캐시 이전 절차](WINDOWS_APP_CACHE_RELOCATION.md)는 복사·연결·잠금·MSIX 경로·복구·재시작 검증을 구분하며 앱의 공식 캐시 설정을 대신한다고 보증하지 않는다.

2026-11-05 추가 독립 쿠폰에서 실제 패턴 Name 필드 입력과 일반 곡선 생성, ZPRJ 저장·재열기 후 이름·곡선·기준 치수 유지를 확인했다. 정확 이차 Bézier 제어점과 2D 절대 수치 배치는 미검증이다. 현행 공식 문서 5개와 MD9 현지 결과의 차이·자동화 입력 제한은 [이름·곡선 제한 실기 절차](MARVELOUS_WALLET_PATTERN_WORKFLOW.md#11-md9-패턴-이름곡선의-제한-실기-근거)에 기록했다. 다른 제품 파일의 해당 변경 완료를 뜻하지 않는다.
