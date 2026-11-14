---
name: dplanner-multi
description: 디플래너 멀티 기획 검토 스킬셋. 깃허브 인기 오픈소스 셋을 순서대로 돌려 기획 하나를 여러 AI가 검토한다. ① 리서치 스킬(Weizhena/Deep-Research-skills)로 사전조사 → ② AI 회의 스킬(0xNyk/council-of-high-intelligence)로 페르소나 회의 → ③ 디플래너 기획 법정(검사 · 변호인 · 재판장) → ④ markmap 마인드맵 → ⑤ 요약 보고서 한 장. "내 기획 멀티로 검토해 줘", "기획 법정 열어 줘", "이 아이디어 타당성 검증해 줘", "이 사업 될까?" 같은 요청에 쓴다. 처음 쓰면 「설치」 절대로 오픈소스 두 개를 먼저 설치한다.
---

# 디플래너 멀티 기획 검토 (스킬셋)

기획 하나를 넣으면 오픈소스 세 개와 디플래너 기획 법정을 순서대로 돌려, 사전조사부터 AI 회의 · 재판 · 마인드맵 · 요약 보고서까지 한 번에 만듭니다. 재판은 기획을 검토하기 위한 비유입니다. 법률 · 투자 · 재무 자문이 아닙니다.

- 시작하기 전에 사용자에게 한 줄로 알립니다. 클로드 코드에서 처음부터 끝까지 약 2시간이 걸리고, 하위 에이전트 10개(리서치 4개, 회의 6개)를 띄워 사용량 한도를 많이 씁니다. 2026-11-14 디플래너 시험에서는 AI 회의 단계에서만 하위 에이전트가 약 92만 토큰을 썼습니다.

## 스킬셋 구성

| 단계 | 하는 일 | 쓰는 것 | 만든 곳 |
|---|---|---|---|
| ① 사전조사 | 시장 · 경쟁 서비스 · 고객 · 규제 · 비용을 웹에서 깊게 조사 | 리서치 스킬 `/research` → `/research-deep` → `/research-report` | [Weizhena/Deep-Research-skills](https://github.com/Weizhena/Deep-Research-skills) (MIT) |
| ② AI 회의 | 페르소나 5명이 서로 보지 않고 분석하고, 익명으로 서로 따진 뒤, 의장이 평결 | AI 회의 스킬 `/council` | [0xNyk/council-of-high-intelligence](https://github.com/0xNyk/council-of-high-intelligence) (MIT) |
| ③ 기획 법정 | 검사 공소 → 변호인 변론 → 반대신문 → 재판장 판결 → 판결 검증 조사 | 이 파일 | 디플래너 |
| ④ 마인드맵 | 전체 과정을 마인드맵 한 장으로 | markmap | [markmap/markmap](https://github.com/markmap/markmap) (MIT) |
| ⑤ 요약 보고서 | 전체 과정을 HTML 보고서 한 장으로 정리 | 이 파일 | 디플래너 |

## 설치 (처음 한 번)

사용자가 이 파일을 주며 「설치해 줘」라고 하면 아래를 차례로 합니다. 설치 위치 `~`는 사용자 홈 폴더입니다(Windows는 `C:\Users\<이름>`). 명령은 Bash(Windows는 Git Bash)로 실행합니다.

1. **준비물 확인**: `git --version`, `python --version`(또는 `python3 --version`)을 확인합니다.
   - Windows에서 `python`이 Microsoft Store를 열거나 버전이 나오지 않으면, 먼저 `%LOCALAPPDATA%\Programs\Python\Python3*\python.exe`가 있는지 봅니다. 있으면 파이썬은 이미 설치되어 있고 터미널이 새 PATH를 아직 받지 못한 것입니다. 클로드 코드를 다시 열거나, 그 폴더를 이번 명령의 PATH 앞에 붙여 씁니다. 그 파일도 없으면 파이썬이 없는 것입니다. 사용자에게 알리고 허락을 받은 뒤 `winget install -e --id Python.Python.3.12 --scope user`로 설치합니다. macOS는 `brew install python` 또는 python.org 설치 파일을 씁니다. 설치한 뒤에는 새 터미널에서 다시 확인합니다.
   - 리서치 스킬이 쓰는 라이브러리를 설치합니다: `python -m pip install pyyaml`
   - Windows에서는 `python3`가 Microsoft Store 바로 가기여서 실행되지 않을 수 있습니다. 이 스킬셋과 원 스킬의 파이썬 명령은 모두 `python`으로 실행합니다.
2. **리서치 스킬 설치**(원 저장소 설명서와 같은 배치)
   ```bash
   git clone --depth 1 https://github.com/Weizhena/Deep-Research-skills.git /tmp/deep-research
   mkdir -p ~/.claude/skills ~/.claude/agents
   cp -r /tmp/deep-research/skills/research-en/* ~/.claude/skills/
   cp /tmp/deep-research/agents/web-search-agent.md ~/.claude/agents/
   cp -r /tmp/deep-research/agents/web-search-modules ~/.claude/agents/
   ```
3. **AI 회의 스킬 설치**(회의 스킬이 쓰는 파일을 손으로 복사)
   ```bash
   git clone --depth 1 https://github.com/0xNyk/council-of-high-intelligence.git /tmp/council
   mkdir -p ~/.claude/skills/council
   cp /tmp/council/SKILL.md ~/.claude/skills/council/SKILL.md
   cp -r /tmp/council/scripts /tmp/council/configs ~/.claude/skills/council/
   cp /tmp/council/agents/council-*.md ~/.claude/agents/
   ```
   - 원 저장소의 `install.sh`는 `scripts/detect-*.sh`만 복사하고, `configs/`는 `--copy-configs`를 줄 때만 복사합니다. 이 스킬셋은 회의 스킬이 쓰는 `scripts/`와 `configs/`를 모두 복사합니다.
   - 클로드 코드 화면에서 사용자가 직접 `/plugin marketplace add 0xNyk/council-of-high-intelligence` → `/plugin install council@council-of-high-intelligence`로 설치해도 됩니다(원 저장소 안내).
4. **마인드맵(markmap)**: 설치할 것이 없습니다. 보고서가 인터넷으로 불러 씁니다.
5. **이 파일**: `mkdir -p ~/.claude/skills/dplanner-multi`로 폴더를 만든 뒤 `~/.claude/skills/dplanner-multi/SKILL.md`로 저장합니다.
6. **확인**
   - `~/.claude/skills/`에 `research` · `research-deep` · `research-report` · `council` · `dplanner-multi`가 있는지 봅니다. 리서치 스킬의 `research-add-items` · `research-add-fields`도 함께 생기는데, 이 스킬셋에서는 쓰지 않으므로 그대로 둡니다.
   - `~/.claude/agents/`에 `web-search-agent.md`, `web-search-modules` 폴더, `council-` 파일 18개가 있는지 봅니다.
   - 새 스킬이 목록에 보이지 않으면 클로드 코드를 다시 엽니다. 내려받은 `/tmp/deep-research` · `/tmp/council`은 설치가 끝나면 쓰지 않습니다.

## 지킬 원칙

1. **증거가 먼저입니다.** 재판의 모든 주장에는 증거 번호(예: [E3])를 붙입니다. 증거가 없는 주장은 [추정]이라고 씁니다.
2. **맞장구치지 않습니다.** 사용자의 기획을 편들지 않습니다. 검사는 가장 강한 반론을 찾고, 변호인은 증거가 있는 방어만 합니다.
3. **판결은 증거로 내립니다.** 재판장은 양쪽 주장을 기계적으로 반씩 섞지 않습니다. 어느 쪽 주장이 증거로 더 뒷받침되는지 쟁점마다 판단합니다.
4. **사실과 추정을 나눕니다.** 숫자와 사건에는 출처 · 날짜를 붙이고, 오래된 자료(2년 넘음)는 날짜를 밝힙니다.
5. **사용자의 언어로 씁니다.** 리서치 스킬은 조사 결과를 영어로 남깁니다. 보고서와 답변은 사용자의 언어(한국어 등)로 옮겨 씁니다.
6. **비밀을 넣지 않습니다.** 사용자가 회사 내부 자료를 붙이면 보고서에 그대로 옮기지 말고 요약만 씁니다.
7. **원 스킬의 절차를 그대로 따릅니다.** 리서치 스킬과 AI 회의 스킬은 각자의 SKILL.md 순서대로 돌립니다. 이 파일이 바꾸는 것은 아래 「한 번에 진행」의 기본값뿐입니다.

## 한 번에 진행 (기본값)

리서치 스킬은 단계마다 사람에게 확인을 받도록 만들어져 있습니다. 이 스킬셋은 사용자가 따로 말하지 않으면 그 확인 자리에 아래 기본값으로 답하고 묻지 않고 이어 갑니다. 사용자가 「단계마다 확인할게」라고 하면 원 스킬대로 묻습니다.

| 원 스킬이 묻는 것 | 기본값 |
|---|---|
| `/research` 1단계: 항목 · 필드를 더하거나 뺄까 | 항목 5~6개로 맞추고 그대로 진행. 항목은 경쟁 · 대체 서비스 3~4개와 「시장과 수요」 · 「규제와 비용」 같은 주제 항목 1~2개 |
| `/research` 2단계: 조사 기간 | 최근 2년 |
| `/research` 3단계: 기존 필드 파일이 있나 | 없음 |
| `/research` 4단계: batch_size · items_per_agent | batch_size 3, items_per_agent 2, output_dir `./results` |
| `/research-deep`: 다음 배치를 시작할까 | 이어서 시작 |
| `/research-report`: 목차에 보일 필드 | 가격처럼 숫자 · 짧은 값 2~3개 |
| `/council`: 문제를 다시 쓴 결과가 원래 질문과 다름 | 회의록에 적고 그대로 진행 |

- 필드(fields.yaml)에는 꼭 `sources`(출처 주소 목록)와 `as_of`(자료 날짜)를 넣습니다. 보고서의 증거 목록이 이 두 필드에서 나옵니다.
- 필드 카테고리 이름은 검증 스크립트(`validate_json.py`)가 아는 이름 가운데서 고릅니다: `basic_info` · `business_info` · `market_positioning` · `competition_ecosystem` · `technical_features` · `performance_metrics` · `milestone_significance` · `history`. 다른 이름으로 묶으면 그 안의 필드를 읽지 못해 검증에서 실패합니다.
- `items_per_agent`가 2이면 `/research-deep`의 프롬프트 템플릿을 항목마다 한 번씩 채우고, 채운 두 개를 한 에이전트에게 함께 줍니다.
- 1단계에서 정한 항목이 조사해 보니 폐업하거나 중단된 서비스라면, 그 항목을 「실패 선례」로 바꿔 이어서 조사합니다.
- 값을 찾지 못하면 원 스킬대로 `[uncertain]`으로 둡니다. 계산하거나 추정해서 채운 값은 값 앞에 `Estimate:`를 붙이고 근거를 함께 씁니다. `[uncertain]` 값은 보고서에서 빠지므로, 추정을 확인된 값처럼 섞어 쓰지 않습니다.
- 회의에서 70%가 넘는 멤버가 같은 결론을 내면 회의 스킬이 집행 검사(반대 의견 요청)를 합니다(원 스킬 STEP 4). 반대 의견을 요청할 두 명은 1라운드에서 확신도가 낮았거나 조건을 가장 많이 단 멤버로 고릅니다.
- 한 번의 요청 안에서 쓸 수 있는 웹 검색 횟수에는 한도가 있습니다. 시험(2026-11-14)에서는 리서치 단계가 한도를 다 써서 ③ 판결 검증 때 검색이 막혔습니다. 그때는 검색 대신 증거 목록에 있는 원 출처 주소를 직접 열어 확인합니다.

## 진행 순서

### 0단계: 사건 접수

- 기획을 한 문단으로 정리합니다: 누구에게(고객), 무엇을(제품 · 서비스), 어떻게(방식 · 채널), 돈은 어떻게(가격 · 수익 구조), 어디서 · 언제.
- 핵심이 빠져 있으면 한 번만 묻습니다(최대 3개 항목). 빠진 것이 없거나 사용자가 「알아서」라고 하면 합리적인 가정을 [가정]으로 적고 바로 진행합니다.
- 사건명은 「(날짜) (기획 한 줄)」로 짓고, 작업 폴더 아래 `multi-review/YYYYMMDD-<영문 짧은 이름>/`을 사건 폴더로 만듭니다. ①~⑤의 결과는 모두 이 폴더에 둡니다.

### ① 사전조사: 리서치 스킬 돌리기

1. 사건 폴더에서 `research` 스킬을 주제 「(기획 한 줄): 시장 · 경쟁 서비스 · 고객 · 규제 · 비용」으로 실행합니다(`/research <주제>`).
2. 이어서 `research-deep`(`/research-deep`)으로 항목마다 조사를 맡기고, `research-report`(`/research-report`)로 리서치 보고서를 만듭니다. 리서치 스킬은 결과를 사건 폴더 안의 `{topic_slug}/` 폴더(예: `gangnam-lunch-subscription/`)에 저장합니다.
3. 원 스킬의 결과 파일(`{topic_slug}/outline.yaml` · `fields.yaml` · `results/*.json` · `generate_report.py` · `report.md`)은 그대로 둡니다.
4. 결과에서 증거 목록을 12~20개로 뽑아 사용자의 언어로 옮깁니다.

| 번호 | 내용(한두 줄) | 출처 | 날짜 | 신뢰도 | 구분 |
|---|---|---|---|---|---|
| E1 | ... | 출처 이름 + 주소 | YYYY-MM-DD | 높음 · 보통 · 낮음 | 사실 · 추정 |

- 같은 사실을 두 출처 이상에서 확인하면 신뢰도를 「높음」으로 둡니다. `[uncertain]`으로 남은 값은 증거로 쓰지 않고 「찾지 못함」에 적습니다.

### ② AI 회의: 회의 스킬 돌리기

1. `council` 스킬을 다음처럼 실행합니다.
   ```
   /council --members munger,sun-tzu,machiavelli,kahneman,rams (사건 요약) 이 기획을 지금 형태로 추진해야 하는가? 근거 자료: (증거 목록 E1~En 요약)
   ```
   - 다섯 자리는 경제성(Munger) · 경쟁(Sun Tzu) · 이해관계(Machiavelli) · 판단 편향(Kahneman) · 사용자(Rams)를 봅니다. 사용자가 다른 구성을 말하면 그 구성을 씁니다.
2. 회의 스킬의 절차(문제 다시 쓰기 → 1라운드 서로 보지 않고 분석 → 2라운드 익명 교차 질문 → 3라운드 최종 입장 → 의장 평결)를 빠뜨리지 않고 따릅니다.
   - 2 · 3라운드는 1라운드를 맡은 멤버 에이전트에게 이어서 보냅니다(SendMessage처럼 같은 에이전트에 이어 보내는 기능을 씁니다). 원 스킬의 3라운드 프롬프트에는 앞 라운드 내용이 들어 있지 않기 때문입니다. 이어 보낼 수 없으면 그 멤버의 앞 라운드 발언을 프롬프트에 붙입니다.
   - 증거 목록과 1라운드 익명 원문은 사건 폴더에 파일로 저장하고, 프롬프트에는 그 경로를 넘깁니다. 그러면 프롬프트가 지나치게 길어지지 않습니다.
3. 회의 스킬은 Codex · Gemini CLI 같은 다른 AI 도구가 설치되어 있으면 자리를 그 도구들에도 나눠 맡깁니다(원 스킬의 기본 동작). 클로드만 쓰려면 `--no-auto-route`를 붙입니다. 어느 쪽으로 돌았는지 보고서에 적습니다.
4. 의장 평결 전문을 사건 폴더의 `council-verdict.md`로 저장합니다. 이 평결의 투표 집계를 재판의 배심원 평결로 씁니다. 라운드별 원문은 `council-transcript.md`로 함께 저장해 둡니다.

### ③ 기획 법정 (디플래너)

1. **검사 공소**: 이 기획이 실패할 가장 강한 이유 3~5개를 씁니다. 공소 사실마다 증거 번호나 회의의 소수 의견 · 중단 기준(Kill Criteria)을 붙이고, 재판장이 판단할 핵심 쟁점을 2~4개로 정리합니다. 과장하거나 비꼬지 않습니다.
2. **변호인 변론**: 공소 사실마다 증거로 반박하거나, 인정하고 보완책을 냅니다. 보완책에는 비용 · 기간 같은 현실 조건을 붙입니다.
3. **반대신문**: 검사가 변론의 가장 약한 지점 하나를 다시 공격하고, 변호인이 한 번 답합니다. 각각 3~5줄로 씁니다.
4. **재판장 판결**
   - 주문: 인용(지금 형태로 추진) · 조건부 인용(조건을 채우면 추진) · 기각(지금 형태로는 멈춤) 중 하나
   - 판결 이유: 쟁점마다 어느 쪽 주장이 증거로 더 뒷받침되는지 씁니다. 회의 평결과 판결이 다르면 그 이유를 씁니다.
   - 보완 조건(조건부 인용일 때 2~4개, 기간과 숫자로 확인할 수 있게) 또는 재심 청구 조건(기각일 때)
   - 확신도: 높음 · 보통 · 낮음과 그 이유
5. **판결 검증 조사**: 판결을 떠받치는 핵심 근거 1~2개와 조건 2~3개를 웹에서 다시 확인합니다(V1, V2 …). 결과에 따라 「판결 유지」 또는 「판결 수정 의견」을 따로 적습니다. 판결문을 몰래 고치지 않습니다.
   - 검증해 보니 증거의 문구를 고쳐야 하면, 증거 목록과 판결문은 그대로 두고 「표현 정정 의견」에 적습니다. 회의에는 고치기 전 문구가 전달되었다는 점도 함께 적습니다.
   - 웹 검색이 한도에 걸리면 증거 목록에 있는 원 출처 주소를 직접 엽니다.
6. 공소 · 변론 · 반대신문 · 판결 · 검증을 사건 폴더의 `court.md`로 저장합니다.

### ④ 마인드맵 (markmap)

- 가운데에 기획 한 줄을 두고, 가지를 사전조사(핵심 5개) · AI 회의(자리별 최종 입장) · 쟁점(검사 대 변호인) · 판결(주문 · 이유) · 조건 · 검증 결과 · 다음 할 일로 나눕니다.
- 마크다운 제목(#, ##)과 목록으로 쓰고, 한 항목은 25자 안팎으로 줄입니다. 같은 가지 바로 아래에 목록(-)과 ### 제목을 함께 두지 않습니다(함께 두면 목록이 마인드맵에서 빠짐).

### ⑤ 요약 보고서

사건 폴더에 `report.html`을 만듭니다. 마크다운도 필요하면 같은 내용을 `summary.md`로 저장합니다. 리서치 스킬이 만든 `{topic_slug}/report.md`와 헷갈리지 않도록 이름을 다르게 둡니다. 순서는 이렇습니다.

1. 머리: 사건명, 날짜, 주문(큰 글씨, 인용은 초록 · 조건부 인용은 노랑 · 기각은 빨강), 사건 요약과 [가정]
2. 한눈에 보기: 회의 평결 집계, 판결 이유 세 줄, 조건
3. 마인드맵
4. 사전조사: 리서치 스킬 보고서 요약과 증거 목록(표), 찾지 못함
5. AI 회의: 자리 구성, 자리별 최종 입장, 소수 의견, 중단 기준, 의장 평결 요약, 다른 AI 도구를 썼는지
6. 공방(공소 · 변론 · 반대신문)
7. 판결 이유와 확신도
8. 판결 검증 조사
9. 다음 할 일(체크리스트)
10. 이 보고서를 만든 스킬: 위 「스킬셋 구성」 표
11. 알림과 출처: 「이 재판은 기획 검토를 위한 비유이며 법률 · 투자 · 재무 자문이 아닙니다.」, 출처 전체

- 클로드 앱처럼 파일을 쓸 수 없는 곳에서는 HTML(또는 아티팩트)로 보여 주고 내려받을 수 있게 합니다.
- 이 스킬셋을 하위 에이전트로 돌리면 보고서 형식의 `.md` 파일 쓰기가 막힐 수 있습니다. 그때는 `report.html`처럼 쓸 수 있는 파일만 저장하고, 나머지 내용은 답변에 붙여 돌려줍니다. 부모 세션이 그 답변을 받아 저장합니다.
- 마지막 답변은 짧게 씁니다: 주문, 판결 이유 세 줄, 조건, 보고서 위치.

## 보고서 HTML 틀

`{ }` 부분을 채웁니다. 마인드맵은 인터넷이 연결되어 있을 때 markmap(jsDelivr)을 불러와 그립니다. 인터넷이 없으면 마인드맵 칸이 비어 보이므로, 아래 「마인드맵 원문」 상자에 같은 마크다운을 글로 넣습니다.

- 표는 모두 `<div class="tw">`로 감쌉니다. 그러면 휴대폰처럼 좁은 화면에서도 본문이 옆으로 넘치지 않고 표만 가로로 밀어 볼 수 있습니다.
- 표의 출처 칸에는 `<a href="주소">출처 이름</a>`처럼 이름만 보이게 넣고, 주소 전체는 맨 아래 출처 목록에 모읍니다. 주소를 그대로 넣으면 표가 넓어집니다.

```html
<!doctype html>
<html lang="ko">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>멀티 기획 검토 · {사건명}</title>
<style>
  :root { --ink:#1d1d1f; --sub:#5b5b66; --line:#e3e3e8; --bg:#ffffff; --card:#f6f6f8;
          --grant:#1a7f37; --cond:#b7791f; --deny:#c62828; }
  * { box-sizing:border-box; }
  body { margin:0; background:var(--bg); color:var(--ink);
         font-family:"Pretendard","Apple SD Gothic Neo","Malgun Gothic",system-ui,sans-serif; line-height:1.6; }
  main { max-width:960px; margin:0 auto; padding:32px 20px 64px; }
  h1 { font-size:26px; margin:0 0 4px; } h2 { font-size:20px; margin:40px 0 12px; border-bottom:2px solid var(--line); padding-bottom:6px; }
  .meta { color:var(--sub); font-size:14px; }
  .verdict { margin:20px 0; padding:20px 24px; border-radius:14px; color:#fff; font-size:28px; font-weight:800; }
  .verdict.grant { background:var(--grant); } .verdict.cond { background:var(--cond); } .verdict.deny { background:var(--deny); }
  .verdict small { display:block; font-size:15px; font-weight:500; opacity:.95; margin-top:6px; }
  .grid { display:grid; grid-template-columns:repeat(auto-fit,minmax(220px,1fr)); gap:12px; }
  .card { background:var(--card); border-radius:12px; padding:14px 16px; }
  .stage { display:inline-block; font-size:12px; color:var(--sub); border:1px solid var(--line); border-radius:999px; padding:2px 10px; margin-left:8px; vertical-align:middle; }
  .tw { overflow-x:auto; -webkit-overflow-scrolling:touch; margin:8px 0; }
  table { width:100%; border-collapse:collapse; font-size:14px; }
  td a, li a { word-break:break-all; }
  th, td { border-bottom:1px solid var(--line); padding:8px 6px; text-align:left; vertical-align:top; }
  th { background:var(--card); }
  .markmap { width:100%; height:720px; border:1px solid var(--line); border-radius:12px; }
  details { margin-top:8px; } pre { white-space:pre-wrap; background:var(--card); padding:12px; border-radius:10px; font-size:13px; }
  .note { color:var(--sub); font-size:13px; }
</style>
<script src="https://cdn.jsdelivr.net/npm/markmap-autoloader@0.18.12"></script>
</head>
<body>
<main>
  <h1>{사건명}</h1>
  <div class="meta">{날짜} · 디플래너 멀티 기획 검토</div>

  <div class="verdict {grant|cond|deny}">주문: {인용 · 조건부 인용 · 기각}
    <small>{주문을 한 문장으로}</small></div>
  <p>{사건 요약과 [가정]}</p>

  <h2>한눈에 보기</h2>
  <div class="grid">
    <div class="card"><b>AI 회의 평결</b><br>{자리별 최종 입장 집계}</div>
    <div class="card"><b>판결 이유</b><br>{세 줄}</div>
    <div class="card"><b>{보완 조건 · 기각이면 재심 청구 조건}</b><br>{목록}</div>
  </div>

  <h2>마인드맵 <span class="stage">④ markmap</span></h2>
  <div class="markmap"><script type="text/template">
{마인드맵 마크다운}
  </script></div>
  <details><summary>마인드맵 원문(인터넷이 없을 때)</summary><pre>{마인드맵 마크다운}</pre></details>

  <h2>사전조사 <span class="stage">① 리서치 스킬</span></h2>
  {리서치 스킬 보고서 요약}
  <div class="tw"><table><tr><th>번호</th><th>내용</th><th>출처</th><th>날짜</th><th>신뢰도</th><th>구분</th></tr>
  {증거 행: 출처 칸은 <a href="주소">출처 이름</a>}
  </table></div>
  {찾지 못함}

  <h2>AI 회의 <span class="stage">② AI 회의 스킬</span></h2>
  {자리 구성 · 자리별 최종 입장 · 소수 의견 · 중단 기준 · 의장 평결 요약 · 다른 AI 도구 사용 여부}

  <h2>공방 <span class="stage">③ 기획 법정</span></h2>
  {공소 사실 · 변론 · 반대신문}

  <h2>판결 이유와 확신도 <span class="stage">③ 기획 법정</span></h2>
  {쟁점별 판단, 확신도}

  <h2>판결 검증 조사 <span class="stage">③ 기획 법정</span></h2>
  {V 번호 자료, 판결 유지 또는 수정 의견}

  <h2>다음 할 일</h2>
  {체크리스트}

  <h2>이 보고서를 만든 스킬</h2>
  {스킬셋 구성 표}

  <h2>알림과 출처</h2>
  <p class="note">이 재판은 기획 검토를 위한 비유이며 법률 · 투자 · 재무 자문이 아닙니다.</p>
  {출처 목록}
</main>
</body>
</html>
```

## 라이선스와 만든 곳

- ① 리서치 스킬: Weizhena/Deep-Research-skills (MIT). 원 저장소에서 설치해 그대로 돌립니다.
- ② AI 회의 스킬: 0xNyk/council-of-high-intelligence (MIT). 원 저장소에서 설치해 그대로 돌립니다.
- ④ 마인드맵: markmap (MIT). 보고서에서 jsDelivr로 불러 씁니다.
- 전체 순서와 「한 번에 진행」 기본값, ③ 기획 법정, ⑤ 보고서 틀은 디플래너가 만들었습니다. 만든 곳: 디플래너(dplanner@outlook.kr)
