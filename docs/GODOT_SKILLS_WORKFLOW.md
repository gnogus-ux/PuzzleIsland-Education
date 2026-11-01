# Scenario Godot14 문서 학습 매뉴얼

2026-11-01 · 고정 커밋 `7f4b801c7248d51b093ec365aceb114bd06139e6`. SKILL14 본문·family README·expert traps/critique·performance critique 전체를 읽었다. [개별 색인](GODOT_SKILLS_INDEX.md)과 [학습 기록](../reports/ExternalLearning/20261101_GODOT_READING_VERIFICATION.json)에 정확한 출처·줄·SHA가 있다. 모든 Godot 실행·설치·코드 시험·MCP·내보내기·유료 생성·원본 영상 재생은 미실행이다.

## 근거와 목적

원문 대상은 Godot4.7.2 standard와 주로 macOS Apple Silicon이다. 저자는 실제 시험 결과를 보고하지만, 여기서 재현한 성적이 아니다. Windows runner에서 확인했다는 범위도 locks·복사·일부 jobs/capture·debug APK 정도로 제한되고 전체 family 실기는 macOS다. family의 written 비교 점수는 게임 완성 품질의 통계가 아니며 저자도 단일 평가와 반례를 명시한다.

family README의 “모든 절차 실기”라는 표현과 본문에 명시한 미실행 항목은 함께 읽어야 한다. 휴대전화 설치/열 검수, store upload, Apple 서명/공증, AAB/bundletool, xcodebuild, C#, netfox/일부 backend, 실제 Scenario 생성, native build와 GitHub runner workflow 등은 저자도 미실행이다. test/archive 경로는 저자의 빌드 프로젝트 출처이며 이 저장소에 포함된 시험이라고 가정하지 않는다.

실제 프로젝트가 정한 엔진·기기·화면 방향·Safe Area와 기존 경로 탐색을 유지한다. 이 자료는 다른 엔진의 설계·검수 지식을 재사용하기 위한 것이며 Godot로 이전하거나 새 온라인·전투·플랫폼 이동을 추가하는 요청이 아니다. 도구 설치·설정 보류와 금지 앱 조회도 유지한다.

## 공통 실행·인계 계약

실제 Godot 작업이 별도로 승인되면 대상 버전·renderer·physics·장면·기기·프레임 예산·보존 범위부터 정한다. GUI editor와 headless가 같은 프로젝트를 동시에 쓰면 다음 저장으로 덮어쓸 수 있으므로 한 작성자만 쓴다. 사용자 앱을 강제로 종료하지 않는다. 원문의 Windows process 탐지는 command line에 프로젝트가 없는 editor를 놓칠 수 있어 탐지 통과만으로 점유가 비었다고 단정할 수 없다.

작은 idempotent 작업에 owner와 명시 save를 둔다. 새 node를 add_child한 것과 scene에 저장된 것은 다르다. live editor 편집은 해당 undo 경로를 보존한다. scratch마다 user://를 분리해 저장·입력·shader cache가 섞이지 않게 한다. 실제 설치 위치/프로세스 조회는 승인된 앱과 작업 범위에 한정한다.

논리·import·audit는 headless, 렌더/particle/GPU 비용은 windowed 같은 적절한 경로를 고른다. parse error에도 exit0이 나온다는 저자 사례가 있으므로 결과 envelope·오류 로그·실제 artifact를 함께 본다. unknown flag·check-only·리소스 exists 하나를 성공 증거로 삼지 않는다. 모든 await/작업에는 종료 조건을 둔다. 그러나 원문의 “headless만 truth”도 절대화하지 않는다. 실행 로그와 현재 디스크/에디터 상태·의도한 렌더러를 함께 확인해야 한다.

최종 인계는 brief/수치, 실제 사용 channel, 변경과 원본 보존, 실행한 검사와 로그/JSON, 동일 카메라 전후 이미지, 기기/driver/scene 조건, 완료/부분/미검증, 남은 문제와 허용 범위로 한다. 원문의 Verified/Assumed와 이번 문서의 문서학습/실기미실행을 구별한다.

## architecture · 데이터·저장·입력

scene이 단독으로 실행되도록 의존성을 위에서 주입하고, call down/signal up/event out으로 연결한다. 모든 프로젝트에 같은 event bus·autoload 개수를 강제하는 뜻은 아니다. 정의는 typed Resource, 개체 health/cooldown/stack 같은 가변 상태는 개체별로 분리한다. Resource 공유와 외부 subresource 복제 깊이를 확인하고 한 chest의 inventory 변경이 다른 chest에 퍼지지 않게 한다.

export의 경로 대소문자·registry·remap을 검수한다. runtime 디렉터리 순회는 무조건 불가능한 것이 아니라 원본 확장자 검색이 pack의 remap과 달라질 수 있다. edit-time catalog나 지원하는 ResourceLoader listing으로 실제 pack에서 확인한다. `.uid`와 원본 소스의 연결을 보존한다.

저장 파일은 code를 로드하는 경로로 취급하지 않는다. architecture는 JSON envelope(format/version/data), 원자적 tmp/bak/rename, 마이그레이션을 권한다. gameplay에는 검사한 Resource save 경로도 있으나 문자열 scan만으로 임의 코드가 안전해지지는 않는다. 외부/사용자 제공 save는 데이터 allowlist·타입·범위·크기 검증을 갖춘 비실행 형식을 우선한다. JSON의 native type 변환도 object 허용 여부와 null/실패 처리를 실제 버전에서 확인한다. remap ConfigFile도 원문의 parse/object 가능성 경고와 함께 다룬다.

입력은 action table을 한곳에서 만들고 physical key·pad device·로컬 다인 기기 분리 정책을 명시한다. device -1은 모든 패드를 받으려는 경우의 예제이며 로컬 multiplayer 정답이 아니다. menu click 소비와 gameplay unhandled 입력을 구분하고 실제 pad·touch·다른 키보드 배열도 확인한다.

## 2D · pixels·controller·camera

픽셀 아트인지 smooth 2D인지 먼저 정한다. base 해상도·viewport/canvas_items·integer 확대·filter·카메라 보간이 서로 영향을 준다. 원문의640×360/320×180·Exclusive Fullscreen은 데스크톱 픽셀 예제다. 현재 3D 가로 모바일 화면의 해상도 정책으로 복사하지 않는다.

점프는 높이와 apex 시간으로 시작해 실제 물리 tick에서 높이·buffer/coyote 움직임 수·모서리 걸림·접지를 측정한다. 공식 보정 g·dt/2는 해당 적분/컨트롤러 예제이며 모든 이동 구현에 자동 적용하지 않는다. top-down은 감속 부호 반전·대각 속도를 확인한다. 카메라 lookahead·damping·착지 재기준과 interpolation을 프레임/물리 빈도 조건별로 검수한다.

TileMapLayer/TileSet의 terrain mode·peering bit·실제 그림을 sampler로 대조한다. 인덱스가 맞아도 틀린 art가 이어질 수 있다. sprite ground registration·pixel grid·alpha fringe·y-sort의 발 원점·parallax 줌아웃 틈을 함께 본다. generated art는 제작 출처와 원본 크기를 manifest로 받고 import 전후에 검사한다.

## 3D world · geometry·asset import

캐릭터 높이·capsule·door·stairs·ramp·카메라 충돌을 같은 규격으로 설계한다. 카메라 상대 방향은 수평 성분을 먼저 정규화해 pitch에 따른 이동 감속을 막는다. step은 capsule 이동량만이 아니라 실제 tread·바닥 아래 ray로 판정하며 ledge에서 강제 snap-down되지 않는지 본다. 원문의 성인1.8m·0.45m step은 루미 규격이 아니다.

CSG blockout·GridMap·terrain·MultiMesh의 목적을 분리한다. 동적 CSG 비용, 닫히지 않은 operand의 무시, cell 충돌, HeightMap 실제 표면과 collision, region 정렬/할당 면적, MultiMesh buffer 저장과 culling box를 검사한다. Terrain3D1.0.2의 수치·API와 .res 권고는 해당 버전의 출처이며 설치를 뜻하지 않는다. streaming은 load/unload 반경 차이와 baseline node 복귀·최악 프레임으로 검수한다.

AI GLB는 generator 문자열만으로 판별할 수 없다. manifest의 source·크기·피벗·방향·budget·충돌을 기준으로 분류한다. authored DCC를 전부 같은 높이로 맞춰 의도된 크기 차이를 없애지 않는다. importer 바깥 tree에서 owner/local transform/reparent의 동작을 확인한다. glTF 확장 지원·빠진 clearcoat/transmission 등 재질 의미·LOD0·추출 texture VRAM은 원문 4.7.2의 관찰이며 다른 버전에서 재확인해야 한다.

## gameplay · AI·navigation·persistence

순수 decision과 body를 분리해 입력 없이 규칙을 시험할 수 있게 한다. enum/FSM/behavior tree/GOAP는 누가 행동을 작성하고 얼마나 재조합하는지에 따라 고른다. update를 분산하고 실제 agent 수에서 비용과 stuck/관통/orphan을 함께 측정한다. 원문의 M5Max200agent 약2ms는 Android 성능 보증이 아니다.

navigation은 bake source를 정적 collider group으로 제한하고 region 변경이 실제 map에 적용된 뒤 path를 읽는다. avoidance는 벽을 아는 pathfinding의 대체가 아니다. tick당 path 갱신·도착 판정·threshold·속도 관계를 검수한다. 기존 이동 방식을 이 교육 때문에 NavMesh로 바꾸지 않는다.

hitbox/hurtbox의 layer/mask와 한 swing당 HitLog, 고속 projectile의 ray sweep/CCD, friendly fire·관통·자기 타격을 검사한다. procedural content는 seeded data와 validator→geometry/path→시각 확인으로 간다. 천 개 seed·0 overlap 같은 표본 조건은 모든 게임의 필수 기준이 아니며 실제 기획에 맞춘다.

## animation · import·state·root·IK

gameplay가 속도·상태를 소유하고 animation은 표현한다. imported bone 이름·BoneMap·track resolution·RESET·loop를 확인한다. tree의 condition/expression과 advance mode, 여러 전이의 우선순위, OneShot bone filter를 실제 scripted drive로 본다. 빠진 track만으로 upper-body layer가 정의되는 것은 아니다.

clip의 planted foot 속도와 retarget body의 motion_scale를 측정해 controller와 blend point를 맞춘다. root motion은 실제 Root와 좌표 공간을 명시하며 Hips 흔들림을 그대로 쓰지 않는다. IK position과 발 회전은 다른 문제이고 modifier 순서·influence 적용 후 실제 최종 pose를 읽어야 한다. pose 누적 저장 예제가 animation을 덮어쓰지 않는지 확인한다. 원문의2mm·2cm gate와 Rigify preset은 예제 조건이다. 현재 루미 움직임/리깅 보류를 해제하지 않는다.

## rendering-lighting · shaders · VFX

renderer와 static/dynamic·기기 범위를 먼저 정하고 lookdev에서 기준을 잡는다. static lightmap/동적 GI·reflection probe·UV2·bake mode·수렴 시간·실제 leak를 함께 본다. Mobile/Compatibility fallback에서 사라지는 기능은 목록으로 남기고 낮은 tier에서도 승인 분위기가 유지되는지 확인한다. 원문의 AgX·key 비율·focal contrast·고정 clip 비율은 스타일별 조정값이다. 기획된 순백/암전 이미지를 자동 uniform 검사만으로 실패 처리하지 않는다.

shader는 각 renderer compile → 실제 draw → 여러 mesh/scale/rotation parameter sweep → reference/시각 → GPU baseline 순서다. headless compile 통과가 backend draw 성공은 아니다. color와 data sampler, object/world space, shared material의 instance uniform, global registration, reversed-Z·depth branch와 transparent pass를 구분한다. VisualShader를 코드로 생성했다면 GUI 손편집으로 보고하지 않는다. compute의 main/local RenderingDevice와 render thread·RID 해제·CPU parity를 계약한다. shader baker의 windowed 필요·pack 증가·로그는 실제 export에서 입증해야 한다.

VFX는 flash/fire/smoke/sparks/debris/ring/light 같은 작은 층을 시간 순서로 설계한다. vertex color·billboard scale·trail mesh·sub-emitter cap·실제 level collider가 적용되는지 audit한다. visibility AABB는 실제 scale/이동/충돌을 포함해 확인하고 particle 충돌을 gameplay damage의 근거로 쓰지 않는다. 낮은 tier는 amount와 지원 layer를 줄이며 CPU fallback에서 잃는 기능을 기록한다. amount_ratio 감소만으로 같은 비용이 줄었다고 주장하지 않는다.

effect timeline·fixed seed·실제 시각과 lifecycle·baseline node 복귀를 함께 확인한다. hit-stop은 기존 time_scale·중첩·취소 복원을 소유해야 한다. 원문의 고정1.0 복원은 기존 slow motion이 있는 게임의 범용 규칙이 아니다. shake off·접근성·과도한 화면 점유도 기획에 맞춰 검수한다.

## UI · localization·accessibility

컨테이너 최소 크기·Expand/Fill·anchor/offset·grow 방향을 역할별로 정하고 Theme/StyleBox의 공유 상태를 확인한다. HUD root는 수동 입력을 불필요하게 가로채지 않게 하고 값은 signal에 따라 갱신한다. focus 시작점·menu stack·covered panel·복귀 대상·모든 기기의 navigation을 명시한다.

화면 크기/긴 가로/Safe Area·locale·UI scale matrix에서 offscreen·겹침·text clipping을 수치와 실제 이미지로 검사한다. CJK·RTL·plural·긴 번역·pseudolocalization·font fallback과 실제 배포 font를 확인한다. system font가 개발 PC에서 보인다는 이유로 대상 기기에 존재한다고 가정하지 않는다. 원문720×720/sensor는 양방향 공용 UI의 예제이며 현재 가로16:9 방향을 바꾸는 근거가 아니다. 48dp를 물리 pixel과 동일시하지 않고 실제 기기 밀도·접근성 기준을 확인한다. screen reader는 이미지나 코드만으로 통과할 수 없다.

## audio · 숫자 검사와 듣기

bus 이름·routing·voice cap·거리·cooldown·priority·adaptive music 전이표를 데이터로 설계한다. bus rename 뒤 Master fallback, listener·area_mask·공간 감쇠·reverb/occlusion을 실제 loaded resource와 mixer에서 확인한다. generated sound의 silence·peak/loudness·loop seam은 길이와 용도에 맞춰 처리한다. stereo를 무조건 mono로 바꾸거나 모든 source를 -18LUFS로 맞추지 않는다.

voice cap만 있으면 같은 tick start/end로 pulse가 생길 수 있어 takes·cooldown·거리로 비용과 반복을 함께 조절한다. interactive music은 모든 도달 가능한 전이·hold/return·beat 위치를 검사한다. headless Dummy의 speaker silence와 내부 mixer 측정 가능 여부는 다르다는 저자 교정이 있다. waveform·spectrogram·LUFS는 musicality·반복 피로·자연스러운 reverb의 청취를 대체하지 않으며 청취 미실행을 명시한다.

## multiplayer · network contract

이 주제는 현재 게임에 온라인 추가를 승인하는 것이 아니다. 실제 필요시 object별 authority·복제 property/mode/interval·event/RPC·client 요청을 먼저 문서화한다. sender는 await 전에 읽고 owner·값·rate·상태를 서버가 검증한다. 서버 권한도 다른 client에 보낸 위치 정보의 wallhack을 해결하지 않으므로 interest management를 따로 본다.

server+2~3client·late join/leave/reconnect·위조 입력·delay/jitter/loss·대역폭을 각 process와 일관된 code/schema에서 시험한다. localhost 성공만으로 network 완료라 하지 않는다. RPC checksum이 method name만 본다는 저자 관찰에 의존하지 않고 모드/인수/transfer/channel까지 맞춘다. ENet/WebSocket/WebRTC의 신뢰성·browser 제한·TLS·head-of-line을 구분한다. dedicated server는 export feature·시각 자산 제외·실제 boot와 client 접속으로 검증한다. 원문 backend·rollback 예제의 미실행 범위를 유지한다.

## pipeline · performance·release

ingest는 byte parser·manifest·budget·source 분류→sidecar→import→texture pass→실제 resource audit→thumbnail→재실행/한 파일 변경→export/pack 검수로 간다. 개수 합계·reject 이유·duplicate와 변화 없는 재실행을 기록한다. test는 public behavior·signal·bounded wait·실제 실패 사례로 검증하고 JUnit0test를 성공으로 취급하지 않는다. headless GUI input은 synthetic viewport test 가능한 부분과 실제 device/특정 framework가 skip하는 부분을 구분한다.

shutdown crash 뒤 artifact가 존재하는 경우도 byte/pack/load 검증과 crash 원인을 따로 기록한다. 누수·RID 경고를 모두 무시하거나 종료코드0만 통과시키지 않는다. 원문의 특정 noisy fixture whitelist는 사용자 프로젝트의 broad ignore 정책이 아니다. editor plugin owner/save/undo, native extension·CI·tool 설치는 명시된 범위에서만 하고 이번에는 실행하지 않았다.

성능은 같은 scene·해상도·driver·warm/cold·실행 시간에서 before/after를 비교한다. CPU/GPU bound와 fill/geometry/shadow를 나누고 pipeline compile/loading hitch를 구분한다. Metal0ms는 비용0의 증거가 아니며 headless loop time을 실제 GPU FPS로 보고하지 않는다. Mac/Vulkan proxy는 최종 Android frame·메모리·열 검사를 대신하지 않는다. 30분 soak·5%/0.1ms noise floor는 원문 시험 제안이며 프로젝트 조건에 맞게 정한다.

export는 정확한 template/version·preset·renderer·파일목록/size·실제 exported boot·서명·대상기기 단계가 따로다. Xcode project 생성은 IPA/설치/서명/스토어 완료가 아니다. Web은 실제 제공 host의 압축 byte·thread/headers·browser/audio/백그라운드 동작을 확인한다. Android는 debug와 release signer/ABI/version·Safe Area·권한을 검증한다. 계정·keystore·billing 정보는 공용 문서에 넣지 않는다. 파일 export 성공을 업로드·배포로 부르지 않는다.

## 충돌과 적용 전 확인 목록

| 원문 내 차이/일반화 | 교정 |
|---|---|
| architecture JSON만 / gameplay checked Resource·ConfigFile | 외부 save의 code 실행 가능성 우선. scan을 안전 보증으로 삼지 않음 |
| headless GUI input skip /expert viewport.push_input 가능 | 테스트 경로·framework·실제 device를 구분 |
| MultiMesh headless 금지 /buffer 직접 할당 대안 | helper 경로와 저장 buffer를 실제 재열기로 확인 |
| expert iOS project artifact 지원 /performance helper IPA 부재 실패 설명 | helper revision·artifact 종류를 기록. project와 IPA를 따로 판정 |
| Mobile 기능 설명과 SSAO 제외 문구의 불명확한 목록 | renderer/버전 실제 feature matrix·draw 결과 확인 |
| Jolt를 항상 쓰라는 gate | brief·기존 프로젝트 physics 우선, 설정 선택과 실제 probe를 구분 |
| UI 배경의 “6.3 traps” | 본문·family는4.7.2 대상. 오탈자로 보고 버전 근거로 사용하지 않음 |
| 모든 경고·누수 whitelist | 정확한 재현된 소음만 분리하고 새로운 경고는 원인 확인 |
| headless/export/test 저자 성적 | 문서의 관찰이며 로컬 실기 성공으로 이전하지 않음 |

현재 부족한 것은 실제 설치/버전·프로젝트·기기에서의 재현 근거다. 구체적인 Godot 제작이 승인되면 필요한 API·참조 절차를 추가 확인해야 한다. 이 문서와 색인 작성 완료는 게임 기능·성능·배포 검증 완료가 아니다.
