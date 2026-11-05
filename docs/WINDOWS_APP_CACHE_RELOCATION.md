# Windows 앱 캐시의 별도 드라이브 이전

2026-11-05 · PowerShell 7 공식 문서 3개와 OpenAI 설정 문서를 읽은 범위의 운영 절차다. 문서 학습과 실제 경로 전환·앱 재시작 검증은 구분한다.

## 적용 범위

캐시라는 폴더 이름만으로 삭제·이전 가능하다고 판단하지 않는다. 다운로드된 실행 환경, 플러그인, 브라우저 캐시, 로그인 정보와 대화 데이터는 역할이 다르다. Codex의 `CODEX_HOME` 변경은 상태 저장소 전체에 영향을 주므로 캐시만 옮기는 설정으로 취급하지 않는다. 공식 설정 문서에서 특정 실행 캐시의 독립 이전 옵션을 확인하지 못했다면 지원 여부를 미확인으로 기록한다.

## 보존·준비

1. 사용자 지정 원본과 대상 절대 경로를 확인하고 용량·파일 수·재분석 지점 여부를 기록한다. 원본 밖으로 이어지는 링크가 있으면 무작정 재귀 복사하지 않는다.
2. 잠긴 캐시는 복사 오류를 기록하고 앱 종료 후 처리한다. 읽기 메타데이터 캐시도 전환 전후 동일성과 복구 경로를 확인한다. 실행 환경을 순수 캐시에 포함하지 않는다. 앱 종료는 사용자 지시 범위에서 작업을 먼저 저장한 뒤 진행하며 파일 잠금을 강제로 해제하지 않는다.
3. 새 목적지는 비어 있는 별도 폴더로 만들며 기존 파일을 덮어쓰지 않는다. 파일 크기·상대 경로·SHA256을 대조한다. 변경 중이거나 잠긴 파일은 별도 미검증으로 기록한다. 복사 검증은 앱 사용 검증과 다르다.

## 경로 전환과 복구

`Move-Item -LiteralPath`는 지정한 항목과 하위 내용을 이동한다. 이동 전 원본과 목적지의 정규화된 절대 경로가 승인 범위 안에 있는지 확인한다. 대상이 이미 있으면 병합·강제 덮어쓰기를 하지 않는다.

앱에서 공식 캐시 위치 설정을 제공하면 그 설정을 우선한다. 별도 승인된 파일시스템 연결 방식은 `New-Item -ItemType Junction`으로 구성할 수 있지만 앱의 공식 이전 기능과 구별한다. 기존 경로를 가리키는 연결을 만들기 전에 원본을 별도 보존하고, 연결 실패 시 원래 경로로 복원한다. 이 문서는 실행 중 앱의 무중단 전환을 보장하지 않는다.

경로 전환 뒤 연결 대상·파일 수·해시를 다시 확인하고 앱 재시작, 플러그인 로드와 필요한 실제 기능을 시험한다. 업데이트가 경로를 재생성하는지도 나중에 확인한다. 원본 보존본 정리는 검증 후 사용자가 지정한 정확한 폴더만 대상으로 한다. 공간 확보량은 논리 파일 합계와 별도로 실제 드라이브 여유 공간을 측정한다.

## 학습 근거와 제한

- [Microsoft New-Item](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/new-item?view=powershell-7.5): 파일시스템의 Junction 항목과 Force의 기존 연결 덮어쓰기 동작을 확인했다. Force 없이 새 경로에만 연결하는 절차로 적용한다.
- [Microsoft Move-Item](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/move-item?view=powershell-7.5): LiteralPath, 하위 항목 이동, 기존 대상 충돌 동작을 확인했다. 파일 잠금이나 앱 무중단 사용 성공은 이 문서로 입증되지 않는다.
- [Microsoft Get-FileHash](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/get-filehash?view=powershell-7.5): SHA256 기본값과 내용 동일성 확인 용도를 읽었다. 파일 해시는 실행 상태·권한·앱 호환 검증을 대신하지 않는다.
- [OpenAI 고급 설정](https://learn.chatgpt.com/docs/config-file/config-advanced): CODEX_HOME이 설정·이력·로그·캐시 등을 포함하는 상태 저장소임을 확인했다. [앱 설정](https://learn.chatgpt.com/docs/app/settings)을 추가 검토했으나 특정 실행 캐시의 공식 이전 기능은 확인하지 못했다.

이번 문서 작성 시점에는 복사 준비와 경로 전환을 분리한다는 적용 절차만 정리했다. 실제 앱 종료·경로 전환·재시작 성공을 미리 완료로 기록하지 않는다.


## MSIX의 논리 AppData 경로와 실제 저장 위치

[Microsoft MSIX 실행 동작](https://learn.microsoft.com/en-us/windows/msix/desktop/desktop-to-uwp-behind-the-scenes)의 AppData 절과 [문제 해결 문서](https://learn.microsoft.com/en-us/windows/msix/msix-troubleshooting-guide)를 추가 확인했다. 패키지에 따라 새 AppData 파일이 앱별 저장소에 기록되고 논리 경로에 병합되어 보일 수 있다. 따라서 논리 경로에서 만든 연결과 실제 패키지 저장소 경로를 구분한다. 앱 설치 파일·패키지 매니페스트·보안 설정을 고쳐 해결하지 않는다.

제한 적용에서 순수 도구 메타데이터 캐시는 별도 드라이브 연결 후 읽기 해시 검증을 통과했다. 일부 웹 캐시는 사용 중 파일 잠금으로 복사가 실패했다. 잠기지 않은 웹 캐시 두 곳은 연결 생성 뒤 논리 경로 읽기가 실패하여, 실제 패키지 저장 위치에서 생성한 연결을 보존 이름으로 변경하고 보존본을 복사해 원래 폴더를 복구했다. 복구 해시와 논리 경로 읽기를 확인했다. 파일 잠금과 경로 해석 오류를 구분하며 앱 종료만으로 두 문제가 함께 해결된다고 단정하지 않는다. 앱 재시작 후 캐시 경로 유지 성공은 별도 검증 대상이다.
