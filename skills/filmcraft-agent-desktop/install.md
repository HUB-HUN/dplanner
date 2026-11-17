# FilmCraft × agent-desktop 한 번에 설치 (클로드 코드용)

이 파일은 클로드 코드가 읽고 그대로 따라 하는 설치 순서입니다.
사람은 이 파일 주소를 클로드 코드에 붙여 넣고 「이 순서대로 설치해 줘」라고만 말하면 됩니다.

## 클로드에게

- 아래 1 → 2 → 3 → 4를 순서대로 진행해 줘. 이미 설치돼 있으면 그 단계는 건너뛰고 「이미 있음」이라고 알려 줘.
- 내려받는 파일은 공식 GitHub 릴리스에서만 받고, SHA-256이 맞지 않으면 멈추고 알려 줘.
- 관리자 권한이 필요한 방식은 쓰지 마. FilmCraft 윈도우 설치 파일은 사용자별 설치라 관리자 권한 없이 설치돼.
- 설치 창의 단추는 agent-desktop 기본 동작(헤드리스 클릭)으로 눌러. 진짜 마우스를 움직이는 `--headed`는 쓰지 마.
- 다 끝나면 무엇을 설치했고 어디에 있는지 한 번에 정리해 줘.

## 1. agent-desktop (버셀 랩스, Apache-2.0)

1) `agent-desktop --version`이 되면 이 단계는 건너뛰어. 명령을 찾지 못해도 `%LOCALAPPDATA%\Programs\agent-desktop\agent-desktop.exe --version`(윈도우)이 되면 이미 설치된 것이니 건너뛰어(PATH에 넣기 전에 열린 터미널에서는 명령 이름만으로 안 될 수 있어).
2) Node.js가 있으면 `npm install -g agent-desktop`으로 설치해. Node.js가 없으면 https://github.com/vercel-labs/agent-desktop/releases/latest 에서 내 OS에 맞는 압축 파일과 checksums.txt를 받아 SHA-256을 확인하고, 압축을 풀어 사용자 폴더(윈도우는 `%LOCALAPPDATA%\Programs\agent-desktop`)에 두고 사용자 PATH에 추가해.
3) `~/.claude/skills/agent-desktop/SKILL.md`가 없으면 `agent-desktop skills get desktop` 결과의 `data.content`를 요약하지 말고 그대로 그 파일로 저장하고, 파일 맨 끝에 「agent-desktop 실행 파일 위치: (전체 경로)」 한 줄을 붙여.
4) `agent-desktop status`로 확인해.

## 2. FilmCraft (무료 오픈소스 영상 편집기, MIT 또는 Apache-2.0)

1) 이미 설치돼 있으면 건너뛰어(윈도우 기본 위치: `%LOCALAPPDATA%\Programs\ArtCraft\FilmCraft\filmcraft.exe`).
2) https://github.com/storytold/filmcraft/releases/latest 에서 내 OS에 맞는 설치 파일(윈도우는 `filmcraft-<버전>-windows-x64.msi`)과 `SHA256SUMS.txt`를 받아 SHA-256을 확인해. 윈도우라면 설치 파일의 코드 서명(Authenticode)이 유효한지도 확인해.
3) 설치 파일을 실행하고, 설치 창이 뜨면 agent-desktop으로 창의 단추를 차례로 눌러 설치를 마쳐(윈도우 MSI: 「Only for me」(사용자별 설치) → Next → 환영 화면 Next → 설치 폴더 Next → Install → Finish). 설치 창을 찾지 못하면 윈도우에서는 `msiexec /i <설치 파일 전체 경로> /passive`로 설치해도 돼.
4) 설치된 실행 파일 위치를 확인해.

## 3. FilmCraft 조작 스킬

`~/.claude/skills/filmcraft-agent-desktop/SKILL.md`가 없으면 아래 주소의 파일을 요약하지 말고 원본 그대로 내려받아 그 위치에 저장해.

https://hub-hun.github.io/dplanner/skills/filmcraft-agent-desktop/SKILL.md

## 4. 확인

- `agent-desktop status` 결과
- FilmCraft를 한 번 실행하고 `agent-desktop list-windows`에 FilmCraft 창이 보이는지 확인한 뒤 창을 닫아.
- 두 스킬 파일(`~/.claude/skills/agent-desktop/SKILL.md`, `~/.claude/skills/filmcraft-agent-desktop/SKILL.md`)이 있는지 확인해.

---
디플래너(dplanner@outlook.kr) · 2026-11-09 · FilmCraft 0.18.0 · agent-desktop 1.2.0 · 윈도우 10에서 확인. 새 클로드 코드 대화에 이 주소와 「이 순서대로 설치해 줘」만 넣어 시험했고, FilmCraft 설치와 조작 스킬 저장까지 끝까지 진행됐습니다(agent-desktop은 이미 설치돼 있어 건너뜀).
