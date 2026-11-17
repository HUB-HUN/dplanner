---
name: dplanner-stageshow
description: 디플래너가 정리한 Stageshow 스킬셋이에요. 우리 서비스의 로그인 · 회원가입 · 결제 · 대시보드 같은 화면을 진짜 제품처럼 보이는 시연 화면(정지 그림, 커서가 입력하고 누르는 애니메이션)으로 만들 때 써요. Stageshow(benjitaylor/skills, MIT)를 고정 커밋으로 받아 미리 보기까지 켜는 세팅, 화면을 부탁하는 문장 틀, 한글 글꼴을 넣는 방법, 정지 그림과 리허설 점검을 받는 방법을 담았어요. "Stageshow 세팅해 줘", "Stageshow로 우리 서비스 로그인 화면 만들어 줘" 같은 요청에 쓰고, 화면을 만들 때는 Stageshow 스킬(stageshow)과 함께 읽어요. 처음 쓰면 「세팅」 절의 순서대로 한 번 세팅해요. 클로드 코드와 GPT 앱(ChatGPT 데스크톱 앱 · 코덱스)에서 써요.
---

# 디플래너 Stageshow 스킬셋

Stageshow는 벤지 테일러(Benji Taylor)가 MIT 라이선스로 공개한 스킬이에요. 진짜 제품처럼 보이는 제품 화면을 React로 그려서 정지 그림이나 짧은 애니메이션으로 만들고, 애니메이션에서는 커서가 들어와 입력하고 눌러요. 이 스킬셋에는 Stageshow 설치부터 우리 서비스 화면을 부탁하는 문장, 한글 글꼴, 결과 점검까지 차례로 정리했어요.

벤지 테일러는 Stageshow를 클로드 코드 · 코덱스 · 제미나이 같은 코딩 에이전트에서 쓸 수 있다고 소개해요(benji.org/stageshow). 이 스킬셋도 클로드 코드와 GPT 앱에서 쓸 수 있게, 「세팅」 0단계에서 앱에 맞는 스킬 폴더를 골라요.

Stageshow 화면은 시연하려고 그린 화면이에요. 커서가 누르는 모습도 그림이라서 실제 서비스를 조작하거나 자동화하지 않아요(Stageshow README).

| 절 | 하는 일 |
|---|---|
| 지킬 것 | 원본 · 라이선스 · 로고 · 숫자 규칙 |
| 세팅 | 스킬 폴더 정하기 → 원본 받기 → Node 확인 → `npm install` → 미리 보기 주소 알리기 |
| 부탁하기 | 문장 틀과 예시, 부탁을 받은 AI가 따르는 순서 |
| 한글 글꼴 | 글꼴 파일을 장면 폴더에 넣는 방법(예: 페이퍼로지) |
| 결과 받기 | 정지 그림 · 리허설 점검 명령, 영상이 필요할 때 할 일 |
| 막힐 때 | 자주 나는 오류와 할 일 |

## 지킬 것 (먼저 읽음)

- **Stageshow 원본 파일은 고치지 않아요.** 스킬 폴더의 `stageshow/`(「세팅」 0 · 2단계)에 받은 파일(SKILL.md · README.md · LICENSE · NOTICE.md · package.json · package-lock.json과 `kit/` · `references/` · `scripts/` · `playground/` · `teaching/` · `assets/`, `examples/`의 기존 예시)은 그대로 둬요. 4단계 `npm install`이 만드는 `node_modules/`만 예외예요. 우리 화면은 `examples/<새 이름>/` 새 폴더에만 만들어요. 원본을 고쳐야만 해결되는 문제가 보이면 고치지 말고 사용자에게 알려요.
- **원작자 표시와 라이선스를 지켜요.** Stageshow는 MIT 라이선스이고 저작권 표시는 `Copyright (c) 2026 Benji Taylor`예요. `LICENSE`와 `NOTICE.md`를 지우지 않아요. `kit/`나 예시 코드를 우리 프로젝트로 복사할 때는 `LICENSE`도 함께 넣어요. MIT 라이선스는 저작권 표시와 허가 문구를 사본에 함께 넣는 조건으로 사용을 허락해요.
- **다른 회사의 로고와 상표를 화면에 넣지 않아요.** 카드사 · 결제사 · 은행 · 앱의 로고도 마찬가지예요. Stageshow에 든 로고(`kit/brands/`, `BrandMark`)와 앱 아이콘(`assets/app-icons.ts`), 실제 제품을 본떠 그린 예시(Figma · Slack 등)에는 그 회사들의 이름과 마크가 들어 있어요. Stageshow 라이선스는 상표권을 주지 않고, 앱 아이콘은 MIT 라이선스에도 들어가지 않아요(NOTICE.md). 우리 서비스 로고는 사용자가 준 파일만 쓰고, 없으면 지어내지 말고 서비스 이름을 글자로만 써요.
- **상품 · 가격 · 숫자 · 기능을 지어 넣지 않아요.** 화면에 넣는 상품 이름, 가격, 매출이나 성과 숫자는 사용자가 알려 준 값만 써요. 모르면 사용자에게 묻거나, 이야기와 상관없는 자리는 Stageshow 방식대로 빈 막대(`Bar`)로 둬요. 우리 서비스에 없는 기능은 그리지 않고, 실제 카드 번호 · 고객 이름 · 연락처 같은 개인 정보도 넣지 않아요.
- **프로그램은 대신 설치하지 않아요.** Node(「세팅」 3단계)나 구글 크롬(「결과 받기」의 촬영)이 없으면 설치 방법만 알려 주고 멈춰요.

## 세팅 (처음 한 번)

사용자가 이 파일을 주며 「설치해 줘」 · 「세팅해 줘」라고 하면 아래를 차례로 해요. `~`는 사용자 홈 폴더(윈도우는 `C:\Users\<이름>`)예요. 윈도우에서는 PowerShell 명령을, 맥 · 리눅스에서는 터미널 명령을 그대로 실행해요. 단계가 끝날 때마다 한 줄로 알려 줘요.

세팅을 이어서 해 달라는 말(예: Node를 설치한 뒤 「Stageshow 세팅 이어서 해 줘」)을 들으면, 0단계로 스킬 폴더를 다시 정하고 1 · 2단계는 아래 「이미 있을 때」 규칙대로 확인만 한 뒤 3단계부터 이어서 해요.

0. **스킬 폴더 정하기**: 지금 실행 중인 앱에 따라 스킬 폴더를 골라요. 아래 명령의 `$SK`가 이 폴더예요. AI 앱은 명령을 실행할 때마다 셸을 새로 열 수 있어서 앞에서 정한 값이 남지 않아요. 그래서 아래 명령 블록마다 첫 줄에서 `$SK`를 다시 정해요(GPT 앱이면 그 줄을 `.agents` 폴더로 바꿔요).

   - 클로드 코드(클로드 앱의 Code 탭): `~/.claude/skills`
   - GPT 앱(ChatGPT 데스크톱 앱 · 코덱스): `~/.agents/skills`(OpenAI 공식 문서 https://learn.chatgpt.com/docs/build-skills 의 사용자 스킬 폴더)

   ```powershell
   $SK = "$env:USERPROFILE\.claude\skills"    # GPT 앱이면 "$env:USERPROFILE\.agents\skills"
   ```

   ```sh
   SK="$HOME/.claude/skills"    # GPT 앱이면 "$HOME/.agents/skills"
   ```

1. **이 스킬 설치**: 이 파일을 요약하거나 고치지 말고 원본 그대로 `$SK/dplanner-stageshow/SKILL.md`로 복사해요(클로드 코드는 `~/.claude/skills/dplanner-stageshow/SKILL.md`, GPT 앱은 `~/.agents/skills/dplanner-stageshow/SKILL.md`). `<받은 파일>`은 사용자가 준 SKILL.md의 경로예요. 대화에 첨부한 파일이면 앱이 알려 주는 경로를 쓰고, 경로를 알 수 없으면 다운로드 폴더에서 이름이 SKILL로 시작하는 .md 파일을 찾아요. 그런 파일이 여러 개면 어느 것인지 사용자에게 물어요.

   ```powershell
   $SK = "$env:USERPROFILE\.claude\skills"    # GPT 앱이면 "$env:USERPROFILE\.agents\skills"
   $src = '<받은 파일>'
   $dst = Join-Path $SK 'dplanner-stageshow\SKILL.md'
   if (Test-Path $dst) {
     if ((Get-FileHash $src).Hash -eq (Get-FileHash $dst).Hash) { '이미 같은 파일이 있음' } else { '다른 판이 있음' }
   } else {
     New-Item -ItemType Directory -Force (Split-Path $dst) | Out-Null
     Copy-Item $src $dst; '복사함'
   }
   ```

   ```sh
   SK="$HOME/.claude/skills"    # GPT 앱이면 "$HOME/.agents/skills"
   SRC='<받은 파일>'
   DST="$SK/dplanner-stageshow/SKILL.md"
   if [ -e "$DST" ]; then cmp -s "$SRC" "$DST" && echo "이미 같은 파일이 있음" || echo "다른 판이 있음"
   else mkdir -p "$(dirname "$DST")" && cp "$SRC" "$DST" && echo "복사함"; fi
   ```

   「다른 판이 있음」이 나오면 덮어쓰지 말고, 새 판으로 바꿀지 사용자에게 물어요. 세팅을 이어서 할 때 대화에 받은 파일이 없으면, 이미 설치된 `$SK/dplanner-stageshow/SKILL.md`를 그대로 쓰고 넘어가요.

2. **Stageshow 원본 받기**: 디플래너가 확인한 판(커밋 `299140fafd08df55a9c234e610c3f64af3f45531`)을 받아 `$SK/stageshow/`에 둬요. 받은 파일은 이 단계에서 실행하지 않아요.

   윈도우(PowerShell):

   ```powershell
   $SK = "$env:USERPROFILE\.claude\skills"    # GPT 앱이면 "$env:USERPROFILE\.agents\skills"
   $sha  = '299140fafd08df55a9c234e610c3f64af3f45531'
   $dest = Join-Path $SK 'stageshow'
   if (Test-Path $dest) { "이미 있음: $dest" } else {
     $tmp = Join-Path $env:TEMP ('stageshow-' + [guid]::NewGuid().ToString('N'))
     New-Item -ItemType Directory -Force $tmp | Out-Null
     curl.exe -fsSL -o "$tmp\skills.tar.gz" "https://codeload.github.com/benjitaylor/skills/tar.gz/$sha"
     if ($LASTEXITCODE -eq 0) { tar.exe -xzf "$tmp\skills.tar.gz" -C $tmp --strip-components=1 }
     if ($LASTEXITCODE -eq 0 -and (Test-Path "$tmp\stageshow")) {
       New-Item -ItemType Directory -Force $SK | Out-Null
       try { Copy-Item -Recurse "$tmp\stageshow" $dest -ErrorAction Stop; "받음: $dest" }
       catch { Remove-Item -Recurse -Force $dest -ErrorAction SilentlyContinue; "받기 실패: $($_.Exception.Message)" }
     } else { '받기 실패' }
     Remove-Item -Recurse -Force $tmp
   }
   'SKILL.md', 'LICENSE', 'NOTICE.md' | ForEach-Object { "$_ $(Test-Path (Join-Path $dest $_))" }
   ```

   맥 · 리눅스(터미널):

   ```sh
   SK="$HOME/.claude/skills"    # GPT 앱이면 "$HOME/.agents/skills"
   SHA=299140fafd08df55a9c234e610c3f64af3f45531
   DEST="$SK/stageshow"
   if [ -e "$DEST" ]; then echo "이미 있음: $DEST"; else
     TMP=$(mktemp -d)
     if curl -fsSL -o "$TMP/skills.tar.gz" "https://codeload.github.com/benjitaylor/skills/tar.gz/$SHA" \
        && tar -xzf "$TMP/skills.tar.gz" -C "$TMP" --strip-components=1 && [ -d "$TMP/stageshow" ]; then
       mkdir -p "$SK"
       if cp -R "$TMP/stageshow" "$DEST"; then echo "받음: $DEST"; else rm -rf "$DEST"; echo "받기 실패"; fi
     else echo "받기 실패"; fi
     rm -rf "$TMP"
   fi
   for f in SKILL.md LICENSE NOTICE.md; do [ -e "$DEST/$f" ] && echo "$f True" || echo "$f False"; done
   ```

   마지막 세 줄에서 `SKILL.md` · `LICENSE` · `NOTICE.md`가 모두 `True`여야 해요. `True`도 `False`도 아닌 빈 값이 나오면 `$SK`가 비어 있다는 뜻이니, 블록 첫 줄을 확인하고 다시 실행해요.

   - 「받음」 다음에 셋 다 `True`: 다음 단계로 가요.
   - 「이미 있음」 다음에 셋 다 `True`(이미 있을 때): 전에 받아 둔 원본이에요. 덮어쓰지 않고 그대로 쓰고 다음 단계로 가요. 세팅을 이어서 할 때가 이 경우예요. 디플래너가 확인한 판인지는 알 수 없으니, 기존 폴더를 그대로 쓴다고 사용자에게 한 줄로 알려요.
   - 「받기 실패」가 나오거나 하나라도 `False`: 다음 단계로 가지 말고, 폴더를 지우거나 덮어쓰지도 말고 사용자에게 알려요.

3. **Node 확인**: Stageshow는 Node 20.19 이상이 필요해요(Stageshow README).

   - 윈도우: `if (Get-Command node -ErrorAction SilentlyContinue) { node --version } else { 'Node 없음' }`
   - 맥 · 리눅스: `command -v node >/dev/null 2>&1 && node --version || echo "Node 없음"`

   `v22` 이상이거나 `v20.19` 이상인 `v20`이면 다음 단계로 가요. 그 밖의 경우(`Node 없음`, `v20.19`보다 낮은 버전, `v21`)에는 **Node를 설치하지 말고 여기서 멈춰요.** 미리 보기를 띄우는 Vite 6은 `v21`을 지원 목록에 두지 않아요. 그리고 사용자에게 이렇게 알려요.

   > Node가 없거나 맞는 버전이 아니어서 세팅을 멈췄어요. https://nodejs.org 에서 LTS 버전을 받아 설치해 주세요. 설치한 뒤에는 지금 쓰고 있는 AI 앱을 닫았다가 다시 열고 「Stageshow 세팅 이어서 해 줘」라고 말해 주세요.

4. **npm install**: Stageshow README대로 받은 폴더 안에서 설치해요.

   ```powershell
   $SK = "$env:USERPROFILE\.claude\skills"    # GPT 앱이면 "$env:USERPROFILE\.agents\skills"
   Set-Location (Join-Path $SK 'stageshow'); npm install
   ```

   ```sh
   SK="$HOME/.claude/skills"    # GPT 앱이면 "$HOME/.agents/skills"
   cd "$SK/stageshow" && npm install
   ```

   `--omit=optional`은 붙이지 않아요. 디플래너가 리눅스 서버에서 이 옵션을 붙였더니 Vite에 필요한 부품(rollup의 리눅스용 파일)까지 빠져서 미리 보기가 켜지지 않았어요.

5. **미리 보기 켜기**: 같은 폴더에서 `npm run dev`를 실행해요(Stageshow README). 서버라서 끝나지 않으므로 백그라운드로 켜고, 출력에 나온 주소를 사용자에게 알려 줘요.

   - 윈도우: Vite가 바로 켜져요. Vite가 출력한 `Local:` 주소를 알려 줘요. 보통 `http://127.0.0.1:5173`이에요.
   - 맥 · 리눅스: Portless를 거쳐 `http://stageshow.localhost:1355`로 열려요(README).
   - 미리 보기에는 골드 예시, 비주얼 스타일 아홉 가지, 잘못된 예와 고친 예를 짝지은 교육용 예시가 있어요. 멈춤 · 다시 재생 · 느리게 · 한 프레임씩 넘기기가 되고, `Phone`은 폭을 358px로 바꾸고, `Reduced motion`은 장면마다 멈춘 화면을 보여 줘요(README).
   - 장면 하나만 보여 주는 주소는 `<미리 보기 주소>/?capture=<장면 이름>`이에요. 촬영 명령에도 이 주소를 써요.

6. **세팅 끝**: 「세팅이 끝났어요. 미리 보기는 <주소>에서 볼 수 있어요. 이제 'Stageshow로 ○○ 로그인 화면 만들어 줘'처럼 부탁하면 돼요」라고 알리고, 아래 「부탁하기」의 빈칸 틀을 보여 줘요.

## 부탁하기

「Stageshow로 ○○ 화면 만들어 줘」 한 줄로도 시작할 수 있어요. 디플래너도 이 한 줄에 서비스 이름 · 화면 크기 · 글꼴 파일 위치를 붙여서 로그인 · 회원가입 · 결제 · 대시보드 화면을 만들었어요. 그다음 리허설 점검(아래 「결과 받기」)에 찍힌 줄을 클로드에게 전해 고치게 했어요. 이야기를 적지 않으면 AI가 이야기를 정하니까, 꼭 보여 주고 싶은 장면이 있으면 이야기까지 적어요.

빈칸 틀:

```text
Stageshow로 [서비스 이름]의 [화면 종류] 화면 만들어 줘.
- 이야기: [무엇을 입력하거나 누르면] → [무엇이 바뀌는지]
- 크기: [가로 × 세로] ([쓰는 곳])
- 글꼴: [글꼴 파일이 있는 폴더] (없으면 「기본 글꼴」)
- 참고: [우리 서비스 주소나 코드 폴더 · 로고 파일 · 실제 상품과 가격 · 숫자] (있을 때만)
```

크기는 쓰는 곳에 맞춰 적어요. 아래 값은 Stageshow SKILL.md의 기준이에요. 데모는 가로 약 320보다 작게 만들지 않아요.

| 쓰는 곳 | 크기 |
|---|---|
| 홈페이지 첫 화면, 글 옆 | 약 720 × 340 |
| 홈페이지 첫 화면, 전체 폭 | 가로 900~1100 |
| 기능 소개 카드 | 400 × 300 |
| 휴대폰 화면 폭 | 휴대폰 칸에 들어갈 수 있는 화면이면 AI가 가로 358 판(`compact`)을 따로 만들어요 |

예시(「디플래너」 자리에 우리 서비스 이름을 넣어요):

- **로그인**: 「Stageshow로 디플래너 로그인 화면 만들어 줘. 이메일과 비밀번호를 입력하고 로그인을 누르면, 누른 버튼이 '계정 확인 중'을 거쳐 '로그인 완료'로 바뀌는 이야기야. 크기는 720 × 340이고 홈페이지 첫 화면에서 글 옆에 놓을 거야. 글꼴은 내려받기 폴더의 Paperlogy 폴더에 있는 페이퍼로지를 써 줘.」
- **회원가입**: 「Stageshow로 디플래너 회원가입 화면 만들어 줘. 이메일을 덜 쓰면 칸 아래에 무엇이 빠졌는지 오류가 뜨고, 고쳐 쓰면 확인 표시가 붙고, 약관에 동의하면 가입하기 버튼이 켜지는 이야기야. 크기는 560 × 400이야.」
- **결제**: 「Stageshow로 디플래너 결제 화면 만들어 줘. 카드 번호를 넣으면 네 자리씩 띄어지고, 결제하기를 누르면 버튼이 '결제 완료'로 바뀌는 이야기야. 상품은 '[실제 상품 이름]', 금액은 [실제 금액]으로 써 줘. 크기는 가로 1000이고 홈페이지 첫 화면 전체 폭에 쓸 거야.」
- **대시보드**: 「Stageshow로 디플래너 대시보드 화면 만들어 줘. 오늘 할 일 하나에 체크하면 줄이 그어지고, 한 박자 뒤에 이번 주 완료 수가 18에서 19로 바뀌며 오늘 막대가 올라가는 이야기야. 크기는 960 × 540이고 발표 자료 한 장에 넣을 거야.」

### 부탁을 받으면 (AI가 하는 일)

Stageshow 스킬(`$SK/stageshow/SKILL.md`)을 열고 그 「Workflow」 순서를 그대로 따라요. 스킬 도구로 부를 수 없거나 GPT 앱에서 쓸 때는 그 파일을 직접 읽고 따라요. 이 스킬셋은 그 순서를 바꾸지 않아요.

1. **계획**: 코드보다 먼저 화면이 놓일 곳과 크기, 눈이 갈 대상, 동작, 결과, 뺄 것을 적어요(Workflow 1~3).
2. **가까운 골드 예시에서 시작**(Workflow 4): Stageshow SKILL.md의 Gold 표에서 가장 가까운 예시를 골라 정지 그림으로 찍어 보고, 그 폴더를 `examples/<새 이름>/`으로 복사해요. 그다음 `references/craft.md`를 끝까지 읽고, 우리 서비스의 글 · 색 · 아이콘으로 바꿔요. 디플래너가 해 봤을 때는 로그인 · 회원가입 · 결제를 `form-error`에서, 대시보드를 `table-edit`에서 시작했어요.
3. **화면**(Workflow 5): 실제 글자는 이야기에 필요한 곳에만 쓰고(보통 3~7개), 나머지는 빈 막대로 둬요. 버튼 · 입력 칸 · 카드는 직접 그리지 않고 Stageshow 키트 부품을 써요.
4. **움직임**(Workflow 6): 커서 이동 · 입력 · 누름과 바뀌는 값을 `Act`로 짜요.
5. **리허설**(Workflow 7): 멈춘 한 장(`poster`)을 먼저 정하고, `film.mjs --gate`로 넓은 폭과 폰 폭(390)을 찍어요. 끝줄이 `rehearsal passed`가 될 때까지 찍힌 줄을 고쳐요. 통과는 필요조건일 뿐이라서, 그다음 `references/rehearse.md`의 마지막 점검을 하고 장면 옆에 `REHEARSAL.md`(복사한 골드, 바꾼 것, 확인하지 못한 것)를 써요.
6. **보여 주기**: 미리 보기 주소와 정지 그림, 리허설 결과를 사용자에게 보여 줘요.

## 한글 글꼴

Stageshow에는 외부 글꼴이 들어 있지 않고, 미리 보기도 바깥에서 글꼴을 받아 오지 않아요(NOTICE.md). 따로 정하지 않으면 시스템 글꼴(`system-ui`)로 그려요. 화면 글자를 원하는 한글 글꼴로 만들려면 글꼴 파일을 장면 폴더에 넣어요. 디플래너는 네 화면 모두 장면 폴더의 `fonts/`에 페이퍼로지를 넣고 `@font-face`로 썼어요.

1. 장면 폴더에 `fonts/`를 만들고, 쓰는 굵기의 파일과 글꼴 라이선스 파일을 넣어요.

   ```text
   examples/<장면>/fonts/Paperlogy-4Regular.woff2
   examples/<장면>/fonts/Paperlogy-6SemiBold.woff2
   examples/<장면>/fonts/Paperlogy-7Bold.woff2
   examples/<장면>/fonts/OFL license.txt
   ```

2. 장면 CSS에 `@font-face`를 굵기마다 적어요. 글꼴 이름에 장면 이름을 붙이면 다른 장면의 선언과 겹치지 않아요. `font-display: block`은 다른 글꼴로 먼저 그렸다가 바뀌면서 글자가 흔들리는 일을 막아요.

   ```css
   @font-face {
     font-family: 'mylogin Paperlogy';
     src: url('./fonts/Paperlogy-4Regular.woff2') format('woff2');
     font-weight: 400;
     font-style: normal;
     font-display: block;
   }
   /* 600(6SemiBold) · 700(7Bold)도 같은 꼴로 적어요 */
   ```

3. `Stage`에 글꼴 토큰을 줘요. `--ss-font`는 Stageshow가 글자에 쓰는 토큰이에요(`references/looks.md`).

   ```tsx
   <Stage tokens={{ '--ss-font': "'mylogin Paperlogy', system-ui, sans-serif" }} ...>
   ```

4. 정지 그림을 찍어서 한글이 그 글꼴로 나오는지 눈으로 확인해요.

**예: 페이퍼로지(Paperlogy)** (2026-11-15 확인)

- 배포 페이지: https://www.freesentation.blog/paperlogyfont
  - 리디자인과 제작은 이주임, 기획은 김도균이라고 배포 페이지에 적혀 있어요.
- 파일: woff2는 https://github.com/Freesentation/paperlogy 저장소의 `woff2/` 폴더에 있어요(예: `https://raw.githubusercontent.com/Freesentation/paperlogy/main/woff2/Paperlogy-4Regular.woff2`). 같은 저장소에 `OFL license.txt`가 있고, TTF 묶음은 배포 페이지에서 받아요.
- 라이선스: SIL 오픈 폰트 라이선스(OFL) 1.1이에요. 저장소의 `OFL license.txt`와 글꼴 파일 안에 적혀 있어요. 배포 페이지에는 글꼴만 따로 팔거나 라이선스를 바꾸는 일 말고는 상업적 이용 · 수정 · 재배포가 된다고 적혀 있어요. OFL은 글꼴을 함께 배포할 때 사본마다 저작권 표시와 라이선스를 넣으라고 해요. 그래서 장면을 다른 사람에게 주거나 저장소에 올릴 때는 `OFL license.txt`를 같은 폴더에 둬요.
- 글꼴 파일은 사용자가 받아 둔 위치를 쓰거나, 사용자 허락을 받고 AI가 위 주소에서 받아요.

다른 한글 글꼴도 같은 방법으로 넣어요. 그 전에 글꼴 라이선스가 웹 페이지에 넣어 쓰는 것을 허락하는지 확인해요. Stageshow도 라이선스가 없는 글꼴과 이미지는 쓰지 말라고 해요(`references/looks.md`).

## 결과 받기

촬영 도구 `scripts/film.mjs`는 이 컴퓨터에 설치된 구글 크롬으로 찍어요. 크롬이 없으면 사용자에게 설치를 부탁하거나, 크롬 · 크로뮴 실행 파일 경로를 환경 변수 `CHROME_PATH`에 넣어요(`scripts/browser.mjs`). 미리 보기를 켜 둔 채 `$SK/stageshow` 폴더에서 실행해요. 아래 명령은 PowerShell과 맥 · 리눅스 터미널에서 똑같이 써요.

- `<주소>`: 미리 보기 주소(윈도우는 보통 `http://127.0.0.1:5173`, 맥 · 리눅스는 `http://stageshow.localhost:1355`)
- `<장면>`: `examples/` 아래의 장면 폴더 이름

**정지 그림** (PNG 한 장, 2배 해상도)

```sh
# 결과 화면: 동작 줄이기 모드라서 poster(멈춘 결과 화면)를 찍어요
node scripts/film.mjs "<주소>/?capture=<장면>" --select '#example' --reduced --still --out shots/<장면>-poster.png
# 첫 화면: 장면이 열린 직후를 찍어요
node scripts/film.mjs "<주소>/?capture=<장면>" --select '#example' --still --out shots/<장면>-still.png
```

**리허설 점검** (모음판 한 장과 판정)

```sh
node scripts/film.mjs "<주소>/?capture=<장면>" --select '#example' --gate --out shots/<장면>-film.png
node scripts/film.mjs "<주소>/?capture=<장면>" --select '#example' --width 390 --gate --out shots/<장면>-390.png
node scripts/film.mjs "<주소>/?capture=<장면>" --select '#example' --states --gate --out shots/<장면>-states.png
```

- 끝줄이 `rehearsal passed`면 점검을 통과한 거예요. `rehearsal failed: N never-intentional line(s) above`면 그 위에 찍힌 줄을 `references/rehearse.md`의 「Lines that are never intentional」 표에서 찾아 고치고 다시 찍어요.
- `film: inconclusive`가 함께 나오면 촬영 간격이 벌어지는 등의 이유로 일부 움직임을 판정하지 못했다는 뜻이에요. 이유는 그 위의 `incomplete:` 줄에 나와요. 디플래너 서버에서도 나왔어요. 그 부분은 미리 보기에서 직접 재생해서 확인해요.
- 통과해도 모음판 그림을 직접 보고, 미리 보기에서 움직임을 재생해 봐요. Stageshow README는 자동 점검이 움직임을 직접 보는 일을 대신하지 못한다고 해요.
- 결과 파일은 `shots/`에 생겨요. 다른 곳에 두려면 `--out`에 경로를 적어요.

**영상(mp4)**: Stageshow에는 영상 파일을 바로 뽑는 명령이 없어요. 영상이 필요하면 미리 보기에서 장면(`?capture=<장면>` 주소)을 재생하고 화면 녹화 도구로 녹화해요. 디플래너 영상은 따로 만든 녹화 스크립트로 뽑았고, 그 스크립트는 이 스킬셋에 넣지 않았어요.

**코드로 쓰기**: 우리 React 프로젝트에 넣으려면 `kit/`와 장면 폴더를 복사하고 `import { Stage, Window, type Act } from './kit'`처럼 가져와요(README 「Use the kit」). 이때 `LICENSE`도 함께 넣어요.

## 막힐 때

| 상황 | 할 일 |
|---|---|
| `Node 없음`, 또는 맞지 않는 버전 | Node를 설치하지 말고 멈춰요. 「세팅」 3단계의 안내를 사용자에게 보여 줘요 |
| PowerShell에서 `npm`이 「스크립트를 실행할 수 없으므로」 오류로 막힘 | 실행 정책은 바꾸지 말고 `npm.cmd install`, `npm.cmd run dev`처럼 `npm.cmd`로 실행해요 |
| 맥 · 리눅스에서 `npm run dev`가 `Portless is unavailable` 오류를 냄 | README대로 `npm install --include=optional`을 해요. 그래도 안 되면 Vite를 바로 켜요: `node node_modules/vite/bin/vite.js playground --config playground/vite.config.ts --port 5173`. 디플래너가 리눅스 서버에서 쓴 명령이고, 주소는 `http://127.0.0.1:5173`이에요 |
| 미리 보기에 새 장면이 안 보임 | 장면 폴더가 `examples/<장면>/index.tsx` 꼴인지 확인해요. 새 장면은 미리 보기 목록의 `Kit` 묶음 끝에 붙어요 |
| film이 `Couldn't start Chrome`을 냄 | 구글 크롬 설치를 사용자에게 부탁하거나, `CHROME_PATH`에 크롬 · 크로뮴 경로를 넣어요 |
| film이 `This page embeds its scene in an iframe`을 냄 | 일반 미리 보기 주소 대신 `?capture=<장면>` 주소로 찍어요 |
| `rehearsal failed` | 「결과 받기」대로 찍힌 줄을 고치고 다시 찍어요. 원본 파일을 고쳐야만 없어지는 줄이면 고치지 말고 사용자에게 알려요 |
| 한글이 다른 글꼴로 나옴 | `@font-face`의 `font-family` 이름과 `--ss-font`에 적은 이름이 같은지, `url('./fonts/...')` 경로가 맞는지 확인해요 |

## 확인한 것과 확인하지 못한 것

- 디플래너가 해 본 것
  - 리눅스(깃허브 서버, Node 22, 2026-11-14~15): 같은 커밋 받기 → `npm install` → `npm run typecheck` · `npm run check:css` → Vite 미리 보기(`http://127.0.0.1:5173`) → `film.mjs`의 `--gate` · `--still` · `--reduced --still`까지 돌렸어요.
  - 윈도우 10, 클로드 코드: 「세팅」 0~3단계(스킬 폴더 정하기, 이 스킬 복사, PowerShell로 원본 받기, Node 확인)까지 해 봤어요(2026-11-15). 두 앱 폴더를 다루게 고친 이 판으로는 2026-11-17에 같은 단계와, Node가 없어 멈춘 뒤 새 대화에서 「이어서 해 줘」로 3단계까지 다시 가는 것을 해 봤어요.
- 확인하지 못한 것
  - 윈도우 · 맥에서 `npm install` 다음 단계(미리 보기 · 촬영)
  - 맥 · 리눅스의 Portless 주소(`http://stageshow.localhost:1355`). 디플래너 서버는 Portless를 거치지 않고 Vite를 바로 켰어요.
  - GPT 앱에서 쓰는 것: 스킬 폴더(`~/.agents/skills`)는 OpenAI 공식 문서를 따랐고, 디플래너는 클로드 코드에서만 시험했어요.

출처: Stageshow(`benjitaylor/skills` 커밋 299140f)의 README.md · SKILL.md · LICENSE · NOTICE.md · package.json · package-lock.json · scripts/dev.mjs · scripts/film.mjs · scripts/browser.mjs · playground · references(looks · craft · brands · rehearse), benji.org/stageshow, OpenAI 공식 문서(learn.chatgpt.com/docs/build-skills), 페이퍼로지 배포 페이지와 Freesentation/paperlogy 저장소, nodejs.org 릴리스 표. 확인 날짜 2026-11-15(두 앱 폴더는 2026-11-17). 문의: dplanner@outlook.kr
