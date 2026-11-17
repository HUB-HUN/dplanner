---
name: dplanner-plan10
description: 디플래너 기획 조사 10단계 스킬셋. 깃허브 인기 스킬 셋(phuryn/pm-skills, wshobson/agents의 startup-business-analyst, NomaDamas/k-skill)을 순서대로 돌려, 아이디어 한 줄을 시장 · 트렌드 · 고객 · VOC · 경쟁사 · 종합 · 문제 정의 · 수익모델과 가격 · 사업성 · 리스크 10단계로 조사하고, 숫자마다 출처를 붙인 보고서 한 장으로 만든다. "이 아이디어 기획 조사해 줘", "시장조사부터 수익모델까지 해 줘", "신사업 사업성 봐 줘", "기획 전에 조사할 것 다 해 줘" 같은 요청에 쓴다. 처음 쓰면 「설치」 절대로 원 스킬을 먼저 설치한다.
---

# 디플래너 기획 조사 10단계 (스킬셋)

아이디어 한 줄을 넣으면 인기 스킬 세 묶음을 순서대로 돌려, 기획에 들어가기 전에 하는 조사 10단계를 한 번에 끝내고 보고서 한 장(`report.html`)으로 정리합니다. 보고서의 숫자에는 모두 출처 번호가 붙습니다. 사업 · 투자 · 법률 자문이 아닙니다.

- 시작하기 전에 사용자에게 한 줄로 알립니다: 조사에 한 시간 안팎이 걸리고(맨 아래 「시험 기록」), 웹 검색을 여러 번 써서 사용량을 많이 씁니다. 하위 에이전트 · 예약 실행처럼 중간에 말할 수 없으면 이 안내를 마지막 답변 맨 앞에 적습니다.
- 원 스킬의 저장 위치 · 파일 이름 · 출력 언어 · 보고 단위 지시가 이 파일과 다르면 이 파일을 따릅니다. 예: `pre-mortem`이 권하는 `PreMortem-….md` 대신 `10-risk.md`에 쓰고, 재무 기간과 단위는 「한 번에 진행」 표를 따릅니다.

## 스킬셋 구성

| 단계 | 하는 일 | 쓰는 스킬 | 만든 곳 |
|---|---|---|---|
| 0 조사 계획서 | 내릴 결정 · 고객 가설 · 문제 가설 · 조사 질문 · 범위 정하기 | 이 파일 | 디플래너 |
| 1 시장 · 거시 환경 | 한국 통계로 시장 규모(TAM · SAM · SOM)와 바깥 환경(PEST) | `kosis-stats` · `bok-ecos-stats`, `market-sizing`, `pestle-analysis` | k-skill, pm-skills |
| 2 트렌드 · 수요 | 관심과 수요가 실제로 있는지, 언제 몰리는지 | 웹 검색, `kosis-stats`(시계열) | 이 파일, k-skill |
| 3 고객 조사 | 인터뷰 질문지 · 설문지 · 페르소나 | `interview-script`, `survey-design`, `user-personas` | pm-skills |
| 4 VOC · 리뷰 | 기존 제품에 대한 불만과 요구 | `sentiment-analysis` | pm-skills |
| 5 경쟁사 | 경쟁사 5곳 비교표(기능 · 가격) · 다섯 가지 힘 | `competitor-analysis`, `porters-five-forces` | pm-skills |
| 6 종합 · 포지셔닝 | 3C · SWOT · STP · 포지셔닝 맵 | `swot-analysis`, `competitive-landscape` | pm-skills, wshobson/agents |
| 7 문제 정의 · 가치 제안 · 가설 | 풀 문제 · 가치 제안문 · 검증할 가설 | `value-proposition`, `identify-assumptions-new` | pm-skills |
| 8 수익모델 · 가격 | 수익 모델 비교 · 가격 티어 · 린 캔버스 | `monetization-strategy`, `pricing-strategy`, `lean-canvas` | pm-skills |
| 9 사업성 · 재무 | 3년 추정 · 단위 경제(CAC · LTV) · 손익분기 | `startup-financial-modeling`, `startup-metrics-framework`, 손익분기 계산 | wshobson/agents, 이 파일 |
| 10 리스크 · 규제 | 한국 법령 · 판례 확인 · 프리모템 | `korean-law-search`, `pre-mortem` | k-skill, pm-skills |
| 끝 보고서 | 결론(진행 · 조건부 진행 · 보류) · 출처 원장 · 다음 할 일 | 이 파일 | 디플래너 |

- 원 저장소: [phuryn/pm-skills](https://github.com/phuryn/pm-skills)(MIT), [wshobson/agents](https://github.com/wshobson/agents)(MIT, `plugins/startup-business-analyst`), [NomaDamas/k-skill](https://github.com/NomaDamas/k-skill)(MIT, 프록시 폴더만 AGPL-3.0)
- pm-skills와 wshobson/agents의 스킬은 원래 이름 그대로 `~/.claude/skills/`에 설치해 부릅니다. k-skill은 스크립트와 설명서만 이 스킬 폴더 안(`vendor/k-skill/`)에 받아 이 파일이 직접 실행합니다. k-skill의 SKILL.md는 실행하면 저장소 전체를 전역으로 다시 설치하는 명령(`npx ... update`)을 먼저 시키기 때문에 넣지 않습니다.

## 설치 (처음 한 번)

사용자가 이 파일을 주며 「설치해 줘」라고 하면 아래를 차례로 합니다. `~`는 사용자 홈 폴더입니다(Windows는 `C:\Users\<이름>`). 명령은 Bash(Windows는 Git Bash)로 실행합니다.

1. **준비물 확인**: `git --version`, `python --version`을 확인합니다.
   - Windows에서 `python`이 Microsoft Store를 열거나 버전이 나오지 않으면 `%LOCALAPPDATA%\Programs\Python\Python3*\python.exe`가 있는지 봅니다. 있으면 터미널이 새 PATH를 아직 받지 못한 것이니 그 폴더를 PATH 앞에 붙여 씁니다. 없으면 사용자에게 알리고 허락을 받은 뒤 `winget install -e --id Python.Python.3.12 --scope user`로 설치합니다. macOS는 `brew install python`을 씁니다.
   - Windows의 `python3`는 Microsoft Store 바로 가기일 수 있습니다. 이 파일의 파이썬 명령은 모두 `python`으로 실행합니다.
   - k-skill 스크립트는 파이썬 표준 라이브러리만 씁니다. 따로 설치할 패키지가 없습니다.
   - 파이썬을 `-I`(격리 모드)로 실행하면 `PYTHONUTF8=1`이 무시되어 한글이 깨집니다. 그럴 때는 `-X utf8`을 붙입니다.
   - 처음 설치하는데(`~/.claude/skills/dplanner-plan10`이 없음) 아래 2 · 3번 스킬과 같은 이름의 폴더가 `~/.claude/skills/`에 이미 있으면, 덮어쓰기 전에 사용자에게 알리고 허락을 받습니다.
   - `/tmp/plan10-*` 폴더가 남아 있으면 처음 설치이더라도 먼저 지웁니다. 다시 설치하거나 지난 설치가 중간에 멈추면 남아 있을 수 있고, 남아 있으면 clone이 실패합니다: `rm -rf /tmp/plan10-pm-skills /tmp/plan10-agents /tmp/plan10-k-skill`
   - `/tmp/plan10-*`는 이름이 고정된 폴더라서, 설치를 두 개 동시에 돌리면 서로의 사본을 지우거나 clone이 실패합니다. 설치는 한 번에 하나씩 돌립니다.
2. **pm-skills 설치**(스킬 15개). 명령마다 작업 폴더가 바뀌어도 되도록 모두 절대 경로로 씁니다.
   ```bash
   git clone --depth 1 https://github.com/phuryn/pm-skills.git /tmp/plan10-pm-skills
   mkdir -p ~/.claude/skills
   for s in pm-market-research/skills/market-sizing pm-market-research/skills/user-personas \
            pm-market-research/skills/survey-design pm-market-research/skills/sentiment-analysis \
            pm-market-research/skills/competitor-analysis pm-product-discovery/skills/interview-script \
            pm-product-discovery/skills/identify-assumptions-new pm-product-strategy/skills/pestle-analysis \
            pm-product-strategy/skills/swot-analysis pm-product-strategy/skills/porters-five-forces \
            pm-product-strategy/skills/value-proposition pm-product-strategy/skills/lean-canvas \
            pm-product-strategy/skills/monetization-strategy pm-product-strategy/skills/pricing-strategy \
            pm-execution/skills/pre-mortem; do
     cp -r "/tmp/plan10-pm-skills/$s" ~/.claude/skills/
   done
   ```
   - pm-skills에는 `business-model` 같은 다른 스킬도 있지만, 이 스킬셋은 사업 모델을 `lean-canvas` 한 장으로 정리하므로 받지 않습니다.
   - pm-skills README의 「Known Issue on Windows」 절에는 SYSTEM 권한 예약 작업을 등록하는 코드가 있습니다. 이 스킬셋과 관계가 없으므로 실행하지 않습니다.
3. **wshobson/agents의 startup-business-analyst 설치**(스킬 4개, 필요한 폴더만 받음)
   ```bash
   git clone --depth 1 --filter=blob:none --sparse https://github.com/wshobson/agents.git /tmp/plan10-agents
   git -C /tmp/plan10-agents sparse-checkout set plugins/startup-business-analyst
   for s in market-sizing-analysis competitive-landscape startup-financial-modeling startup-metrics-framework; do
     cp -r /tmp/plan10-agents/plugins/startup-business-analyst/skills/$s ~/.claude/skills/
   done
   ```
4. **이 파일과 k-skill 스크립트**(k-skill은 스크립트 · 설명서만)
   ```bash
   mkdir -p ~/.claude/skills/dplanner-plan10/vendor/k-skill
   cp "<사용자가 준 이 파일>" ~/.claude/skills/dplanner-plan10/SKILL.md
   git clone --depth 1 --filter=blob:none --sparse https://github.com/NomaDamas/k-skill.git /tmp/plan10-k-skill
   git -C /tmp/plan10-k-skill sparse-checkout set kosis-stats bok-ecos-stats korean-law-search
   for s in kosis-stats bok-ecos-stats korean-law-search; do
     d=~/.claude/skills/dplanner-plan10/vendor/k-skill/$s; mkdir -p "$d"
     cp -r /tmp/plan10-k-skill/$s/scripts /tmp/plan10-k-skill/$s/instruction.md "$d"/
     [ -d /tmp/plan10-k-skill/$s/references ] && cp -r /tmp/plan10-k-skill/$s/references "$d"/
   done
   cp /tmp/plan10-k-skill/LICENSE ~/.claude/skills/dplanner-plan10/vendor/k-skill/LICENSE
   ```
5. **확인과 정리**
   - `~/.claude/skills/`에 위 스킬 19개(pm-skills 15개, wshobson/agents 4개)와 `dplanner-plan10`이 있는지 봅니다.
   - `~/.claude/skills/dplanner-plan10/vendor/k-skill/`에 `kosis-stats` · `bok-ecos-stats` · `korean-law-search` 폴더와 `LICENSE`가 있는지 봅니다.
   - 시험 삼아 한 번 부릅니다: `PYTHONUTF8=1 python ~/.claude/skills/dplanner-plan10/vendor/k-skill/kosis-stats/scripts/run_kosis_stats.py search --query "사업체" --text`
   - 각 저장소의 커밋을 적어 둡니다: `git -C /tmp/plan10-pm-skills rev-parse HEAD`(나머지 둘도 같음).
   - 받은 커밋이 맨 아래 「시험 기록」의 커밋과 다르면, 사본을 지우기 전에 이 스킬셋이 쓰는 폴더만 비교합니다. `git -C <사본> fetch --depth 1 origin <기록 커밋>`으로 기록 커밋을 받은 뒤 `git -C <사본> diff --stat <기록 커밋> HEAD -- <폴더들>`을 봅니다. 아무것도 나오지 않으면 받은 그대로 쓰고, 바뀐 파일이 나오면 그 목록을 사용자에게 알립니다.
     - 쓰는 폴더: pm-skills는 2번 `for` 목록의 15개, wshobson/agents는 3번 `for` 목록의 4개(앞에 `plugins/startup-business-analyst/skills/`를 붙임), k-skill은 `kosis-stats bok-ecos-stats korean-law-search LICENSE`입니다.
   - 커밋을 적은 뒤 받은 사본을 지웁니다: `rm -rf /tmp/plan10-pm-skills /tmp/plan10-agents /tmp/plan10-k-skill`. 설치한 스킬은 `~/.claude/skills/`에 복사되어 있어서 지워도 그대로 쓸 수 있습니다.
   - 원 저장소가 바뀌어 어떤 단계가 실패하면, 2~4번의 clone 바로 뒤에 `git -C <폴더> fetch --depth 1 origin <커밋> && git -C <폴더> checkout <커밋>`(커밋은 「시험 기록」의 값)을 넣어 다시 설치합니다.
   - 새 스킬이 목록에 보이지 않으면 클로드 코드를 다시 엽니다.

## 지킬 원칙

1. **숫자마다 출처를 붙입니다.** 보고서와 단계 파일의 숫자에는 출처 번호 `[S1]`을 붙이고, 출처 원장(`ledger.md`)에 번호 · 내용 · 값 · 단위 · 기관 · 주소 · 자료 날짜 · 확인 날짜를 적습니다. 출처가 없는 숫자는 `[가정]`(사용자 · 스킬셋이 정한 값) 또는 `[추정]`(계산한 값, 계산식을 함께 적음)으로 표시합니다. 이 셋 가운데 아무것도 붙지 않은 숫자는 쓰지 않습니다.
   - 표시하지 않아도 되는 숫자: 날짜 · 연도 · 시점(「n개월 차」 · 「n년 차」), 연령대(「30대」), 조문 · 판례 번호, 단계 · 문항 · 가설 · 항목 번호, 공식 속 단위 환산 상수(12개월 · 100%), 표 머리글에 표시를 붙인 열의 칸.
   - 시장 정의에 쓴 구간(예: 종사자 5~299명)은 처음 나오는 곳에 한 번 `[가정]`과 `[확인 필요]`를 붙이고, 뒤에서는 다시 붙이지 않습니다.
   - 인터뷰 · 설문의 설계값(인원 · 시간 · 보기)은 파일 머리말에서 한 번 `[가정]`이라고 밝히면 됩니다.
   - 사용자가 아이디어 문장에 직접 쓴 조건(예: 「매주」 → 주 1회)은 0단계에서 한 번 「사용자 조건」이라고 밝히면, 뒤에서는 다시 표시하지 않아도 됩니다.
   - 0단계에서 정한 설계값(예: 시범 기간 · 견적 수)도 정할 때 한 번 `[가정]`이라고 밝히면, 뒤에서는 다시 표시하지 않아도 됩니다.
2. **지어내지 않습니다.** 원 스킬 안의 예시 숫자 · 회사 이름 · 보고서 이름을 결과에 옮기지 않습니다. 원 스킬 예시 가운데 계산이 틀린 것도 있습니다(예: wshobson `examples/saas-market-sizing.md`). 찾지 못한 값은 「찾지 못함」으로 둡니다.
   - 웹 검색 결과 요약에 나온 숫자는 그대로 쓰지 않습니다. 원문 페이지를 열어 확인한 값만 쓰고, 요약과 원문이 다르면 원문 값을 씁니다.
3. **한국 기준으로 씁니다.** 금액은 원화로 쓰고, 달러 자료는 환율과 환율 기준일을 함께 적습니다. 국내 자료(KOSIS 통계 · 한국은행 · 공시 · 법령)를 먼저 찾습니다. 원 스킬에 들어 있는 미국 · 투자 업계 기준 숫자(예: LTV가 CAC의 3배 이상, 프리미엄 전환율 1~5%)는 「해외 일반 기준」이라고 밝히고, 출처 원장에 그 원 스킬 파일(저장소 주소)을 올려 번호를 붙입니다.
4. **네이버 검색 결과는 넣지 않습니다.** 네이버 검색 API 이용 특약이 검색 결과를 AI에 넣는 것을 막는다는 보도가 있습니다(2026-09-07 시행). 그래서 네이버 검색 결과를 모아 클로드에 넣지 않습니다. 사용자가 네이버 데이터랩 화면에서 직접 내려받은 파일을 주면 그 파일만 읽고, 상대 지수라는 점을 밝힙니다.
5. **사람이 정할 곳은 표시만 하고 이어 갑니다.** 시장 정의 · 가정값 · 표적 고객 · 법률 해석 · 최종 결론 다섯 곳은 사람이 확인해야 합니다. 기본으로는 묻지 않고 `[확인 필요]`를 붙여 진행하고, 보고서의 「사람이 확인할 것」에 모읍니다.
6. **회사 비밀은 밖으로 보내지 않습니다.** `kosis-stats` 기본 조회와 `korean-law-search`는 검색어 · 통계표 번호가 k-skill 운영자 서버(`k-skill-proxy.nomadamas.org`)를 거칩니다. 회사 내부 정보는 검색어에 넣지 않습니다. KOSIS 무료 키를 받아 `--direct`를 쓰면 운영자 서버를 거치지 않습니다(`vendor/k-skill/kosis-stats/instruction.md`). 사용자가 붙인 내부 자료는 보고서에 그대로 옮기지 않고 요약만 씁니다.
7. **원 스킬의 홍보 · 참고 링크는 옮기지 않습니다.** 원 스킬이 추천하는 작성자의 상품(예: survey-design의 설문 도구)과 Further Reading 링크는 결과물에 넣지 않습니다.
8. **사용자의 언어로 씁니다.** 원 스킬의 출력 틀은 영어입니다. 절 이름은 한국어로 바꾸고, TAM · JTBD · CAC 같은 약어는 괄호로 함께 적습니다.

## 한 번에 진행 (기본값)

사용자가 따로 말하지 않으면 아래 기본값으로 끝까지 진행합니다. 묻는 곳은 0단계의 한 번뿐입니다(0단계 참고). 사용자가 「단계마다 확인할게」라고 하면 단계가 끝날 때마다 결과를 보여 주고 다음 단계로 갈지 묻습니다.

| 정할 것 | 기본값 |
|---|---|
| 지역 · 통화 | 한국, 원화 |
| SOM 기간 | 3년(pm-skills market-sizing의 1~3년에 맞춤) |
| 재무 추정 기간 | 3년, 1년 차는 분기별, 2~3년 차는 연간 |
| 재무 시나리오 | 보수 · 기본 · 낙관 세 가지(wshobson의 P10 · P50 · P90에 해당) |
| 경쟁사 수 | 5곳(직접 경쟁 3~4곳, 대체재 1~2곳) |
| 조사 자료 기간 | 최근 2년. 2년 넘은 자료는 날짜를 밝힘 |
| 웹 검색 | 단계마다 3~6번, 전체 45번 안쪽. 한도에 걸리면 검색 대신 이미 찾은 출처 주소를 직접 열어 확인함 |
| 고객 데이터가 없을 때 | 3단계는 질문지 · 설문지만 만들고, 페르소나는 공개 자료로 세운 「가설 페르소나」 2~3명으로 표시 |
| 리뷰 데이터가 없을 때 | 4단계는 공개 글(커뮤니티 · 기사 · 앱 마켓 리뷰 화면)에서 불만 · 요구 10~20건을 모아 출처와 함께 분석하고, 표본이 작다고 밝힘 |
| 결론 | 진행 · 조건부 진행 · 보류 가운데 하나와 이유 세 줄 |

## 진행 순서

원 스킬은 Skill 도구로 원래 이름(예: `market-sizing`)을 불러 쓰고, 입력 요약을 함께 넘깁니다. Skill 도구로 부를 수 없거나 하위 에이전트로 돌릴 때는 `~/.claude/skills/<이름>/SKILL.md`를 읽고 그 지시대로 합니다. 원 스킬의 분석 순서와 출력 틀은 그대로 따르고, 이 파일은 입력 · 한국 자료 · 저장 위치 · 표시 규칙만 정합니다.

### 0단계: 조사 계획서

- 아이디어를 한 문단으로 정리합니다: 누구에게(고객), 무엇을(제품 · 서비스), 어떻게(방식 · 채널), 돈은 어떻게(가격 · 수익 구조), 어디서 · 언제.
- 원 스킬들이 필요로 하는 입력을 여기서 한 번에 정합니다: 이 조사로 내릴 결정, 대상 고객 · 세그먼트, 알려진 경쟁사 · 대안, 가진 자료(인터뷰 · 설문 · 리뷰 파일), 예상 단가 · 고정비 · 변동비, 회사 역량과 제약.
- 예상 단가는 과금 단위(1인당 · 팀당 · 건당)와 함께 정합니다. 1단계 상향식 계산은 이 단가를 쓰고, 8단계에서 가격 티어를 정하면 그 가격으로 다시 계산합니다(8단계 참고).
- 핵심이 빠졌고 사용자가 바로 답할 수 있는 대화이면 한 번만 묻습니다(최대 3개). 사용자가 「알아서」라고 하거나, 빠진 것이 없거나, 하위 에이전트 · 예약 실행처럼 물을 수 없으면 묻지 않고 합리적인 값을 `[가정]`으로 적어 바로 진행합니다.
- 조사 질문 5~7개를 정합니다(단계마다 답할 질문).
- 사건 폴더를 만듭니다: 작업 폴더 아래 `plan10/YYYYMMDD-<영문 짧은 이름>/`. 작업 폴더 이름이 이미 `plan10`이면 그 아래에 `plan10`을 또 만들지 않고, 바로 `YYYYMMDD-<영문 짧은 이름>/`을 만듭니다. 단계 결과는 `00-plan.md`부터 `10-risk.md`까지 이 폴더에 두고, 한국 자료 조회 결과(JSON)는 `data/`에, 출처 원장은 `ledger.md`에 둡니다.

### 1단계: 시장 · 거시 환경

1. **한국 통계를 먼저 찾습니다**(k-skill `kosis-stats`). 쓰는 법은 `vendor/k-skill/kosis-stats/instruction.md`에 있습니다.
   - instruction.md의 예시는 `npx -y @nomadamas/k-skill@0 exec <스킬> scripts/<파일> -- <인자>` 꼴입니다. 이 스킬셋은 npx를 쓰지 않으므로 `PYTHONUTF8=1 python $K/<스킬>/scripts/<파일> <인자>`로 바꿔 실행합니다. `--` 뒤의 인자는 그대로 씁니다.
   ```bash
   K=~/.claude/skills/dplanner-plan10/vendor/k-skill
   KS="$K/kosis-stats/scripts/run_kosis_stats.py"
   PYTHONUTF8=1 python $KS search --query "<시장을 나타내는 낱말>" --text          # 통계표 찾기
   PYTHONUTF8=1 python $KS meta --org-id <기관> --table-id <표> --meta-type ITM --json   # 항목 · 분류 · 단위
   PYTHONUTF8=1 python $KS explain --org-id <기관> --table-id <표> --text      # 조사 주기 확인
   PYTHONUTF8=1 python $KS data --org-id <기관> --table-id <표> --prd-se Y --start 2024 --end 2024 \
     --itm-id ALL --obj-l 1=ALL --json > "<사건 폴더>/data/kosis-<표>.json"      # 자료 받기
   ```
   - 검색으로 통계표(orgId · tblId)를 찾은 뒤 메타 · 자료를 받아 `data/kosis-*.json`으로 저장합니다. 고객 수 · 사업체 수 · 가구 수처럼 상향식 계산의 바탕이 되는 숫자를 고릅니다.
   - 수록 주기(`--prd-se`)는 `M` · `Q` · `S` · `Y` · `F` · `IR`만 받습니다. 반기 표는 `S`에 `YYYY01`(상반기) · `YYYY02`(하반기) 형식이고, 5년마다 하는 총조사는 연 단위로 보여도 `F`입니다. 결과 없음(코드 30)이 나오면 먼저 주기를 `explain`으로 확인합니다.
   - 분류 값 여러 개는 `--obj-l "1=00+11+23+31"`처럼 `+`로 이어 한 번에 받습니다. 조회 횟수가 줄어듭니다.
   - 잘못된 요청 변수(코드 21)가 나오면 그 표의 `meta`로 항목 · 분류 코드를 다시 확인합니다. 이름이 비슷한 표(예: 연도만 다른 표)라도 코드가 다를 수 있습니다.
2. **원/달러 환율은 늘 받습니다**(지킬 원칙 3). 경쟁사 · API 가격이 달러로 나오는 경우가 많기 때문입니다. k-skill `bok-ecos-stats`로 한국은행 자료를 받고(키 없이 한 번에 10행, `vendor/k-skill/bok-ecos-stats/instruction.md`), 금리 · 물가가 필요하면 같은 도구로 함께 받습니다.
   ```bash
   PYTHONUTF8=1 python $K/bok-ecos-stats/scripts/bok_ecos.py search --alias 원달러환율 --start <YYYYMMDD> --end <YYYYMMDD> --text
   ```
   - 키 없이 쓰는 데모 키(`sample`)는 앞에서부터 10행만 줍니다. 그래서 긴 기간을 부르면 최근 값이 빠집니다(예: 일별 기준금리를 연초부터 오늘까지 부르면 1월 초 값만 옴). 최근 값이 필요하면 최근 기간만 부르고(일별 자료면 끝 날짜에서 열흘 안쪽), 받은 마지막 행의 날짜가 원하는 시점인지 확인합니다.
3. **`market-sizing`**(pm-skills)을 부릅니다. 넘길 것: 시장 정의, 지역 한국, 통화 원화, SOM 3년, 1번에서 받은 통계와 출처 번호. 하향식과 상향식을 모두 계산하게 하고, 두 결과가 크게 다르면 이유를 적게 합니다. 계산 방법을 더 볼 때는 `market-sizing-analysis`(wshobson)의 `references/details.md`를 참고합니다.
   - 두 결과가 크게 다르면 둘 다 TAM 표에 둡니다. 작은 쪽을 기본 TAM으로 삼아 SAM · SOM을 계산하고, 작은 쪽을 고른 이유를 한 줄로 적습니다.
4. **`pestle-analysis`**(pm-skills)를 부릅니다. 한국 기준으로 쓰게 하고, 원 스킬의 GDPR · CCPA 같은 해외 법 예시 대신 국내 법령을 떠올리게 합니다. 법적 요인은 10단계에서 법령 원문으로 다시 확인합니다.
5. `01-market.md`: 시장 정의, TAM · SAM · SOM 표(값마다 출처 번호), PEST 요약. 시장 정의와 침투율 가정에는 `[확인 필요]`를 붙입니다.
   - PEST 요약은 `pestle-analysis`의 6범주를 네 칸으로 합칩니다: 정치 · 법, 경제, 사회, 기술 · 환경. 보고서의 PEST 칸(`.tiles.two`)도 이 이름과 순서로 씁니다.

### 2단계: 트렌드 · 수요

- 전담 스킬이 없어서 이 파일이 직접 합니다.
- 웹 검색으로 최근 2년의 수요 신호(보도 · 공식 보고서 · 시장 조사 발표)를 찾고, 1단계 KOSIS 통계표의 시계열(증가율)을 함께 봅니다.
- 네이버 검색 결과는 쓰지 않습니다(지킬 원칙 4). 사용자가 데이터랩 · 구글 트렌드에서 내려받은 파일을 주면 읽어서 넣습니다.
- `02-trend.md`: 수요 신호 표(신호 · 방향 · 크기 · 출처 번호 · 자료 날짜), 몰리는 시기, 한계(검색량 실제 수치가 없으면 없다고 적음).

### 3단계: 고객 조사

- **`interview-script`**(pm-skills)로 인터뷰 질문지를 만들고, **`survey-design`**(pm-skills)으로 설문지를 만듭니다. 둘 다 0단계의 「내릴 결정」에서 출발하게 합니다. 영어 예문은 한국어 존댓말 질문으로 바꿉니다.
- 사용자가 인터뷰 · 설문 · 피드백 파일을 줬으면 **`user-personas`**(pm-skills)로 페르소나 3명을 만듭니다. 자료가 없으면 공개 자료로 세운 「가설 페르소나」 2~3명을 쓰고, 인터뷰 전 가설이라고 표시합니다.
- `03-customer.md`: 페르소나(또는 가설 페르소나), 인터뷰 질문지, 설문지. 참여자 모집과 인터뷰 진행은 사람이 합니다(`[확인 필요]`).

### 4단계: VOC · 리뷰

- 사용자가 리뷰 · 피드백 파일을 줬으면 그 파일을, 없으면 기본값대로 공개 글 10~20건을 모아(주소 · 날짜와 함께) **`sentiment-analysis`**(pm-skills)에 넘깁니다.
- 경쟁 앱 리뷰를 한꺼번에 내려받는 공식 경로는 없습니다. 많은 양이 필요하면 사용자에게 수집 방법(앱 마켓 약관 확인)을 알리고 멈춥니다.
- 브라우저 도구가 없어 앱 마켓 리뷰 화면을 읽지 못하면 공개 글(커뮤니티) · 기사로 대신하고, 표본 한계에 최근 2년 글 수와 그보다 오래된 글 수(날짜가 없는 글은 따로)를 적습니다.
- `04-voc.md`: 불만 · 요구 빈도표, 대표 의견(원문을 옮기지 않고 뜻을 한 줄로 요약, 출처 번호), 세그먼트별 감정 점수, 표본 한계. 표본 한계에 적는 건수(예: 2년보다 오래된 글 수)는 표의 날짜 칸으로 다시 세어 적습니다. 커뮤니티 글 · 리뷰 원문은 저작권이 있으므로 그대로 옮기지 않습니다.

### 5단계: 경쟁사

- **`competitor-analysis`**(pm-skills)로 경쟁사 5곳을 찾고 강약점 · 사업 모델 · 가격 · 차별화 기회를 정리합니다. 가격은 각 회사의 공식 가격 안내 화면에서 확인한 값만 쓰고, 확인 날짜를 적습니다. 브라우저 도구(Claude in Chrome · Playwright MCP 등)가 연결되어 있으면 가격 안내 화면을 직접 열어 확인하고, 없으면 웹 페이지 읽기 도구로 읽습니다.
- 공식 화면에 가격이 없으면(영업 문의, 다른 요금제에 포함, 표기 없음) 가격 칸에 「공개 안 함(문의)」 · 「○○ 요금제에 포함」처럼 그대로 적고 출처를 붙입니다. 가격을 짐작해 채우지 않고, 가격대 계산에서도 빼며 뺐다는 사실을 표 아래에 적습니다. 기사 · 판매처에 나온 가격은 날짜와 출처를 붙여 참고로만 씁니다.
- 화면이 스크립트로 그려져 웹 페이지 읽기 도구에 가격이 보이지 않으면, 브라우저 도구가 연결되어 있을 때만 그 화면을 열어 확인합니다. 브라우저 도구가 없으면 「화면에서 확인하지 못함」으로 적고 가격대 계산에서 뺍니다. 사이트가 화면을 그릴 때 안에서 부르는 주소를 직접 부르지 않습니다(이용 약관 · 차단 문제).
- 가격대는 공식 가격을 확인한 곳만으로 잡습니다. 과금 단위가 서로 다르면(1팩 · 1개 · 월 구독) 한 범위로 묶지 않고, 우리 과금 단위로 바꾼 값을 함께 적습니다.
- 공식 가격을 확인한 곳이 2곳 이하이면 보고서의 경쟁사 가격대 카드 설명에 「n곳 기준」을 적습니다. 판매처(오픈마켓 · 쇼핑몰) 화면에서 본 가격은 공식 가격과 구분해 「판매처 가격」으로 적습니다.
- **`porters-five-forces`**(pm-skills)로 다섯 가지 힘을 봅니다. 결과는 힘마다 1~5점 표로 정리합니다(wshobson `competitive-landscape`의 참조 파일 표 형식).
- `05-competitors.md`: 경쟁사 비교표(이름 · 대상 · 핵심 기능 · 가격(원) · 출처 번호 · 확인 날짜), 다섯 가지 힘 표, 차별화 기회.

### 6단계: 종합 · 포지셔닝

- **`swot-analysis`**(pm-skills)에 1~5단계 결과를 넘겨 SWOT을 만듭니다. 강점 · 약점은 회사 역량(0단계)에서, 기회 · 위협은 1~5단계 근거에서 가져오고, 항목마다 근거 단계를 적습니다.
- **`competitive-landscape`**(wshobson)로 포지셔닝 맵(두 축)과 포지셔닝 문장을 만듭니다. 영어 어순 틀(For · Who · Unlike)은 한국어 문장으로 새로 짭니다.
- 3C(고객 · 경쟁사 · 자사)와 STP(시장 나누기 · 표적 고르기 · 위치 정하기)는 전용 스킬이 없어서 이 파일이 표로 정리합니다.
- `06-synthesis.md`: 3C 표, SWOT 표, STP, 포지셔닝 맵 좌표(축 이름, 회사별 위치 1~10). 표적 고객 선택에는 `[확인 필요]`를 붙입니다.

### 7단계: 문제 정의 · 가치 제안 · 가설

- **`value-proposition`**(pm-skills)으로 6칸 가치 제안(누구 · 왜 · 이전 · 방법 · 이후 · 대안)과 가치 제안문을 만듭니다. 포지셔닝 문장은 6단계에서 만든 것을 그대로 쓰고 새로 만들지 않습니다.
- **`identify-assumptions-new`**(pm-skills)로 8범주 위험 가정을 뽑고, 가정마다 확신도와 검증 방법 · 성공 기준을 적습니다.
- `07-problem.md`: 문제 진술 한 문장, 가치 제안문, 가설 표(가설 · 범주 · 확신도 · 검증 방법 · 성공 기준). 어떤 문제를 풀지는 사람이 정합니다(`[확인 필요]`).

### 8단계: 수익모델 · 가격

- **`monetization-strategy`**(pm-skills)로 수익 모델 3~5개를 비교하고 하나를 고릅니다.
- **`pricing-strategy`**(pm-skills)로 고른 모델의 가격 티어 2~4개를 정합니다. 5단계 경쟁사 가격(원)을 기준으로 삼고, 지불 의사 확인용 가격 민감도 설문 문항(Van Westendorp 네 문항)을 함께 만듭니다.
- **`lean-canvas`**(pm-skills)로 9칸을 한 장에 정리합니다.
- **1단계 금액을 다시 계산합니다.** 0단계의 예상 단가와 여기서 정한 가격(과금 단위를 1단계와 같게 환산)이 다르면, 정한 가격으로 SAM · SOM을 다시 계산합니다. 두 값을 `08-revenue.md`에 함께 적고, 보고서의 시장 규모 카드와 9단계 재무는 다시 계산한 값을 씁니다.
- `08-revenue.md`: 수익 모델 비교표, 가격 티어 표(티어 · 가격 · 대상 · 포함 기능 · 근거), 린 캔버스, 다시 계산한 SAM · SOM.

### 9단계: 사업성 · 재무

- **`startup-financial-modeling`**(wshobson)으로 3년 매출 · 비용 구조와 세 시나리오를 세웁니다. 가정값(고객 수 증가 · 유지율 · 가격 · 비용)은 모두 표에 모으고 출처 번호나 `[가정]`을 붙입니다. 해지율은 매달 활성 고객의 같은 비율이 빠지는 단순 모형을 기본으로 씁니다.
- 1단계와 연결합니다: 기본 시나리오의 36개월 차 활성 고객 수가 1단계 SOM의 고객 수(8단계에서 다시 계산한 값)와 맞도록 첫 달 신규 고객 수를 거꾸로 계산하고, 그 방법을 `09-finance.md`에 적습니다. SOM(3년 차 말 기준 연간 환산 매출)과 3년 차 매출(그해 합계)은 기준이 달라 값이 다르다는 점도 한 줄로 적습니다.
- 단위 경제는 **`startup-metrics-framework`**(wshobson)의 `references/universal-and-saas-metrics.md` 공식으로 계산합니다. 월 순소진액은 「월 비용 - 월 매출」입니다(`startup-financial-modeling` 본문의 「Monthly Burn = Monthly Revenue - Monthly Expenses」는 부호가 반대라 쓰지 않습니다).
- **손익분기는 이 파일이 계산합니다**(원 스킬에 계산 절이 없음).
  - 손익분기 판매량 = 고정비 ÷ (단가 - 단위당 변동비)
  - 손익분기 매출 = 고정비 ÷ 공헌이익률
  - 기본 시나리오에서 월 이익이 처음 0을 넘는 달과, 누적 이익이 0을 넘는 달
  - 월 이익이 흑자로 돌아선 뒤 다시 적자가 되면(예: 해마다 고정비가 오를 때) 「흑자를 이어 가기 시작한 달」(그달부터 계산 끝까지 월 이익이 계속 0을 넘는 첫 달)도 함께 적습니다.
  - 36개월 안에 0을 넘지 않으면 3년 차 조건(가격 · 고객 증가율 · 비용)을 그대로 이어 최대 120개월까지 계산하고, 「n개월 차(37개월 차부터는 3년 차 조건을 이어 간 [추정])」로 적습니다. 120개월 안에도 없으면 「120개월 안에 없음」으로 적습니다. 그래프에서는 37개월 차부터의 구간을 다른 배경색으로 칠하고 그 뜻을 적습니다.
  - 이어 간 구간의 활성 고객 수는 1단계 SAM의 고객 수를 넘지 않게 두고, 120개월 차 활성 고객이 SAM 고객 수의 몇 %인지 함께 적습니다.
  - 필요 자금은 누적 이익이 가장 낮은 값(누적 최저점)으로 계산하고, 여유 기간을 몇 달로 잡았는지 함께 적습니다.
- 민감도: 가격 ±20%, 고객 증가율 ±20%일 때 손익분기 달이 어떻게 바뀌는지 표로 봅니다. 가격 ±20%는 가격만 바꾸고 원가 · 배송비 같은 변동비 금액과 수요는 그대로 둔 값이고, 고객 증가율 ±20%는 매달 새로 들어오는 고객 수를 0.8배 · 1.2배로 한 값입니다. 가격 ±20%에서 결제 수수료처럼 판매가의 %로 둔 변동비는 바뀐 가격에 같은 비율을 곱합니다. 원가는 판매가의 %로 정했어도 기본 가격일 때의 금액으로 바꿔 그대로 둡니다. 이 정의를 표 아래에 적습니다.
- `09-finance.md`와 `09-finance.csv`(엑셀로 열 수 있는 가정 · 3년 표): 가정표, 시나리오별 3년 표, CAC · LTV · 회수 기간, 손익분기(판매량 · 매출 · 도달 달), 민감도 표. 계산한 값에는 `[추정]`과 계산식을 붙입니다.

### 10단계: 리스크 · 규제

1. **한국 법령을 원문으로 확인합니다**(k-skill `korean-law-search`). 쓰는 법은 `vendor/k-skill/korean-law-search/instruction.md`에 있습니다.
   ```bash
   curl -fsS --get https://k-skill-proxy.nomadamas.org/v1/korean-law/search \
     --data-urlencode target=law --data-urlencode query="<법령 이름이나 낱말>"
   ```
   찾은 법령은 검색 결과의 법령일련번호(MST)로 상세 조회를 해서 조문을 받아 `data/law-*.json`으로 저장합니다. 판례 · 해석례가 필요하면 instruction.md에 적힌 다른 target(`prec` · `expc`)을 씁니다. Windows PowerShell에서는 `curl`이 다른 명령이라 Git Bash에서 실행합니다.
   ```bash
   curl -fsS --get https://k-skill-proxy.nomadamas.org/v1/korean-law/detail \
     --data-urlencode target=law --data-urlencode MST=<법령일련번호> > "<사건 폴더>/data/law-<이름>.json"
   ```
   - 시설 · 판매 방법 · 수수료 같은 세부 기준은 조문 본문이 아니라 시행령 · 시행규칙의 별표에 있는 경우가 많습니다. 낱말을 찾을 때 응답의 조문(`법령.조문`)뿐 아니라 별표(`법령.별표`)까지 봅니다.
   - 상세 응답은 시행규칙처럼 별표가 많은 법령이면 1MB를 넘기도 합니다. 낱말이 든 조문 · 별표는 아래 명령으로 찾습니다. 조문(`법령.조문.조문단위`)은 항 · 호 · 목까지, 별표(`법령.별표.별표단위`)는 서식까지 보고, 공백 · 줄바꿈을 지운 뒤 비교해 별표의 고정 폭 줄에서 쪼개진 낱말도 찾습니다. 첫 줄의 `if 1:`은 목록의 들여쓰기가 남은 채로 붙여 넣어도 돌아가게 합니다.
     ```bash
     python -I -X utf8 -c "if 1:
       import json, sys
       law = json.load(open(sys.argv[1], encoding='utf-8'))['법령']
       word = ''.join(sys.argv[2].split())
       def flat(x):
           if isinstance(x, list): return ''.join(map(flat, x))
           if isinstance(x, dict): return ''.join(flat(v) for k, v in x.items() if k.endswith('내용') or k in ('항', '호', '목'))
           return x if isinstance(x, str) else ''
       for part in ('조문', '별표'):
           units = (law.get(part) or {}).get(part + '단위') or []
           for u in units if isinstance(units, list) else [units]:
               t = ''.join(flat(u).split())
               i = t.find(word)
               if i >= 0: print(u.get('별표구분', part), u.get(part + '번호'), u.get(part + '가지번호') or '', u.get(part + '제목', '').strip(), t.count(word), '|', t[max(0, i - 30):i + 60])
     " "<사건 폴더>/data/law-<이름>.json" "<낱말>"
     ```
     찾은 곳마다 한 줄에 구분(조문 · 별표 · 서식), 번호, 가지번호, 제목, 나온 횟수, 처음 나온 자리의 앞뒤 글이 나옵니다. 번호는 응답 그대로라 별표 17은 `0017 00`, 제4조의2는 `4 2`로 나옵니다. 아무것도 나오지 않으면 낱말을 줄여 다시 찾습니다(예: 「수송포장」 → 「수송」).
   - 판례 검색(`target=prec`)은 사건명에서 찾습니다. 낱말을 이어 붙인 검색어(예: 「대화 녹음 통신비밀보호법」)가 0건이면, 죄명 · 사건명(예: 「통신비밀보호법위반」)이나 핵심 낱말 하나(예: 「녹음」)로 다시 찾습니다.
2. **`pre-mortem`**(pm-skills)으로 「1년 뒤 이 사업이 실패했다」고 가정하고 위험을 Tigers(진짜 위험) · Paper Tigers(부풀려진 걱정) · Elephants(말하지 않던 걱정)로 나눕니다. 원 스킬의 「14일 뒤 출시」 가정은 기획 단계에 맞게 1년으로 바꿉니다. 7단계의 가설 표를 함께 넘깁니다.
3. `10-risk.md`: 규제 표(법령 · 조문 · 무엇에 걸리는지 · 대응 · 출처 번호 · 확인 날짜), 프리모템 표(위험 · 분류 · 긴급도 · 대응). 법률 해석에는 `[확인 필요]`를 붙이고 「전문가 확인이 필요하다」고 적습니다.

### 끝: 보고서

1. **결론**을 정합니다: 진행 · 조건부 진행 · 보류 가운데 하나, 이유 세 줄(근거 단계 표시), 조건(조건부 진행이면), 다음 할 일 5개(인터뷰 · 설문 · 가격 시험처럼 사람이 할 일과, MVP 범위 · PRD 같은 다음 단계).
2. **`ledger.md`**: 출처 원장 전체. 보고서에 나온 출처 번호가 모두 원장에 있는지, 원장 번호가 모두 실제 주소를 가리키는지 확인합니다.
   - 주소가 열리는지는 `curl -sL -o /dev/null -w '%{http_code}' "<주소>"`로 상태 코드를 봅니다. 403 · 410 · 429처럼 자동 접속이 막히면 웹 페이지 읽기 도구로 열어 확인합니다.
   - Windows에서 만든 주소 목록 파일은 줄 끝의 `\r` 때문에 상태 코드가 모두 `000`으로 나올 수 있습니다. 목록을 읽기 전에 `tr -d '\r'`로 지웁니다.
   - 200이 나와도 차단 · 로그인 화면일 수 있습니다. 숫자를 가져온 출처는 그 페이지 내용에 그 숫자가 실제로 있는지 함께 확인합니다.
3. **`report.html`**: 아래 「보고서 HTML 틀」로 만듭니다. 같은 내용을 `summary.md`로도 저장합니다. 두 파일의 숫자 · 결론은 같아야 하므로, 보고서를 고치면 `summary.md`도 함께 고칩니다.
4. `~/.claude/skills/dplanner-multi/SKILL.md`가 있으면, 이 보고서를 멀티 기획 검토 스킬셋(`dplanner-multi`)에 넣어 AI 회의 · 기획 법정으로 한 번 더 검토할 수 있다고 한 줄로 알립니다. 없으면 이 안내를 하지 않습니다.
5. 마지막 답변은 짧게 씁니다: 결론, 이유 세 줄, 사람이 확인할 것, 보고서 위치.

- 하위 에이전트로 돌려서 보고서 형식의 `.md` 파일 쓰기가 막히면, `report.html`처럼 쓸 수 있는 파일만 저장하고 나머지 내용은 답변에 붙여 돌려줍니다. 부모 세션이 그 답변을 받아 저장합니다.
- 클로드 앱처럼 파일을 쓸 수 없는 곳에서는 HTML(또는 아티팩트)로 보여 주고 내려받을 수 있게 합니다.

## 보고서 HTML 틀

`{ }` 부분을 채웁니다. 스크립트를 쓰지 않으므로 인터넷이 없어도 그대로 보입니다. 글꼴(페이퍼로지)만 인터넷에서 받고, 인터넷이 없으면 컴퓨터의 기본 글꼴로 보입니다. 그래프(손익분기 · 포지셔닝 맵)는 계산한 값으로 SVG를 직접 그립니다.

화면은 단순하게 둡니다. 아래 규칙은 그 방법입니다.

- `<style>`은 틀에 적힌 그대로 복사하고 바꾸지 않습니다. 색은 `<style>`의 변수와 클래스만 씁니다. 새 색 · 그라데이션 · 배경 그림 · 이모지 · 아이콘 그림을 더하지 않습니다(완료 표시의 체크는 틀에 들어 있습니다).
- 바탕은 연한 회색이고, 내용은 흰 카드(`.card`)에 담습니다. 단계마다 카드 하나를 씁니다.
- 파란색은 「우리」 · 「완료」와 길잡이에만 씁니다: 10단계 결과의 완료 표시, 포지셔닝 맵의 우리 점, 손익분기 그래프의 기본 시나리오 선과 손익분기 점, 「확인 필요」 칩, 출처 번호 링크, 단계 번호. 표의 우리 줄(`<tr class="ours">`)은 진한 굵은 글자로 구분합니다.
- 결론 색(진행 초록 · 조건부 진행 주황 · 보류 빨강)은 결론 배지 하나에만 씁니다.
- 큰 숫자는 「한눈에 보기」 카드(두 줄 두 칸)에만 하나씩 둡니다(`.num`). 본문 숫자는 보통 글자로 씁니다.
- 경쟁사 가격대 카드: 경쟁사들의 과금 단위가 같으면 공식 가격의 최저~최고를 큰 숫자로 씁니다. 단위가 다르면 5단계에서 우리 과금 단위로 바꾼 값의 범위를 큰 숫자로 쓰고 `추정` 칩을 붙입니다. 공식 가격의 원래 범위와 몇 곳 기준인지는 설명 줄에 적습니다.
- 칸 묶음: 네 칸(PEST · SWOT)은 `.tiles.two`(두 줄 두 칸), 린 캔버스 아홉 칸은 `.tiles.three`, 그 밖은 `.tiles`를 씁니다. PEST 네 칸은 PESTLE 6범주를 합친 정치 · 법, 경제, 사회, 기술 · 환경입니다(1단계 5번). `.reasons` · `.todo` · `.steps`의 칸 안 글은 `<span>`으로 감쌉니다. 칩이 들어가도 줄이 깨지지 않습니다.
- 단계 카드는 그 단계의 결론 한 문장(`.lead`)으로 시작하고, 그 아래에 표 · 목록 · 그래프를 둡니다. 한 문단은 세 문장 안쪽으로 씁니다.
- 10단계 결과(`.steps`)의 단계 이름은 틀에 적힌 글자를 그대로 쓰고, 결과는 한 줄(40자 안쪽)로 씁니다.
- 표시는 글자 칩으로 씁니다: `<span class="t">가정</span>` · `<span class="t">추정</span>` · `<span class="t chk">확인 필요</span>`. HTML에서는 대괄호(`[가정]`)를 쓰지 않습니다. md 파일에서는 대괄호를 그대로 씁니다.
- 출처 번호는 `<a class="src" href="#s3">S3</a>`로 씁니다. 출처 원장의 같은 번호 줄(`<tr id="s3">`)에 기관 이름과 주소를 둡니다. 주소 전체는 원장의 「주소」 칸에만 씁니다.
- 표는 모두 `<div class="tw">`로 감쌉니다. 휴대폰처럼 좁은 화면에서도 본문이 옆으로 넘치지 않고 표만 가로로 밀어 볼 수 있습니다. 숫자 열은 `class="n"`으로 오른쪽에 맞춥니다.
- 그래프는 틀의 `figure.chart` 모양을 따릅니다. 선 · 점 · 글자 · 배경은 클래스(`base` · `opt` · `con` · `zero` · `grid` · `tick` · `lbl` · `dot` · `rival` · `ours` · `frame` · `axis` · `ext`)로 색을 받습니다.
- 손익분기 그래프: 데이터는 x=64~760 안에 그려 마지막 눈금 글자가 그림 밖으로 나가지 않게 합니다. 가로 범위는 손익분기 달이 보이게 잡고(예: 누적 흑자가 53개월 차면 60개월까지), 그 범위를 그림 설명(`figcaption`)에 적습니다. 세로 범위는 기본 · 보수 시나리오가 잘 보이게 잡습니다. 낙관 선이 그 범위를 넘으면 위 끝에서 잘린 채 두고, 가로 범위 마지막 달의 낙관 값을 그림 설명에 적습니다. 37개월 차부터 3년 차 조건을 이어 간 구간은 `ext` 사각형으로 옅게 칠하고, 그 위에 「37개월 차부터는 3년 차 조건을 이어 간 값」을 `tick` 글자로 적습니다.
- 그래프 이름표는 서로 겹치거나, 선 · 점을 가리거나, 그림(viewBox) 밖으로 나가지 않게 둡니다.
  - 점이 가까우면 이름표를 위아래로 나눠 놓고, 선 이름은 범례(`.legend`)에만 씁니다.
  - 선 위의 점에 붙이는 이름표는 선이 지나가지 않는 쪽에 둡니다. 오른쪽으로 오르는 선이면 점의 왼쪽 위나 오른쪽 아래입니다.
  - 이름표 글자(`lbl` · `rlbl` · `olbl`)에는 틀이 흰 테두리를 줍니다. 선이 지나가도 글자가 읽힙니다.
  - 그린 뒤 이름표마다 상자를 계산합니다. 너비는 한글 · 전각 기호 한 글자에 글자 크기만큼, 영문 소문자 · 숫자는 그 0.55배, 영문 대문자 · 기호(&)는 0.7배, 공백은 0.3배, 「·」은 0.5배, 「~」은 0.6배로 잡습니다. 세로는 기준선(`y`)에서 위로 글자 크기만큼, 아래로 글자 크기의 0.25배까지입니다. 상자끼리 겹치는지, 상자가 선(꺾은선의 각 구간) · 점과 만나는지, 그림 밖으로 나가는지 확인하고 고칩니다. 여유는 2px로 둡니다.
- 손익분기가 36개월 뒤이면 「한눈에 보기」의 손익분기 카드에도 「37개월 차부터는 3년 차 조건을 이어 간 값」과 `추정` 칩을 함께 적습니다.
- 다 만든 뒤 확인합니다: `<style>`이 틀과 같은지, 틀에 없는 색 코드(`#` · `rgb`)를 본문에 썼는지(완료 표시 체크의 `#fff`는 틀에 있음), 출처 번호마다 원장 줄(`id`)이 있는지, `report.html`과 `summary.md`의 숫자 · 결론이 같은지.

```html
<!doctype html>
<html lang="ko">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>기획 조사 10단계 · {아이디어 한 줄}</title>
<style>
  @font-face { font-family:"Paperlogy"; font-weight:400; font-display:swap; src:url("https://cdn.jsdelivr.net/gh/projectnoonnu/2408-3@1.0/Paperlogy-4Regular.woff2") format("woff2"); }
  @font-face { font-family:"Paperlogy"; font-weight:500; font-display:swap; src:url("https://cdn.jsdelivr.net/gh/projectnoonnu/2408-3@1.0/Paperlogy-5Medium.woff2") format("woff2"); }
  @font-face { font-family:"Paperlogy"; font-weight:600; font-display:swap; src:url("https://cdn.jsdelivr.net/gh/projectnoonnu/2408-3@1.0/Paperlogy-6SemiBold.woff2") format("woff2"); }
  @font-face { font-family:"Paperlogy"; font-weight:700; font-display:swap; src:url("https://cdn.jsdelivr.net/gh/projectnoonnu/2408-3@1.0/Paperlogy-7Bold.woff2") format("woff2"); }
  :root { color-scheme:light;
    --canvas:#f4f5f7; --surface:#fff; --well:#f6f7f9;
    --ink:#1d1e22; --text:#45464d; --sub:#7d7e86; --faint:#a9aab2;
    --line:rgba(0,0,0,.06); --line-2:rgba(0,0,0,.1);
    --accent:#3b82f6; --accent-soft:rgba(59,130,246,.1); --accent-text:#2563eb;
    --go:#15803d; --go-soft:rgba(34,197,94,.12); --cond:#b45309; --cond-soft:rgba(245,158,11,.14);
    --hold:#b91c1c; --hold-soft:rgba(239,68,68,.1);
    --shadow:0 0 0 1px rgba(0,0,0,.05), 0 1px 2px rgba(0,0,0,.04), 0 12px 32px -16px rgba(50,50,93,.14);
    --r:16px; --r-sm:10px; }
  * { box-sizing:border-box; }
  body { margin:0; background:var(--canvas); color:var(--text);
    font:400 15px/1.7 "Paperlogy","Pretendard","Apple SD Gothic Neo","Malgun Gothic",system-ui,sans-serif;
    letter-spacing:-.01em; -webkit-font-smoothing:antialiased; word-break:keep-all; overflow-wrap:anywhere; }
  main { max-width:920px; margin:0 auto; padding:56px 20px 80px; }
  a { color:var(--accent-text); text-decoration:none; }
  b, strong { color:var(--ink); font-weight:600; }
  p { margin:10px 0 0; }
  .eyebrow { font-size:13px; font-weight:500; color:var(--sub); }
  h1 { margin:8px 0 0; font-size:30px; line-height:1.35; font-weight:700; color:var(--ink); letter-spacing:-.03em; }
  .idea { margin:12px 0 0; font-size:16px; }
  .toc { display:flex; flex-wrap:wrap; gap:6px 16px; margin:20px 0 0; padding:0; list-style:none; font-size:13px; }
  .toc a { color:var(--sub); } .toc span { color:var(--faint); margin-right:4px; }
  .card { background:var(--surface); border-radius:var(--r); box-shadow:var(--shadow); padding:28px; margin-top:16px; }
  .head { display:flex; align-items:center; gap:10px; flex-wrap:wrap; }
  .label { font-size:13px; font-weight:500; color:var(--sub); }
  .badge { display:inline-flex; align-items:center; height:26px; padding:0 11px; border-radius:999px; font-size:13px; font-weight:600; }
  .badge.go { background:var(--go-soft); color:var(--go); } .badge.cond { background:var(--cond-soft); color:var(--cond); } .badge.hold { background:var(--hold-soft); color:var(--hold); }
  .headline { margin:14px 0 0; font-size:21px; line-height:1.5; font-weight:600; color:var(--ink); letter-spacing:-.02em; }
  .reasons { list-style:none; counter-reset:r; margin:20px 0 0; padding:20px 0 0; border-top:1px solid var(--line); display:grid; gap:12px; }
  .reasons li { counter-increment:r; display:grid; grid-template-columns:24px 1fr; gap:12px; }
  .reasons li::before { content:counter(r); width:24px; height:24px; margin-top:2px; border-radius:999px; background:var(--well); color:var(--sub); font-size:12px; font-weight:600; display:grid; place-items:center; }
  .box { margin-top:16px; padding:16px 18px; border-radius:var(--r-sm); background:var(--well); }
  .box ol, .box ul { margin:6px 0 0; padding-left:20px; } .box li { margin:4px 0; }
  .kpis { display:grid; grid-template-columns:repeat(2,1fr); gap:12px; margin-top:12px; }
  .kpi { background:var(--surface); border-radius:var(--r); box-shadow:var(--shadow); padding:20px; }
  .kpi .num { display:block; margin:8px 0 6px; font-size:30px; line-height:1.2; font-weight:700; color:var(--ink); letter-spacing:-.03em; }
  .kpi .note { margin:0; font-size:13px; line-height:1.55; color:var(--sub); text-align:left; }
  .steps { list-style:none; margin:8px 0 0; padding:0; }
  .steps li { display:grid; grid-template-columns:32px 116px 1fr 20px; gap:12px; align-items:start; padding:12px 0; border-top:1px solid var(--line); }
  .steps li:first-child { border-top:0; }
  .steps .no { padding-top:1px; font-size:13px; font-weight:600; color:var(--faint); font-variant-numeric:tabular-nums; }
  .steps .name { font-weight:600; color:var(--ink); }
  .steps .ok { width:20px; height:20px; margin-top:3px; border-radius:999px; background:var(--accent); display:grid; place-items:center; }
  .steps .ok svg { width:12px; height:12px; }
  .sec { display:flex; align-items:baseline; gap:12px; flex-wrap:wrap; }
  .sec .no { font-size:13px; font-weight:700; color:var(--accent-text); font-variant-numeric:tabular-nums; }
  h2 { margin:0; font-size:20px; line-height:1.4; font-weight:700; color:var(--ink); letter-spacing:-.02em; }
  .sec .by { margin-left:auto; font-size:12px; color:var(--faint); }
  .lead { margin:12px 0 0; font-size:16px; line-height:1.65; font-weight:500; color:var(--ink); }
  h3 { margin:24px 0 0; font-size:15px; font-weight:600; color:var(--ink); }
  ul.list, ol.list { margin:8px 0 0; padding-left:20px; } .list li { margin:4px 0; }
  .t { display:inline-block; margin:0 2px; padding:0 5px; border-radius:5px; background:var(--well); color:var(--sub); font-size:11px; line-height:18px; font-weight:500; vertical-align:1px; white-space:nowrap; }
  .t.chk { background:var(--accent-soft); color:var(--accent-text); }
  a.src { margin-left:2px; font-size:12px; font-weight:600; white-space:nowrap; }
  .tw { overflow-x:auto; -webkit-overflow-scrolling:touch; margin-top:12px; }
  table { width:100%; border-collapse:collapse; font-size:14px; line-height:1.55; }
  th { padding:0 12px 8px 0; border-bottom:1px solid var(--line-2); text-align:left; font-size:12px; font-weight:600; color:var(--sub); white-space:nowrap; }
  td { padding:10px 12px 10px 0; border-bottom:1px solid var(--line); vertical-align:top; }
  th:last-child, td:last-child { padding-right:0; }
  tr:last-child td { border-bottom:0; }
  .n { text-align:right; font-variant-numeric:tabular-nums; white-space:nowrap; }
  tr.ours td { color:var(--ink); font-weight:600; }
  tr:target td { background:var(--accent-soft); }
  td a { word-break:break-all; }
  .tiles { display:grid; grid-template-columns:repeat(auto-fit,minmax(220px,1fr)); gap:10px; margin-top:12px; }
  .tiles.two { grid-template-columns:repeat(2,1fr); } .tiles.three { grid-template-columns:repeat(3,1fr); }
  .tile { padding:14px 16px; border-radius:var(--r-sm); background:var(--well); font-size:14px; line-height:1.6; }
  .tile .label { display:block; margin-bottom:4px; }
  .chart { margin:20px 0 0; }
  .chart svg { display:block; width:100%; height:auto; }
  .chart .grid line { stroke:rgba(0,0,0,.06); }
  .chart .zero { stroke:#c8c9cf; stroke-dasharray:4 4; }
  .chart .tick { fill:#7d7e86; font-size:12px; }
  .chart .base, .chart .opt, .chart .con { fill:none; stroke-linejoin:round; stroke-linecap:round; }
  .chart .base { stroke:#3b82f6; stroke-width:2.5; } .chart .opt { stroke:#93c5fd; stroke-width:2; } .chart .con { stroke:#a9aab2; stroke-width:2; }
  .chart .dot { fill:#3b82f6; stroke:#fff; stroke-width:2; }
  .chart .frame, .chart .ext { fill:#f6f7f9; } .chart .axis { stroke:rgba(0,0,0,.1); }
  .chart .rival { fill:#c4c5cc; } .chart .ours { fill:#3b82f6; stroke:#fff; stroke-width:2; }
  .chart .lbl, .chart .rlbl, .chart .olbl { paint-order:stroke; stroke:#fff; stroke-width:4px; stroke-linejoin:round; }
  .chart .lbl { fill:#1d1e22; font-size:13px; font-weight:600; } .chart .rlbl { fill:#7d7e86; font-size:12px; } .chart .olbl { fill:#2563eb; font-size:13px; font-weight:700; }
  .legend { display:flex; flex-wrap:wrap; gap:16px; margin-top:10px; font-size:12px; color:var(--sub); }
  .legend i { display:inline-block; width:12px; height:3px; margin-right:6px; border-radius:2px; vertical-align:middle; }
  .legend i.base { background:#3b82f6; } .legend i.opt { background:#93c5fd; } .legend i.con { background:#a9aab2; }
  figcaption { margin-top:8px; font-size:12px; color:var(--sub); }
  .todo { list-style:none; margin:8px 0 0; padding:0; }
  .todo li { display:grid; grid-template-columns:18px 1fr; gap:12px; padding:10px 0; border-top:1px solid var(--line); }
  .todo li:first-child { border-top:0; }
  .todo li::before { content:""; width:18px; height:18px; margin-top:3px; border-radius:6px; box-shadow:inset 0 0 0 1.5px var(--line-2); }
  .disclaimer { margin-top:24px; font-size:12px; color:var(--sub); text-align:center; }
  @media (max-width:640px) {
    main { padding:32px 14px 56px; } h1 { font-size:24px; } .card { padding:20px; } .headline { font-size:18px; }
    .steps li { grid-template-columns:24px 1fr 20px; } .steps .no { grid-column:1; grid-row:1; } .steps .name { grid-column:2; grid-row:1; }
    .steps .ok { grid-column:3; grid-row:1; } .steps .res { grid-column:2; grid-row:2; }
    .kpis, .tiles.two, .tiles.three { grid-template-columns:1fr; } .sec .by { margin-left:0; width:100%; }
    .chart { overflow-x:auto; } .chart svg { min-width:600px; }
  }
  @media print { body { background:#fff; } .card, .kpi { box-shadow:none; border:1px solid #e3e4e8; } .card { break-inside:avoid; } }
</style>
</head>
<body>
<main>
  <div class="eyebrow">디플래너 기획 조사 10단계 · {날짜}</div>
  <h1>{아이디어 한 줄}</h1>
  <p class="idea">{아이디어 요약 두 문장 안쪽, 가정 칩}</p>
  <ul class="toc">
    <li><a href="#step0"><span>0</span>조사 계획</a></li><li><a href="#step1"><span>1</span>시장 규모</a></li>
    <li><a href="#step2"><span>2</span>트렌드</a></li><li><a href="#step3"><span>3</span>고객</a></li>
    <li><a href="#step4"><span>4</span>고객 불만</a></li><li><a href="#step5"><span>5</span>경쟁사</a></li>
    <li><a href="#step6"><span>6</span>종합</a></li><li><a href="#step7"><span>7</span>문제 정의</a></li>
    <li><a href="#step8"><span>8</span>수익모델과 가격</a></li><li><a href="#step9"><span>9</span>사업성</a></li>
    <li><a href="#step10"><span>10</span>법과 리스크</a></li><li><a href="#ledger">출처 원장</a></li>
  </ul>

  <div class="card">
    <div class="head"><span class="label">결론</span><span class="badge {go|cond|hold}">{진행 · 조건부 진행 · 보류}</span></div>
    <p class="headline">{결론을 한 문장으로}</p>
    <ol class="reasons">
      <li><span>{이유 1, 근거 단계 표시}</span></li>
      <li><span>{이유 2}</span></li>
      <li><span>{이유 3}</span></li>
    </ol>
    <div class="box"><span class="label">조건</span><ol>{조건부 진행이면 조건 목록. 진행 · 보류면 이 상자를 지움}</ol></div>
  </div>

  <div class="kpis">
    <div class="kpi"><span class="label">시장 규모(SOM, 3년 차)</span><span class="num">{금액}</span><div class="note">{기준 한 줄, 칩, 출처 번호}</div></div>
    <div class="kpi"><span class="label">경쟁사 가격대</span><span class="num">{최저~최고}</span><div class="note">{공식 가격을 확인한 n곳 기준(과금 단위가 다르면 함께 적음), 출처 번호}</div></div>
    <div class="kpi"><span class="label">손익분기</span><span class="num">{n개월 차}</span><div class="note">{기본 시나리오, 추정 칩}</div></div>
    <div class="kpi"><span class="label">가장 큰 위험</span><span class="num">{한 낱말}</span><div class="note">{한 줄, 출처 번호}</div></div>
  </div>

  <div class="card">
    <div class="head"><span class="label">10단계 결과</span></div>
    <ol class="steps">
      <li><span class="no">01</span><span class="name">시장 규모</span><span class="res">{한 줄}</span><span class="ok"><svg viewBox="0 0 12 12" aria-hidden="true"><path d="M2.5 6.3 4.9 8.6 9.5 3.6" fill="none" stroke="#fff" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"/></svg></span></li>
      {02 트렌드 · 03 고객 · 04 고객 불만 · 05 경쟁사 · 06 종합 · 07 문제 정의 · 08 수익모델과 가격 · 09 사업성 · 10 법과 리스크를 같은 모양으로}
    </ol>
  </div>

  <section class="card" id="step0">
    <div class="sec"><span class="no">00</span><h2>조사 계획</h2></div>
    <p class="lead">{내릴 결정 한 문장}</p>
    {고객 가설 · 문제 가설 · 조사 질문 · 범위(ul.list)}
  </section>

  <section class="card" id="step1">
    <div class="sec"><span class="no">01</span><h2>시장 규모</h2><span class="by">kosis-stats · bok-ecos-stats · market-sizing · pestle-analysis</span></div>
    <p class="lead">{이 단계의 결론 한 문장}</p>
    {TAM · SAM · SOM 표(숫자 열은 class="n"), PEST 요약(.tiles.two 네 칸)}
  </section>

  <section class="card" id="step2">
    <div class="sec"><span class="no">02</span><h2>트렌드</h2><span class="by">웹 검색 · kosis-stats</span></div>
    <p class="lead">{결론 한 문장}</p>
    {수요 신호 표, 한계}
  </section>

  <section class="card" id="step3">
    <div class="sec"><span class="no">03</span><h2>고객</h2><span class="by">interview-script · survey-design · user-personas</span></div>
    <p class="lead">{결론 한 문장}</p>
    {페르소나 .tiles, 질문지 · 설문지 요약(전문은 03-customer.md)}
  </section>

  <section class="card" id="step4">
    <div class="sec"><span class="no">04</span><h2>고객 불만</h2><span class="by">sentiment-analysis</span></div>
    <p class="lead">{결론 한 문장}</p>
    {불만 · 요구 빈도표, 표본 한계}
  </section>

  <section class="card" id="step5">
    <div class="sec"><span class="no">05</span><h2>경쟁사</h2><span class="by">competitor-analysis · porters-five-forces</span></div>
    <p class="lead">{결론 한 문장}</p>
    <div class="tw"><table><tr><th>경쟁사</th><th>대상</th><th>핵심 기능</th><th class="n">가격(원)</th><th>출처</th><th>확인 날짜</th></tr>
    {경쟁사 행}
    </table></div>
    {다섯 가지 힘 표, 차별화 기회}
  </section>

  <section class="card" id="step6">
    <div class="sec"><span class="no">06</span><h2>종합</h2><span class="by">swot-analysis · competitive-landscape</span></div>
    <p class="lead">{결론 한 문장}</p>
    {3C 표, SWOT .tiles.two(강점 · 약점 · 기회 · 위협), STP}
    <figure class="chart">
      <svg viewBox="0 0 640 440" role="img" aria-label="포지셔닝 맵">
        <rect class="frame" x="40" y="24" width="560" height="368" rx="12"/>
        <line class="axis" x1="320" x2="320" y1="24" y2="392"/><line class="axis" x1="40" x2="600" y1="208" y2="208"/>
        <text class="tick" x="40" y="418">{가로축 왼쪽 끝}</text><text class="tick" x="600" y="418" text-anchor="end">{가로축 오른쪽 끝}</text>
        <text class="tick" x="328" y="44">{세로축 위 끝}</text><text class="tick" x="328" y="380">{세로축 아래 끝}</text>
        {경쟁사마다: <circle class="rival" cx="{x}" cy="{y}" r="6"/><text class="rlbl" x="{x}" y="{y}">{이름}</text>}
        <circle class="ours" cx="{x}" cy="{y}" r="8"/><text class="olbl" x="{x}" y="{y}">우리</text>
      </svg>
      <figcaption>{축을 정한 근거 한 줄, 출처 번호}</figcaption>
    </figure>
  </section>

  <section class="card" id="step7">
    <div class="sec"><span class="no">07</span><h2>문제 정의</h2><span class="by">value-proposition · identify-assumptions-new</span></div>
    <p class="lead">{문제 진술 한 문장}</p>
    {가치 제안문, 가설 표}
  </section>

  <section class="card" id="step8">
    <div class="sec"><span class="no">08</span><h2>수익모델과 가격</h2><span class="by">monetization-strategy · pricing-strategy · lean-canvas</span></div>
    <p class="lead">{결론 한 문장}</p>
    {수익 모델 비교, 가격 티어 표, 린 캔버스 9칸(.tiles.three)}
  </section>

  <section class="card" id="step9">
    <div class="sec"><span class="no">09</span><h2>사업성</h2><span class="by">startup-financial-modeling · startup-metrics-framework</span></div>
    <p class="lead">{결론 한 문장}</p>
    {가정표, 시나리오별 3년 표, CAC · LTV · 회수 기간}
    <figure class="chart">
      <svg viewBox="0 0 800 340" role="img" aria-label="손익분기 그래프">
        <rect class="ext" x="{37개월 차의 x}" y="16" width="{760까지의 너비}" height="{그래프 아래 끝까지의 높이}"/><text class="tick" x="{37개월 차의 x + 8}" y="34">37개월 차부터는 3년 차 조건을 이어 간 값</text>
        <g class="grid">{가로 눈금선: <line x1="64" x2="760" y1="{y}" y2="{y}"/>}</g>
        <line class="zero" x1="64" x2="760" y1="{0원의 y}" y2="{0원의 y}"/>
        {세로 눈금 글자: <text class="tick" x="56" y="{y}" text-anchor="end" dominant-baseline="middle">{값}</text>}
        {가로 눈금 글자: <text class="tick" x="{x}" y="326" text-anchor="middle">{n}개월</text>}
        <polyline class="con" points="{x,y …}"/><polyline class="opt" points="{x,y …}"/><polyline class="base" points="{x,y …}"/>
        <circle class="dot" cx="{x}" cy="{y}" r="5"/><text class="lbl" x="{x}" y="{y}">{기본 누적 흑자 n개월 차}</text>
      </svg>
      <div class="legend"><span><i class="base"></i>기본</span><span><i class="opt"></i>낙관</span><span><i class="con"></i>보수</span></div>
      <figcaption>{가로 월, 세로 누적 이익(원). 설명 한 줄, 추정 칩}</figcaption>
    </figure>
    {민감도 표와 그 아래 정의 한 줄}
  </section>

  <section class="card" id="step10">
    <div class="sec"><span class="no">10</span><h2>법과 리스크</h2><span class="by">korean-law-search · pre-mortem</span></div>
    <p class="lead">{결론 한 문장}</p>
    {규제 표, 프리모템 표}
  </section>

  <section class="card">
    <div class="sec"><h2>사람이 확인할 것</h2></div>
    {확인 필요 항목 모음(ul.list): 시장 정의 · 가정값 · 표적 고객 · 법률 해석 · 결론}
  </section>

  <section class="card">
    <div class="sec"><h2>다음 할 일</h2></div>
    <ul class="todo"><li><span>{할 일}</span></li>{같은 모양으로 5개}</ul>
  </section>

  <section class="card" id="ledger">
    <div class="sec"><h2>출처 원장</h2></div>
    <div class="tw"><table><tr><th>번호</th><th>내용</th><th>값(단위)</th><th>기관</th><th>주소</th><th>자료 날짜</th><th>확인 날짜</th></tr>
    {원장 행: <tr id="s1"><td>S1</td>…</tr>}
    </table></div>
  </section>

  <section class="card">
    <div class="sec"><h2>이 보고서를 만든 스킬</h2></div>
    {스킬셋 구성 표}
  </section>
  <p class="disclaimer">이 보고서는 기획 검토를 위한 조사 정리이며 사업 · 투자 · 법률 자문이 아닙니다. 가정 · 추정 값은 실제 조사로 확인해야 합니다.</p>
</main>
</body>
</html>
```

## 라이선스와 만든 곳

- pm-skills: phuryn/pm-skills, MIT(Copyright (c) 2026 Pawel Huryn). 원 저장소에서 설치해 그대로 부릅니다.
- startup-business-analyst 스킬 4개: wshobson/agents, MIT(Copyright (c) 2024 Seth Hobson). 원 저장소에서 설치해 그대로 부릅니다.
- kosis-stats · bok-ecos-stats · korean-law-search: NomaDamas/k-skill, MIT(`vendor/k-skill/LICENSE`). 스크립트와 설명서를 원 저장소에서 받아 이 파일이 실행합니다. korean-law-search의 `scripts/amendment/`는 chrisryugj/korean-law-mcp의 MIT 코드이고 고지 파일이 함께 들어 있습니다.
- 디플래너가 만든 부분: 10단계 순서, 단계마다 넘기는 입력, 한국 자료 규칙(지킬 원칙), 출처 원장 · 표시 규칙, 2단계 수요 조사, 3C · STP 표, 손익분기 계산, 보고서 틀. 만든 곳: 디플래너(dplanner@outlook.kr)

## 시험 기록

- 1차(2026-11-16, 고치기 전 판): 맥락 없는 새 클로드 코드 대화(하위 에이전트) 하나에 「이 파일로 스킬 설치하고, 이 아이디어 기획 조사해 줘: 중소기업 팀이 회의 녹음을 올리면 AI가 회의록과 할 일을 정리해 주는 구독 서비스」만 주고 끝까지 돌렸습니다.
  - 걸린 시간: 설치 약 1분 17초, 전체 64분 35초. 웹 검색 16번, 하위 에이전트 0개.
  - 결과: 단계 파일 11개, `09-finance.csv`, `ledger.md`(출처 30개), `report.html`, `summary.md`. 결론은 「조건부 진행」이었습니다.
  - KOSIS(통계표 4개) · 한국은행 ECOS(원/달러 환율) · 법령(법령 3개 전문, 대법원 판례 4건) 조회가 모두 실제 값을 돌려줬습니다.
  - 이 시험에서 나온 고칠 점 16개와 그래프 이름표끼리 겹친 문제를 고쳐 2차 시험 판을 만들었습니다.
- 2차(2026-11-16, 1차 결과로 고친 판): 맥락 없는 새 대화(하위 에이전트) 하나에 「이 파일로 스킬 설치하고, 이 아이디어 기획 조사해 줘: 1인 가구가 앱에서 고른 반찬을 매주 집으로 받아 보는 정기 구독 서비스」만 주고 끝까지 돌렸습니다.
  - 걸린 시간: 설치 약 1분 56초, 전체 70분 32초. 웹 검색 13번, 페이지 열기 25번, 하위 에이전트 0개.
  - 결과: 단계 파일 11개, `09-finance.csv`, `ledger.md`(출처 38개, 주소 38개 모두 HTTP 200), `report.html`, `summary.md`. 결론은 「조건부 진행」이었습니다.
  - KOSIS(통계표 11개) · 한국은행 ECOS(원/달러 환율 · 소비자물가 · 기준금리) · 법령(법령 6개 전문, 대법원 판례 1건) 조회가 모두 실제 값을 돌려줬습니다.
  - 1차 뒤에 고친 곳(설치 명령, 8단계 가격으로 시장 규모 다시 계산, 36개월 뒤 손익분기 표시, 판례 다시 찾기, 이름표끼리 겹침 검사)이 모두 그대로 동작했습니다.
  - 이 시험에서 나온 고칠 점 15개와, 보고서 화면에서 찾은 「손익분기 이름표를 선이 가로지른 문제」를 고쳐 3차 시험 판을 만들었습니다.
- 3차(2026-11-16, 2차 결과로 고친 판, 새 보고서 틀 포함): 2차와 같은 방법으로, 맥락 없는 새 대화(하위 에이전트) 하나에 「이 파일로 스킬 설치하고, 이 아이디어 기획 조사해 줘: 1인 가구가 앱에서 고른 반찬을 매주 집으로 받아 보는 정기 구독 서비스」만 주고 끝까지 돌렸습니다.
  - 걸린 시간: 설치 약 1분 12초, 전체 51분 7초. 웹 검색 17번, 페이지 열기 28번, 하위 에이전트 0개.
  - 결과: 단계 파일 11개, `09-finance.csv`, `ledger.md`(출처 39개, 주소 40개), `report.html`, `summary.md`. 결론은 「조건부 진행」이었습니다.
  - 주소 40개 가운데 38개는 이 파일의 curl 명령으로 HTTP 200이었고, 410 · 403이 나온 2개는 웹 페이지 읽기 도구로 내용을 확인했습니다.
  - KOSIS(통계표 8개) · 한국은행 ECOS(지표 3개: 원/달러 환율 · 소비자물가 · 기준금리) · 법령(법령 8개 전문, 대법원 판례 1건) 조회가 모두 실제 값을 돌려줬습니다.
  - 이 시험에서 나온 고칠 점 15개를 고쳐 지금 판을 만들었습니다. 지금 판은 아직 처음부터 끝까지 시험하지 않았습니다.
- 측정 방법: 단계를 시작할 때와 끝낼 때 `date`를 찍어 시간을 재고, 웹 검색 · 페이지 열기는 도구를 부른 횟수로 셉니다.
- 원 저장소 커밋(가장 최근 시험 때 받은 main 최신. 설치 5번은 이 커밋과 비교합니다)
  - phuryn/pm-skills: `9af7bfd0bc47fdad43c2eaa7a43cd13918e7aaef`(1~3차 모두 같음)
  - wshobson/agents: `9c61ab243def98f72da12abd41cfcf5bcd91af9d`(1~3차 모두 같음)
  - NomaDamas/k-skill: `c41a11703b0ea25b8c5c3c62bd0f06f31997f7f8`(3차). 1차 · 2차 때 받은 `9766d20fb1fe1a5eb1d10ef5ff9872c8d6fc4985`와 비교하면 이 스킬셋이 쓰는 세 폴더와 `LICENSE`는 그대로입니다.
