# Scenario 서비스 79주제 탐색표

2026-11-01. [적용·검수 매뉴얼](SCENARIO_SERVICE_SKILLS_WORKFLOW.md)과 함께 읽는다. 원본 Scenario Labs skills, 고정 커밋 `7f4b801c7248d51b093ec365aceb114bd06139e6`, MIT. 아래 79개 SKILL 본문은 전체 읽었다. 링크는 해당 고정 본문이다. 본문이 연결한 scripts/reference/template 내용은 이 범위에서 미검토이며 실제 작업 전 필요한 파일을 따로 읽어야 한다. 목록·해시만 확인한 보조 파일은 151개다.

표의 도구명·절차는 **원문에서 읽은 계약**이며 실제 호출한 결과가 아니다. 스키마·가격·가용성·한도·플랫폼 규격은 현행 검증이 필요하다. 모든 주제에 공통 규칙·승인 범위·설치 보류·앱 조회 금지·원본 보존이 적용된다. 표의 “검수”는 다음 작업의 계획이며 이번 실행 PASS가 아니다.

| 본문·전체 행수 | 찾을 주제 | 필요한 입력·선행 확인 | 원문의 작업 분기 | 검수·실패 시 남길 것 |
|---|---|---|---|---|
| [scenario-3d] · 245 | mesh 생성·정리·rig 경계 | 승인 concept·뷰·face 예산·3D Guide | img23d→UV→retexture→필요한 rig, 각 단계 schema/견적 | 실루엣·poly/tri/quad·scale·UV·maps·형식. game-ready 주장 분리 |
| [scenario-3d-worlds] · 89 | panorama→탐색 공간 | 승인 panorama·world 목적·비용 | world 검색 후 splat 생성, 기존 job 대기 | splat와 mesh 구분, 숨은 면·충돌·metric 미검증 |
| [scenario-ace-step] · 124 | song·cover·repaint·stem | 승인 가사·master·교체 구간 | mode별 member, Cover/Repaint 목적 구분 | singer/발음/구간 청취. 원본·선택 후보 보존 |
| [scenario-ad-variants] · 116 | 원본 광고의 독립 변형 | source·정확한 copy/개수·delta | 항목별 원본에서 시작, 요청 revision만 선택본 | hook 전후 frame·오디오·완료 상태. 실패만 복구 |
| [scenario-admin-analytics] · 157 | 사용·비용 분석 | 허용된 scope·기간·단위·조회 목적 | 페이지·상세 usage·cache/provenance 대조 | 할인/중복/기간 오집계, 잔액 추정 금지 |
| [scenario-asset-analysis] · 107 | caption·describe·analyze·detect | source asset·질문·분석 예산 | 고정 목적 도구와 open-ended 분석 구분 | image 수/answer 수, 배경제거 맥락, render와 실제 파일 구분 |
| [scenario-audio] · 169 | 음악·효과·TTS 공통 | 원고·음성 동의·형식·길이 | modality/member schema→견적→생성→청취 | tags·언어·실제 duration/MIME. 청취 없으면 미검증 |
| [scenario-blender] · 148 | 로컬 Scenario 확장 | 허용 연결·token·저장/점유·기능 승인 | scene read→capture→quote→generate→적용 gate | hosted/local ID 차이, 비밀 보호, GUI/headless·저장 한계 |
| [scenario-blender-2d-animation] · 154 | 카드 기반 2D 장면 | 승인 concept·layers·run clip·새 작업 파일 | 생성→key/loop→측정→orthographic scene | feet·horizon·prop count·seam·physics·상대 경로. live 초기화 주의 |
| [scenario-brand-kit] · 128 | 팔레트·로고·브랜드 응용 | 승인 brand brief·vector·폰트 권리 | specification→native vector/래스터 응용 분리 | 실제 fills/path/glyph·clearspace, critic와 법적 판단 구분 |
| [scenario-caption-studio] · 158 | 자막·SRT·번역 | clean master·원고·언어·출력 목적 | transcript→교정→지원 subtitles 입력→style | 실제 captions/segment 수·casing·cue 경계·청취. base64 계약 재확인 |
| [scenario-chatgpt-pet-create] · 172 | 새 pet sheet 제작 | 승인 identity·row 계약·v1/v2·예산 | base→row 생성→look 의미→check→package | 격자·ground·jump·방향·hash. 로컬 package≠Library/활성화 |
| [scenario-chatgpt-pet-update] · 116 | 기존 pet 최소 수정 | 원본 sheet/package·변경 row | split 기록→최소 row→rebuild→새 검수 | kept rows bytes·동일 ID·원본 보존. 무단 install 금지 |
| [scenario-consistency] · 196 | 동일 정체성·스타일 | 승인 hero·불변 특징·변형 목적 | 참조/제어 먼저, 필요 시 학습 검토 | 개별 뷰 대조·복장 새 baseline·seed 한계 |
| [scenario-elevenlabs] · 111 | TTS·dub·voice·music | 원고·권리·언어·source audio/video | member별 tags/dials·voiceId·section 계약 | 발음·배경음·dub≠lipsync·출력 형식 |
| [scenario-fan-cam] · 109 | 정체성→방송 구도 | 동의/승인 사진·행사·반응·배포 범위 | broadcast still→정체성 gate→I2V→overlays | 전체 likeness·후반 글자 누출·가짜 방송 오인, camera 구도 |
| [scenario-formats] · 89 | ratio·크기·placement 파생 | 승인 master·플랫폼·보존할 구도 | resize/crop/outpaint/recompose 선택 | actual pixels·safe zone·글자·인물 잘림. 규격 현행 확인 |
| [scenario-game-assets] · 234 | UI·tile·parallax·static art | 원본·engine layout·alpha·camera | 자산별 generator→후처리→조립 미리보기 | alpha bbox/halo·9-slice·Wang/iso·scroll bleed |
| [scenario-gemini-image] · 87 | Gemini 이미지 생성/편집 | prompt·역할별 refs·원하는 크기 | member별 refs/video·resolution/thinking 선택 | 실제 입력 소비·text·alpha·현행 스키마 |
| [scenario-gemini-omni] · 96 | Omni 영상·edit·extend | source/frame/refs·동작·audio | 모드별 member, motion과 look 구분 | append 길이·비율·정체성·새 음향. 순위 고정 금지 |
| [scenario-gpt-image] · 149 | GPT 이미지 grid/fidelity/mask | 승인 source·mask 의미·정확 크기 | member별 pixel·quality·edit 계약 | 보호 부위·halo·실제 alpha. 현행 OpenAI 정보로 단정 금지 |
| [scenario-grok-imagine-image] · 89 | Grok 이미지/edit | prompt·source·필수 특징 | edit 원본 ratio와 member resolution 확인 | 비율 무시·범위 밖 변경·정확 글자 |
| [scenario-grok-imagine-video] · 92 | Grok I2V/R2V/edit/extend | opening 또는 identity·sound 요구 | mode별 member·참조 태그·명시 길이 | edit truncation·tail·actual resolution·audio |
| [scenario-identity-library] · 111 | 승인 정체성 뷰 정리 | 승인 individual views·검색 이름 | collection 구성→검토 sheet→버전 관리 | 승인과 prefix 구분·중복 ID·membership 변화 후 재구성 |
| [scenario-ideogram] · 134 | text/transparent/edit/layerize | source·정확 copy·mask·alpha 목적 | member 기능 분리, 자동 rewrite 확인 | mask 극성·canvas·레이어 위치·철자 |
| [scenario-image] · 138 | 이미지 공통 생성·edit | brief·source/ref·ratio·예산 | recommend/search→schema→dry_run→run | 실제 크기·참조 scalar/array·변경/보존 특징 |
| [scenario-image-editing] · 137 | deterministic 효과·resize | 원본·목표 크기·비파괴 후보 | 효과와 generative reframe/upscale 분리 | 순서·grade/grain·alpha flatten·원본 차이 |
| [scenario-inspiration] · 86 | 시각 방향 탐색 | 목적·고정 축·선택/예산 범위 | prime→widen→choose→board | 후보/선정/사용자 승인 구분·참조 권리·스타일 누출 |
| [scenario-kinetic-music-video] · 269 | lyric·motion graphics MV | 승인 master·lyrics·style/canvas·예산 | analyze→treatment→footage→JS smoke→render | onset·matte·AV·모든 경계·flashes. OS/설치/담당 생성 미승인 |
| [scenario-kling] · 106 | Kling 영상·motion·avatar | mode 입력·first/ref/driver·sound | 전용/Omni payload·duration·multiPrompt 분리 | element budget·audio 배타·motion control·lip 검수 |
| [scenario-luma-image] · 86 | Luma Uni 생성·편집 | source target와 imageRef 역할 | source와 guidance 구분, member 선택 | ref 한도·누적 edit·원본 불변 특징 |
| [scenario-luma-video] · 90 | Ray·Edit·Reframe·Modify | source/frame·duration·HDR 의도 | unit-string duration·strength/keyframe 분기 | 상호배타·outpaint edges·motion·actual color/형식 |
| [scenario-mai-image] · 89 | MAI 생성·edit | 승인 source·참조·수정 delta | edit array/Pro scalar member 선택 | 필드 형태·chain 계보·원본 특징 |
| [scenario-meshy] · 98 | Meshy 생성·UV·rig | source views·예산·pose·최종 용도 | raw/remesh·정확 texture 입력·rig/animation 대안 | target count 활성 여부·PBR maps·면/UV cap·중복 rig |
| [scenario-minimax-music] · 83 | MiniMax song/cover | style·가사 또는 source·권리 | vocal/instrumental/optimizer/cover 구분 | 완성 가사 재작성·실제 melody/발음·시간 |
| [scenario-minimax-video] · 126 | H3/Max·Insert·Recast | keyframes 또는 refs·clip·audio 정책 | mode/member별 caps·resolution 대소문자 | source 상한·원본 motion·continuation lead-in·최종 sync |
| [scenario-model-comparison] · 137 | 조건 통제 모델 비교 | 같은 brief/ref·사전 기준·총 비용 | schema 정규화→견적→병행 제출→표 | 실제 cost/latency/크기·샘플 수·full size/whole clip |
| [scenario-model-training] · 150 | LoRA·dataset·voice training | reference test 실패 근거·dataset 권리·예산 | base 추천→shell→chunk→quote→start→epoch | job ID·sample prompts·중복 dataset·base 계약. 별도 학습 승인 |
| [scenario-moderation] · 162 | 차단 원인 분류 | 실제 error/hint·허용 scope·비용 기록 | provider/team gate/plan/blocklist 분리 | 우회 자동 실행 금지·정상 거절 존중·허용 지원 경로 |
| [scenario-motion-loops] · 177 | 코드 기반 반복 모션 | 팔레트·주기·canvas·기존 runtime | pure time 함수→page check→encoded QA | deterministic·seam·alpha/색·flash·font 로딩. 새 설치 보류 |
| [scenario-multi-reference] · 146 | 여러 이미지 역할 분리 | approved identity/style/pose refs | 각 ref 역할·순서·금지 복사 영역 지정 | 참조 소비·팔레트/복장 누출·array contract |
| [scenario-orbit-views] · 117 | 3D 중간물로 새로운 뷰 | 승인 사진·geometry 후보·camera zero | mesh→clay layouts→source repaint→cutout | front/back 혼동·실루엣·scale·ground/shadow. 숨은 면 추론 |
| [scenario-patina-retexture] · 170 | surface family PBR·비교 film | mesh/UV·물리 material families·Guide 범위 | inventory→family maps→역할 대조→shader→pilot | roughness polarity·geometry/UV/linked data·같은 조건 film |
| [scenario-product-shots] · 84 | 실제 제품의 연출 이미지 | 실제 승인 제품 사진·불변 checklist | 원본 제품 보존한 scene/edit 분기 | 라벨·형상·뚜껑·재질·색. 실측 물성 확인과 구분 |
| [scenario-quality-gate] · 134 | image 판정·brief 준수 | 이미지·configured brief·add-on·비용 | stored/new_analysis·rerun 구분 | 구조·개수·reference 별도 검사, 점수만 PASS 금지 |
| [scenario-reel-recast] · 130 | 같은 동작의 인물/장식 변경 | 권리·동의 source·identity·음원 | song 보존→muted ref→plate→draft→final | plate camera·전체 정체성·새 fps/길이·AV offset |
| [scenario-refine-loop] · 88 | 제한된 품질 개선 반복 | 사전 rubric·baseline·시도/비용 cap | 결함별 local/global fix 경로 | 반복 실패 중단·미해결 PARTIAL·최선 후보 보존 |
| [scenario-report] · 99 | 버그·요청 보고 | 최소 재현·허용된 공개 범위 | fact/expected/actual·job 근거 정리 | secrets/signed URLs/개인정보 제거. 발송과 초안 구분 |
| [scenario-reve] · 84 | Reve 생성·Remix | prompt·refs·member 목적 | references/frame 태그와 Remix 입력 구분 | 번호·입력 한도·ratio·정확 특징 |
| [scenario-rodin] · 86 | Full/Fast·Bang | 단일 subject views·model/image·예산 | tier/topology/HighPack·segmentation 분기 | 문자열/boolean 차이·면 증가·재질 재생성 |
| [scenario-runway] · 76 | Gen4.5·Aleph | prompt/frame 또는 편집 source·refs | generation/edit·대체 reference arrays | ratio 무시·bytes/time caps·motion 보존·전체 shot |
| [scenario-seedance] · 144 | Seedance 통합 mode | first 또는 ref arrays·태그 역할·sound | edit -1/extend tail·명시 duration·draft | actual opening/tail·Auto 비용·source motion·차단 우회 금지 |
| [scenario-seedance-drafts] · 103 | 여러 take 탐색·completion | original draft ID·budget·유효 기간 | draft 후보 전체 리뷰→선택만 completion | full-speed/closeup·cost 산술·원본 ID·final 비교 |
| [scenario-seedance-music-video] · 113 | 승인 곡에 맞춘 shot cut | master·권리·실제 beat/lyrics·story | song→story→frames→timed shots→cut | master hash와 stream identity 구분·beat/head trim·청취 |
| [scenario-seedance-storyboard] · 132 | 연속 pose chain | cast·축·entry/exit 위치·board | one scripted run 또는 N+1 boundary still | board marks·pose/position·실제 cuts·바닥 미끄러짐 |
| [scenario-seedream] · 114 | Seedream 생성·sequence·Layerize | refs·목적·alpha/출력 구조 | family별 입력/sequence/layer 계약 | array/단일·bbox/z-order·반투명 손실 |
| [scenario-side-view-game-kit] · 183 | side scroller art set | hero poses·key색·level 계획 | clips→loop/key→shared palette→layer finish | 무기/의상 key 소실·feet·lossless strip·level1 실검수 |
| [scenario-skyboxes] · 91 | 360 panorama·upscale | 승인 look·2:1/360 목적 | skybox member→전용 upscale | wrap/poles·실제 dimensions/layout·HDR 의미 |
| [scenario-sonilo] · 89 | SFX·music·video soundtrack | clip·segment 범위·반환 track/mux | SFX/music 및 video/audio 반환 분기 | contiguous timing·speech flag·기존 foley 소실·청취 |
| [scenario-sparc3d] · 77 | 단일/multiview mesh | 동일 subject front/back/left/right | base/Portrait·member별 requestType | no prompt·face/resolution 존재·출력 타입·장시간 pending |
| [scenario-sprite-animation] · 190 | cycle/grid/frame pipeline | 정확 frame count·baseline·동작·출력 | specialty/single-sheet/video lane 선택 | 실제 poses/order/alpha·loop window·GIF cadence·mapping |
| [scenario-storyboards] · 93 | 만화·shot stills | script·cast/setting baseline·대사 | panel별 생성→정체성 gate→letter→page | 축·facing·지속 상태·개별 panel·원본 참조 |
| [scenario-team-admin] · 192 | 팀·project·member·cap | 관리 목적·실제 권한·명시 승인 | read/write/destructive lane 분리 | scope≠권한·cap 의미·block/allow·삭제 복구성 |
| [scenario-text-overlay] · 116 | exact copy·CTA·legal card | 승인 문구·글꼴·layout·원본 plate | 변수 payload→render→glyph QA→합성 | escape/raw 입력·overflow·최종 크기·alpha·폰트 |
| [scenario-textures] · 99 | seamless·PBR·tiling upscale | flat texture 또는 mesh·채널 목적 | 2D maps와3D retexture·전용 upscale | 실제 tiling/기울기·roughness 의미·target engine 규약 |
| [scenario-thumbnails] · 121 | 완성 cover/thumbnail | 승인 subject·copy·실제 feature·개수 | focal hierarchy→plate→exact type→export | 작은 preview·잘림·정확 copy·성과 실험과 구분 |
| [scenario-ugc] · 128 | phone-style creator 광고 | 승인 script·person/product·권리 | avatar/lipsync/motion/native/faceless lane | 실제 speech timing·허구 주장 금지·clip fidelity·overlay |
| [scenario-veo] · 86 | Veo 생성/reference/extend | mode·image 또는 refs·sound | full/Fast/Lite/Extend schema 분리 | duration/ref 배타·실제 audio·ratio/source 상한 |
| [scenario-video] · 217 | 영상 공통·lip·duration | 입력 종류·동작·음성·보존 조건 | T2V/I2V/R2V/edit/lip/extend 선택 | 실제 cap/floor·fullclip·입 모양·소리·format |
| [scenario-video-ads] · 84 | 새 광고 기획·제작 | real product·approved facts·board 예산 | brief→priced board→stills→video→fidelity→cut | 각 clip label/identity·safe zones·audio·발행 승인 분리 |
| [scenario-video-assembly] · 134 | concat·absolute layers | measured clip/audio·exact text cards | sequential concat 또는 overlap compose | trim 양/위치·custom canvas·0.1step·AV drift·tail |
| [scenario-video-color-grade] · 174 | LUT·mask·reference match | source color/log·look·기존 runtime | preset 또는 local recipe·still test→render | spatial은LUT외·skin/edge/flicker·frame/audio·실제 codec |
| [scenario-video-editing] · 161 | cut/split/resize/effect/alpha | 원본 actual properties·목적 형식 | scalar/array·fit·effect/sequence/key 분기 | frame 개수/순서·alpha codec·원본 audio·reframe과 구분 |
| [scenario-video-to-motion] · 113 | video→3D motion | full-body clip·기존 rig 보존 여부 | mesh auto-rig 또는 motion-only·출력 target | kind·skeleton·axes·feet·loop·import. rig 범위 승인 별도 |
| [scenario-vidu] · 90 | Vidu I2V/R2V·anchors | first/end 또는 identity refs | generationType·images 수·tier/member | 참조 video 지원·actual fps/length·BGM 한계 |
| [scenario-walkable-room] · 136 | 사진 기반 splat+props | photo·분리 movable object·support | removal plate→world, original cutouts→mesh→calibrate | metric/lens 추정·collision·support·metalness·runtime 미검증 |
| [scenario-wan] · 100 | Wan 생성/edit/animate/outpaint | mode·source·명시 audio 정책 | 세대별 size/duration·match flags | default frame/fps·expand방향·원본 track·ref 배타 |
| [scenario-workflow-authoring] · 109 | graph 생성·수정·publish | 보존한 graph·editor-info 참고·권한 | fullgraph update→publish→dryrun | stale flow·부분 create·edge방향·outputs·foreign mapping |
| [scenario-workflows] · 110 | saved app 실행·approval | ready graph·inputs_definition·scope | capped list→계약→dryrun→run→wait | required.always·array/forEach·child costs·실제 gate 승인 |

## 탐색 이후의 한계

이 표는 기능을 찾는 색인이다. source에 존재하는 기능을 현재 계정·팀·앱에서 사용할 수 있다고 검증한 목록은 아니다. 링크된 외부 웹 페이지·동영상·API 문서, 보조 파일 151개, main scenario 본문 및 다른 하위 계열을 읽었다고 확대하지 않는다. 실제 앱·자료에 필요한 내용을 읽고 현행 계약/환경과 대조한 뒤 승인 범위에서 작업한다.

79개 원문의 sha256·바이트·행수·읽은 구간과 보조 파일의 NOT_READ 목록은 [검증 기록](../reports/ExternalLearning/20261101_SCENARIO_SERVICE_SKILLS_STUDY.json)에 있다. 본문 링크 정의는 아래 고정 버전으로 연결된다.

[scenario-3d]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-3d/SKILL.md
[scenario-3d-worlds]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-3d-worlds/SKILL.md
[scenario-ace-step]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-ace-step/SKILL.md
[scenario-ad-variants]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-ad-variants/SKILL.md
[scenario-admin-analytics]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-admin-analytics/SKILL.md
[scenario-asset-analysis]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-asset-analysis/SKILL.md
[scenario-audio]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-audio/SKILL.md
[scenario-blender]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-blender/SKILL.md
[scenario-blender-2d-animation]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-blender-2d-animation/SKILL.md
[scenario-brand-kit]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-brand-kit/SKILL.md
[scenario-caption-studio]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-caption-studio/SKILL.md
[scenario-chatgpt-pet-create]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-chatgpt-pet-create/SKILL.md
[scenario-chatgpt-pet-update]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-chatgpt-pet-update/SKILL.md
[scenario-consistency]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-consistency/SKILL.md
[scenario-elevenlabs]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-elevenlabs/SKILL.md
[scenario-fan-cam]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-fan-cam/SKILL.md
[scenario-formats]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-formats/SKILL.md
[scenario-game-assets]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-game-assets/SKILL.md
[scenario-gemini-image]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-gemini-image/SKILL.md
[scenario-gemini-omni]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-gemini-omni/SKILL.md
[scenario-gpt-image]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-gpt-image/SKILL.md
[scenario-grok-imagine-image]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-grok-imagine-image/SKILL.md
[scenario-grok-imagine-video]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-grok-imagine-video/SKILL.md
[scenario-identity-library]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-identity-library/SKILL.md
[scenario-ideogram]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-ideogram/SKILL.md
[scenario-image]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-image/SKILL.md
[scenario-image-editing]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-image-editing/SKILL.md
[scenario-inspiration]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-inspiration/SKILL.md
[scenario-kinetic-music-video]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-kinetic-music-video/SKILL.md
[scenario-kling]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-kling/SKILL.md
[scenario-luma-image]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-luma-image/SKILL.md
[scenario-luma-video]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-luma-video/SKILL.md
[scenario-mai-image]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-mai-image/SKILL.md
[scenario-meshy]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-meshy/SKILL.md
[scenario-minimax-music]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-minimax-music/SKILL.md
[scenario-minimax-video]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-minimax-video/SKILL.md
[scenario-model-comparison]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-model-comparison/SKILL.md
[scenario-model-training]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-model-training/SKILL.md
[scenario-moderation]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-moderation/SKILL.md
[scenario-motion-loops]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-motion-loops/SKILL.md
[scenario-multi-reference]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-multi-reference/SKILL.md
[scenario-orbit-views]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-orbit-views/SKILL.md
[scenario-patina-retexture]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-patina-retexture/SKILL.md
[scenario-product-shots]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-product-shots/SKILL.md
[scenario-quality-gate]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-quality-gate/SKILL.md
[scenario-reel-recast]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-reel-recast/SKILL.md
[scenario-refine-loop]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-refine-loop/SKILL.md
[scenario-report]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-report/SKILL.md
[scenario-reve]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-reve/SKILL.md
[scenario-rodin]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-rodin/SKILL.md
[scenario-runway]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-runway/SKILL.md
[scenario-seedance]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-seedance/SKILL.md
[scenario-seedance-drafts]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-seedance-drafts/SKILL.md
[scenario-seedance-music-video]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-seedance-music-video/SKILL.md
[scenario-seedance-storyboard]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-seedance-storyboard/SKILL.md
[scenario-seedream]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-seedream/SKILL.md
[scenario-side-view-game-kit]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-side-view-game-kit/SKILL.md
[scenario-skyboxes]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-skyboxes/SKILL.md
[scenario-sonilo]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-sonilo/SKILL.md
[scenario-sparc3d]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-sparc3d/SKILL.md
[scenario-sprite-animation]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-sprite-animation/SKILL.md
[scenario-storyboards]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-storyboards/SKILL.md
[scenario-team-admin]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-team-admin/SKILL.md
[scenario-text-overlay]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-text-overlay/SKILL.md
[scenario-textures]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-textures/SKILL.md
[scenario-thumbnails]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-thumbnails/SKILL.md
[scenario-ugc]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-ugc/SKILL.md
[scenario-veo]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-veo/SKILL.md
[scenario-video]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-video/SKILL.md
[scenario-video-ads]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-video-ads/SKILL.md
[scenario-video-assembly]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-video-assembly/SKILL.md
[scenario-video-color-grade]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-video-color-grade/SKILL.md
[scenario-video-editing]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-video-editing/SKILL.md
[scenario-video-to-motion]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-video-to-motion/SKILL.md
[scenario-vidu]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-vidu/SKILL.md
[scenario-walkable-room]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-walkable-room/SKILL.md
[scenario-wan]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-wan/SKILL.md
[scenario-workflow-authoring]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-workflow-authoring/SKILL.md
[scenario-workflows]: https://github.com/scenario-labs/skills/blob/7f4b801c7248d51b093ec365aceb114bd06139e6/skills/scenario-workflows/SKILL.md
