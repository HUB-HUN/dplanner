# FilmCraft × agent-desktop 원프롬프트: 설치부터 편집 자동화까지 (클로드 코드용)

이 파일은 클로드 코드가 읽고 그대로 따라 하는 순서입니다. 사람은 아래처럼 한 번만 붙여 넣으면 됩니다.

```
https://hub-hun.github.io/dplanner/skills/filmcraft-agent-desktop/oneprompt.md
이 문서를 요약하지 말고 원문 그대로 읽은 뒤,
순서대로 FilmCraft 설치부터 편집 자동화까지 진행해 줘.
영상 폴더: (영상 파일이 든 폴더 경로)
자막: (첫 줄) / (둘째 줄) / (셋째 줄)
```

## 클로드에게

- 1 → 2 → 3 → 4 → 5를 순서대로 진행해 줘. 이미 설치된 것은 건너뛰고 「이미 있음」이라고 알려 줘.
- 내려받는 파일은 공식 GitHub 릴리스에서만 받고, SHA-256이 맞지 않으면 멈추고 알려 줘.
- 관리자 권한이 필요한 방식은 쓰지 마. FilmCraft 윈도우 설치 파일은 사용자별 설치라 관리자 권한 없이 설치돼.
- 1~4(설치)에서는 진짜 마우스를 움직이는 `--headed`를 쓰지 마. 5(편집)에서는 4번 끝의 안내를 한 뒤에만 `--headed`를 써.
- 프로그램의 MCP 서버나 명령줄 도구로 편집하지 마. 편집은 agent-desktop으로 FilmCraft 화면을 조작해서 해. 명령줄 도구(`filmcraft-cli`)는 마지막 결과 확인에만 써.
- 사용자가 「영상 폴더」나 「자막」을 적지 않았으면 5번을 시작하기 전에 물어봐.
- 다 끝나면 무엇을 설치했고, 무엇을 편집했고, 결과 파일이 어디에 있는지 한 번에 정리해 줘.

## 1. agent-desktop (버셀 랩스, Apache-2.0)

1) `agent-desktop --version`이 되면 이 단계는 건너뛰어. 명령을 찾지 못해도 `%LOCALAPPDATA%\Programs\agent-desktop\agent-desktop.exe --version`(윈도우)이 되면 이미 설치된 것이니 건너뛰어(PATH에 넣기 전에 열린 터미널에서는 명령 이름만으로 안 될 수 있어. 그때는 이후에도 전체 경로로 실행해).
2) Node.js가 있으면 `npm install -g agent-desktop`으로 설치해. Node.js가 없으면 https://github.com/vercel-labs/agent-desktop/releases/latest 에서 내 OS에 맞는 압축 파일과 checksums.txt를 받아 SHA-256을 확인하고, 압축을 풀어 사용자 폴더(윈도우는 `%LOCALAPPDATA%\Programs\agent-desktop`)에 두고 사용자 PATH에 추가해.
3) `~/.claude/skills/agent-desktop/SKILL.md`가 없으면 `agent-desktop skills get desktop` 결과의 `data.content`를 요약하지 말고 그대로 그 파일로 저장하고, 파일 맨 끝에 「agent-desktop 실행 파일 위치: (전체 경로)」 한 줄을 붙여.
4) `agent-desktop status`로 확인해.

## 2. FilmCraft (무료 오픈소스 영상 편집기, MIT 또는 Apache-2.0)

1) 이미 설치돼 있으면 건너뛰어(윈도우 기본 위치: `%LOCALAPPDATA%\Programs\ArtCraft\FilmCraft\filmcraft.exe`).
2) https://github.com/storytold/filmcraft/releases/latest 에서 내 OS에 맞는 설치 파일(윈도우는 `filmcraft-<버전>-windows-x64.msi`)과 `SHA256SUMS.txt`를 받아 SHA-256을 확인해. 윈도우라면 설치 파일의 코드 서명(Authenticode)이 유효한지도 확인해.
3) 설치 파일을 실행하고, 설치 창이 뜨면 agent-desktop으로 창의 단추를 차례로 눌러 설치를 마쳐(윈도우 MSI: 「Only for me」(사용자별 설치) → Next → 환영 화면 Next → 설치 폴더 Next → Install → Finish). 「Only for me」 라디오 단추는 헤드리스 클릭이 시간 초과로 끝날 수 있는데, 이미 선택돼 있으면 그대로 넘어가면 돼. 설치 창을 찾지 못하면 윈도우에서는 `msiexec /i <설치 파일 전체 경로> /passive`로 설치해도 돼.
4) 설치된 실행 파일 위치를 확인해. 같은 폴더에 `filmcraft-cli`도 있어.

## 3. FilmCraft 조작 스킬

`~/.claude/skills/filmcraft-agent-desktop/SKILL.md`가 없으면 아래 주소의 파일을 요약하지 말고 원본 그대로 내려받아 그 위치에 저장해.

https://hub-hun.github.io/dplanner/skills/filmcraft-agent-desktop/SKILL.md

## 4. 확인과 안내

- `agent-desktop status` 결과, 두 스킬 파일(`~/.claude/skills/agent-desktop/SKILL.md`, `~/.claude/skills/filmcraft-agent-desktop/SKILL.md`)이 있는지 확인해.
- 사용자에게 이렇게 알리고 5번으로 넘어가: 「설치가 끝났어요. 지금부터 편집이 끝날 때까지 마우스와 키보드를 쓰지 말아 주세요. 클로드가 실제 마우스를 움직이는 단계가 있어요.」
- 5번을 시작하기 전에 사용자가 손을 뗐는지 확인해. 윈도우라면 아래 PowerShell로 마지막 마우스 · 키보드 입력 뒤 30초가 지날 때까지 기다려(10분이 지나도 계속 입력이 있으면 멈추고 사용자에게 알려).

```powershell
Add-Type 'using System;using System.Runtime.InteropServices;public static class Idle{[StructLayout(LayoutKind.Sequential)]public struct L{public uint s;public uint t;}[DllImport("user32.dll")]static extern bool GetLastInputInfo(ref L l);public static uint Ms(){var l=new L();l.s=8;GetLastInputInfo(ref l);return (uint)Environment.TickCount-l.t;}}'
$t0 = Get-Date; while ([Idle]::Ms() -lt 30000) { if (((Get-Date) - $t0).TotalMinutes -gt 10) { 'busy'; break }; Start-Sleep -Seconds 1 }; 'idle'
```

## 5. 편집 자동화 (사용자가 준 영상 폴더와 자막으로)

먼저 `~/.claude/skills/filmcraft-agent-desktop/SKILL.md`를 끝까지 읽어. 아래 순서의 자세한 방법(메뉴 이름, 진짜 마우스가 필요한 동작, 자막 칸 다루기, 내보내기 확인)은 그 파일에 있어.

### 5-1. 준비

1) 세션을 열어 화면에 AI 커서가 보이게 해: `agent-desktop session start --name filmcraft --cursor`. 결과의 `data.session_id`를 이후 모든 명령에 `--session <id>`로 붙여.
2) FilmCraft를 실행하고 `list-windows`로 창을 찾아. 새 프로젝트로 시작해(시작 화면이 나오면 새 프로젝트, 이미 열린 프로젝트가 있으면 `파일`에서 새 프로젝트).
3) 창을 정해진 자리와 크기에 둬: `move-window --x=-7 --y 0`, `resize-window --width 1277 --height 1047`. 창을 최소화하지 마.
4) `창` > `작업 영역` > `      편집 Alt+Shift+1`(이름 앞에 공백이 있어).
5) 영상 폴더의 파일을 이름순으로 확인해: 영상(.mp4 · .mov)은 순서대로 쓰고, 소리 파일(.wav · .mp3)이 있으면 효과음으로 써.

### 5-2. 컷편집: 영상마다 1초씩 이어 붙이기

1) 탭 `미디어 브라우저` → textfield `Path`에 영상 폴더를 `set-value` → `press return`.
2) `screenshot`을 찍어(이미지를 직접 봐) 미디어 브라우저 목록에서 파일 줄의 화면 좌표와, 타임라인 빈 자리(「미디어를 여기에 놓아 시퀀스를 만드세요」)의 좌표를 확인해.
3) 첫 영상을 빈 타임라인으로 `--headed drag --from-xy <파일> --to-xy <타임라인> --duration 650 --drop-delay 350`. 영상 크기에 맞는 시퀀스가 생겨(세로 영상이면 세로 시퀀스).
4) 다시 `screenshot`을 찍어 타임라인 눈금자에서 0초 자리와 1초 눈금(또는 두 눈금)의 x 좌표로 1초당 픽셀을 재.
5) 첫 영상 끝을 자르기: 눈금자에서 1초 자리를 `--headed mouse-click --xy <x,y>`로 눌러 재생 헤드를 옮기고 `press w`(Ripple Trim Next Edit to Playhead). 헤드리스 `press shift+right`는 Shift가 빠지니 쓰지 마.
6) 다음 영상을 재생 헤드 자리(지금 시퀀스 끝)에 `--headed drag`로 놓고, 눈금자에서 그다음 1초 자리를 눌러 `press w`. 영상 개수만큼 반복해.
7) `시퀀스` > `빈 구간 제거`로 한두 프레임 벌어진 칸을 메꿔.
8) `screenshot`으로 타임라인에 클립이 1초씩 차례로 붙었는지 확인해. 어긋났으면 `편집` > 실행 취소(Ctrl+Z)로 되돌려 그 단계부터 다시 해.

### 5-3. 효과음

- 소리 파일이 있으면, 컷이 바뀌는 시각(1초, 2초, …)마다 그 파일을 오디오 트랙(비디오 트랙 아래 줄)에 `--headed drag`로 놓아. 놓은 x 좌표가 소리의 시작 시각이야. 소리 파일이 없으면 이 단계는 건너뛰어.

### 5-4. 자막

1) SKILL.md 「자막」 순서대로 사용자가 준 자막을 한 줄씩 넣어. 줄마다 시작 · 끝 시각은 시퀀스 길이를 줄 수로 나눠 정해(예: 4초 · 4줄이면 0~1초, 1~2초, 2~3초, 3~4초).
2) 자막 모양: 글자 크기 incrementor `px`를 64 안팎으로, checkbox `상자`는 꺼.

### 5-5. 내보내기와 확인

1) `파일` > `내보내기` > `미디어…`. 파일 이름은 `원프롬프트-결과`, 폴더는 사용자가 준 영상 폴더.
2) `자막` > `내보내기 옵션` 목록에서 `자막을 비디오에 번인`을 진짜 마우스로 골라(SKILL.md 「진짜 마우스가 필요한 것」). 트리에서 값이 바뀌었는지 확인해.
3) 「내보내기」 단추를 진짜 마우스로 눌러 끝날 때까지 기다려.
4) SKILL.md 「내보내기」 5번의 `filmcraft-cli` 명령으로 1초 안쪽 장면을 두세 장 뽑아, 자막이 영상에 들어갔는지 직접 봐.
5) 끝나면 `agent-desktop session end --session <id>`로 세션을 닫고, 사용자에게 「이제 마우스를 써도 돼요」라고 알려.

## 6. (요청하면) 정갈한 편집: 점프 컷 · 장면 전환 · 배경음 · 마스터링 · 제목 그래픽 · 커서 여러 개

사용자가 「정갈하게」 · 「고급 편집」처럼 부탁하면 5-2 다음부터 아래를 더해. 메뉴 이름은 FilmCraft 0.18.0 한국어 화면 기준이야.

1) 커서 여러 개: 세션을 `agent-desktop session start --name filmcraft --cursor --multi-agent`로 열고, 헤드리스 동작마다 `--agent-id c1` · `c2` …를 돌려 가며 붙여. 동작마다 다른 색 커서가 움직여. 다른 커서로 패널 탭을 눌러 확인할 때는 「소스」 탭(소스 모니터)을 누르지 마. 소스 모니터가 앞에 오면 `시작 표시` · `끝 표시`가 타임라인 대신 소스 모니터에 걸려서, `구간 삭제`가 클립 끝까지 지워.
2) 전환 길이: `편집` > `설정` > `타임라인…`의 「비디오 전환 기본 길이」(30프레임)를 10프레임으로 줄여. 이름 없는 숫자 칸이라 진짜 마우스로 칸을 누르고 `ctrl+a` → 숫자 → `tab`(`--headed press`), 그다음 `확인`.
3) 점프 컷: 눈금자를 진짜 마우스로 눌러 재생 헤드를 옮긴 뒤 `마커` > `시작 표시 I`, 다시 옮긴 뒤 `마커` > `끝 표시 O`, 그리고 `시퀀스` > `구간 삭제 (간격 닫기) '`. 클립마다 0.5초쯤 한두 곳을 들어내면 빠른 컷이 돼. 다 하면 `마커` > `시작/끝 지우기`.
4) 장면 전환: 먼저 `편집` > `모두 선택 해제`(고른 클립이 있으면 전환이 그 클립 가장자리에 걸려). 그다음 편집점마다 눈금자를 눌러 재생 헤드를 편집점에 두고 `시퀀스` > `비디오 전환 적용 Ctrl+D`.
5) 배경음 · 마스터링: 배경음 파일을 오디오 2 트랙에 놓고, 그 클립을 진짜 마우스로 눌러 고른 뒤 `클립` > `오디오 옵션` > `오디오 게인… G`를 열어. 처음에는 「게인 조정:」이 골라져 있어. 「게인 설정:」 단추는 헤드리스로 안 눌리고 dB 칸은 이름이 같은 칸이 넷이라, `snapshot --include-bounds`로 위치를 읽어 둘 다 진짜 마우스로 눌러. 칸에서 `--headed press ctrl+a` → `0`을 넣고(「-」 키 이름이 없어), `down`을 160번 누르면 -16.0 dB야(한 번에 0.1 dB) → `tab` → `확인`. 창을 다시 열면 「피크 진폭」이 그만큼 내려가 있어. 마지막에 `시퀀스` > `믹스 트랙 정규화…`도 같은 식으로 칸을 누르고 `0` → `down` 한 번(이 칸은 한 번에 1 dB)으로 -1 dB → `확인`. 배경음 · 나레이션이 영상보다 길면 끝에 검은 화면이 붙으니 소리 파일 길이를 영상 길이 안으로 맞춰.
6) 제목 그래픽: 재생 헤드를 0초에 두고 `기본 그래픽` 탭 > `찾아보기`에서 템플릿(예: 「제목 – 가운데」)을 진짜 마우스로 고르고 `적용`(템플릿 목록은 이름만 보이는 칸이라 헤드리스로 못 골라). 적용하면 템플릿 속성 칸이 나와: `Title` 칸에 제목을 `set-value`, 세로 영상에서 부제는 글씨가 아주 작으니 `Subtitle` 칸은 비워(`clear`). 템플릿 속성의 「글꼴」(이름 없는 콤보)은 7)처럼 골라. 길이는 그래픽 클립을 진짜 마우스로 고른 뒤 `클립` > `속도/지속 시간… Ctrl+R`의 「길이:」 칸(예: 00:00:02:00) → `확인`. 그 클립을 고른 채 `시퀀스` > `비디오 전환 적용 Ctrl+D`를 하면 앞뒤에 전환이 걸려 제목이 나타나고 사라져.
7) 자막 모양: 텍스트 패널에서 `px`를 40 안팎으로, `상자`를 켜(작은 흰 글씨 + 검정 반투명 상자, 자막 트랙 전체에 걸림). 글꼴 목록(이름 없는 콤보)은 진짜 마우스로 열어. 목록이 길어서 고를 글꼴이 화면 밖에 있으면, `snapshot --include-bounds`로 그 글꼴 항목(role `switch`)의 위치를 읽고, 목록 위에서 진짜 마우스 휠(`--headed mouse-wheel --dy -9`, 한 칸에 40px쯤)을 굴려 보이게 한 뒤 진짜 마우스로 눌러. 헤드리스 `click` · `select`는 「ok」가 나와도 바뀌지 않거나, 같은 이름 콤보가 둘이라 거절돼.
8) 명령 결과(JSON)를 읽을 때: 커서 여러 개로 동시에 돌리면 agent-desktop이 오류 출력에 경고 줄을 쓸 때가 있어. 오류 출력은 떼어 내고 표준 출력만 JSON으로 읽어.

---
디플래너(dplanner@outlook.kr) · 2026-11-09 · FilmCraft 0.18.0 · agent-desktop 1.2.0 · 윈도우 10.

시험 결과(2026-11-09): FilmCraft를 지운 PC에서 새 클로드 코드 대화에 위 원프롬프트(영상 폴더: 캐릭터 영상 4개와 효과음 1개, 자막 4줄)만 넣었습니다. agent-desktop은 이미 설치돼 있어 건너뛰었고, FilmCraft 설치 → 조작 스킬 저장 → 영상 4개를 1초씩 잇는 컷편집 → 효과음 3개 → 자막 4줄(64px, 상자 없음) → 자막을 입힌 1080×1920 · 4초 영상 내보내기 → 장면 확인까지 끝났습니다. 진짜 마우스는 편집 단계에서만 썼습니다(끌어다 놓기 7번, 클릭 14번). 시험에서 막힌 곳(자막 글 확정, 재생 헤드 옮기기, 내보내기 화면의 자막 칸)은 조작 스킬에 반영했습니다.

6절(정갈한 편집)은 2026-11-09 디플래너 PC에서 클로드가 agent-desktop 명령을 이어 붙인 스크립트로 확인한 순서입니다(영상 6개 18컷 · 전환 5곳 · 효과음 17개 · 배경음 게인 -16 dB · 믹스 정규화 -1 dB · 제목 그래픽 · 자막 6줄 페이퍼로지 40px 상자 · 커서 여러 개). 새 대화에 원프롬프트만 넣어 6절까지 시킨 시험은 아직 하지 않았습니다.
