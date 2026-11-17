---
name: dplanner-insta
description: 디플래너 인스타 자동화 스킬. 인스타그램 운영을 소재 찾기 → 만들기(영상 · 캡션 · 해시태그 · 카드뉴스 · 썸네일) → 업로드 → 자동답글 · 자동DM → 성과관리까지 클로드가 이어서 합니다. "인스타 자동화 세팅해 줘", "이번 주 소재 찾아 줘", "이 주제로 카드뉴스 만들어 올려 줘", "릴스 만들어 올려 줘", "자동DM 세팅해 줘", "성과 리포트 보여 줘" 같은 요청에 씁니다. 처음 쓰면 「세팅」 절대로 한 번 세팅합니다.
---

# 디플래너 인스타 자동화

인스타그램 운영을 다섯 단계로 나눠 클로드가 이어서 합니다. 모든 기능은 인스타그램 공식 기능(메타 개발자 문서의 Instagram API with Instagram Login)과 공식 도구만 씁니다. 비공식 API · 자동 팔로우 · 자동 좋아요는 계정이 제한될 수 있어 쓰지 않습니다.

| 단계 | 하는 일 | 쓰는 것 |
|---|---|---|
| ① 소재 찾기 | 내 채널 주제와 비슷한 뜨는 소재와 근거(링크 · 숫자 · 날짜)를 찾아 정리 | 웹 검색, 깃허브 검색 |
| ② 만들기 | 릴스 영상, 캡션, 해시태그, 카드뉴스, 썸네일(릴스 표지) | 리모션 공식 스킬(영상 · 카드뉴스 · 썸네일), 클로드(글) |
| ③ 업로드 | 릴스 · 카드뉴스 게시(캡션 · 표지 함께) | 인스타그램 공식 게시 기능 |
| ④ 자동답글 · 자동DM | 키워드 댓글에 답글과 DM | 댓글 DM 서비스(소셜비즈 · 매니챗) 또는 공식 기능 |
| ⑤ 성과관리 | 게시물별 조회수 · 도달 · 저장 · 공유 · 좋아요 · 댓글 리포트 | 인스타그램 공식 인사이트 기능 |

## 지킬 것 (먼저 읽음)

- **밖으로 보이는 동작은 사용자에게 먼저 보여 주고 허락을 받습니다.** 게시물 올리기, 댓글 답글 · 숨기기, DM 보내기, 자동DM 켜기가 여기에 들어갑니다. 올리기 전에는 미리보기 파일 · 캡션 · 해시태그를 보여 주고 「올릴까요?」라고 묻습니다.
- **토큰 · 비밀번호는 채팅에 쓰지 않습니다.** 토큰은 사용자가 직접 `~/insta-auto/.secrets/ig_token.txt` 파일에 붙여 넣게 하고, 명령에서 파일로 읽습니다. 화면 · 로그에 토큰을 출력하지 않습니다.
- 로그인 · 앱 권한 허용 · 결제 화면은 사용자가 직접 누릅니다. 클로드는 그 화면을 열고 무엇을 누를지 알려 줍니다.
- 공식 게시 기능은 24시간에 게시물 100개까지입니다(카드뉴스 1개 = 1건). 넘지 않게 `content_publishing_limit`로 확인합니다.
- 숫자 · 근거는 실제로 읽은 값만 씁니다. 지어낸 숫자로 리포트를 채우지 않습니다.

## 세팅 (처음 한 번)

사용자가 이 파일을 주며 「설치해 줘」 · 「세팅해 줘」라고 하면 아래를 차례로 합니다. `~`는 사용자 홈 폴더(Windows는 `C:\Users\<이름>`)이고, 명령은 Bash(Windows는 Git Bash)로 실행합니다. 단계마다 끝나면 한 줄로 알려 줍니다.

1. **스킬 설치**: 이 파일을 요약하거나 고치지 말고 원본 그대로 `~/.claude/skills/dplanner-insta/SKILL.md`로 복사합니다(`mkdir -p ~/.claude/skills/dplanner-insta`).
2. **준비물 확인**: `node --version`(18 이상), `git --version`. 없으면 사용자에게 알리고 허락을 받은 뒤 설치합니다(Windows: `winget install -e --id OpenJS.NodeJS.LTS --scope user`, `winget install -e --id Git.Git --scope user`, macOS: `brew install node git`). 설치한 뒤에는 새 터미널에서 다시 확인합니다.
3. **리모션 공식 스킬 설치**(영상 · 카드뉴스 · 썸네일을 코드로 만듦): `npx skills add remotion-dev/skills`. 리모션은 개인과 직원 3명 이하 회사는 무료이고, 그보다 큰 회사는 회사 라이선스가 필요하다고 사용자에게 알립니다(리모션 공식 라이선스).
4. **작업 폴더 만들기**: `~/insta-auto/`와 아래 파일을 만듭니다.
   ```
   ~/insta-auto/
     CLAUDE.md        # 이 폴더의 지도(아래 내용)
     channel.md       # 채널 주제 · 독자 · 말투 · 고정 해시태그 · 금지어
     topics/          # ① 소재 찾기 결과(날짜별)
     posts/           # ② 게시물마다 폴더(영상 · 카드뉴스 · 썸네일 · caption.txt · post.json)
     reports/         # ⑤ 성과 리포트(날짜별)
     studio/          # 리모션 프로젝트(영상 · 카드뉴스 · 썸네일 템플릿)
     .secrets/        # 토큰(깃에 올리지 않음)
   ```
   `CLAUDE.md`에는 「이 폴더는 인스타 자동화 작업 공간이다. 채널 규칙은 channel.md를 먼저 읽는다. 게시 · 답글 · DM은 사용자 허락 뒤에만 한다. 토큰은 .secrets에서만 읽고 출력하지 않는다」를 적습니다. 그다음 사용자에게 세 가지를 묻고 `channel.md`에 적습니다: ① 채널 주제와 독자, ② 말투(예: 해요체, 이모지 사용 여부), ③ 늘 넣는 해시태그와 쓰지 않을 말.
5. **리모션 프로젝트 준비**: `cd ~/insta-auto && npx create-video@latest`를 실행하고, 템플릿은 빈 템플릿(Blank), 폴더 이름은 `studio`로 고릅니다. 세로 릴스(1080×1920, 30fps), 카드뉴스(1080×1350), 썸네일(1080×1920) 컴포지션을 만들고, `channel.md`의 색 · 글꼴로 템플릿을 하나씩 만듭니다. 템플릿을 만들 때는 리모션 공식 스킬의 규칙을 따릅니다.
6. **인스타그램 계정 연결**(메타 공식 문서 「Instagram API with Instagram Login」 순서)
   1. 인스타그램 계정이 프로페셔널 계정(비즈니스 또는 크리에이터)인지 사용자에게 확인합니다. 아니면 인스타 앱 설정 → 계정 유형 전환을 안내합니다.
   2. https://developers.facebook.com/apps 를 열어 앱 만들기 → 유형 「비즈니스」를 고르게 안내합니다(로그인은 사용자가 함).
   3. 앱 대시보드에서 제품 「Instagram」을 추가하고 「API setup with Instagram login」으로 들어가게 안내합니다.
   4. 「Generate access tokens」에서 사용자의 인스타그램 계정을 추가하고 로그인 · 권한 허용을 사용자가 누릅니다. 권한은 `instagram_business_basic`, `instagram_business_content_publish`, `instagram_business_manage_comments`, `instagram_business_manage_messages`, `instagram_business_manage_insights`입니다.
   5. 대시보드가 만든 토큰(60일짜리)을 사용자가 복사해 `~/insta-auto/.secrets/ig_token.txt`에 붙여 넣게 합니다(채팅에 붙여 넣지 않게 안내). `chmod 600`(Windows는 생략).
   6. 확인: 아래 명령이 `user_id`와 `username`을 돌려주면 연결된 것입니다. `user_id`를 `~/insta-auto/.secrets/ig_id.txt`에 저장합니다.
      ```bash
      TOKEN=$(cat ~/insta-auto/.secrets/ig_token.txt)
      curl -s "https://graph.instagram.com/v27.0/me?fields=user_id,username&access_token=$TOKEN"
      ```
   7. 토큰은 60일 뒤 만료됩니다. 50일쯤에 아래로 늘리고 파일을 새 값으로 바꿉니다(사용자에게 날짜를 알려 둠).
      ```bash
      curl -s "https://graph.instagram.com/refresh_access_token?grant_type=ig_refresh_token&access_token=$TOKEN"
      ```
7. **올릴 파일의 공개 주소 준비**: 공식 게시 기능은 사진 · 영상을 공개 주소에서 가져가므로, 올리는 동안만 파일을 공개 주소에 둡니다. 기본은 깃허브 페이지입니다.
   1. 사용자에게 깃허브 계정이 있는지 묻고, 공개 저장소 `insta-media`를 만들게 안내합니다(또는 `gh repo create insta-media --public`, gh 로그인은 사용자가 함).
   2. 저장소 설정 → Pages → 브랜치 `main`, 폴더 `/`로 켜게 안내합니다. 주소는 `https://<깃허브아이디>.github.io/insta-media/`입니다.
   3. 이 저장소를 `~/insta-auto/media/`에 클론해 둡니다. 올릴 때 파일을 넣고 푸시 → 주소가 열릴 때까지 기다림 → 게시 → 게시가 끝나면 파일을 지우고 다시 푸시합니다.
8. **자동답글 · 자동DM 방식 고르기**(사용자에게 묻기)
   - **A. 댓글 DM 서비스(권장, 처음 쓰는 사람)**: 소셜비즈(https://socialbiz-c.nhndata.com) 또는 매니챗(https://manychat.com). 서비스 가입과 인스타그램 연결은 사용자가 하고, 키워드 · 답글 · DM 문구 · 버튼 링크 등록은 클로드가 브라우저로 돕거나 무엇을 넣을지 정리해 줍니다. 게시 전에 「다음 업로드 게시물」로 등록해 두면 새 게시물 첫 댓글부터 바로 동작합니다.
   - **B. 공식 기능으로 직접**: 클로드가 정해 둔 시간마다 새 댓글을 읽어 키워드가 있으면 공개 답글과 비공개 답장(DM)을 보냅니다(아래 ④). 컴퓨터와 클로드가 켜져 있을 때만 동작합니다.
9. **세팅 끝**: 「세팅이 끝났어요. 이제 '이번 주 소재 찾아 줘'라고 하면 돼요」처럼 다음에 할 말을 알려 줍니다.

## ① 소재 찾기

- `channel.md`의 주제 · 독자를 읽고, 그 주제와 비슷한 최근(기본 2주) 화제를 찾습니다: 웹 검색(뉴스 · 공식 발표), 깃허브 인기 저장소(`https://api.github.com/search/repositories?q=<주제 낱말>+pushed:>YYYY-MM-DD&sort=stars`), 사용자가 알려 준 참고 계정.
- 후보마다 근거를 붙입니다: 출처 링크, 숫자(스타 수 · 조회수 · 발표일)와 확인한 날짜. 숫자는 실제로 읽은 값만 씁니다.
- 결과는 `topics/YYYY-MM-DD.md`에 표(후보 · 왜 지금 뜨는지 · 근거 · 내 채널에 맞는 정도 · 한 줄 기획)로 저장하고 사용자에게 상위 3개를 추천합니다.

## ② 만들기

게시물마다 `posts/YYYY-MM-DD-<짧은이름>/` 폴더를 만들고 아래를 넣습니다. 다 만들면 사용자에게 파일과 글을 보여 주고 고칠 곳을 묻습니다.

- **캡션 · 해시태그**: `channel.md`의 말투로 첫 줄 후킹 → 본문(3~6줄) → 해시태그(고정 + 주제 3~5개)를 `caption.txt`에 씁니다. 인스타 캡션은 2,200자, 해시태그는 30개를 넘지 않습니다.
- **카드뉴스**: 리모션 카드뉴스 컴포지션으로 5~10장을 만듭니다. 장마다 JPEG로 뽑습니다(공식 게시 기능은 사진을 JPEG만 받음).
  ```bash
  cd ~/insta-auto/studio
  npx remotion still CardNews posts/<폴더>/card-01.jpg --props='{"page":1}' --image-format=jpeg
  ```
- **썸네일(릴스 표지)**: 1080×1920 JPEG로 뽑습니다(`--image-format=jpeg`).
- **릴스 영상**: 리모션 공식 스킬 규칙대로 9:16 컴포지션을 만들고 렌더합니다. 사용자가 찍은 영상이 있으면 그 영상에 자막 · 제목을 얹습니다.
  ```bash
  npx remotion render Reel posts/<폴더>/reel.mp4 --codec=h264
  ```
- 다른 사람의 사진 · 영상 · 음악은 쓰지 않습니다. 필요하면 사용자가 가진 파일만 씁니다.

## ③ 업로드 (사용자 허락 뒤)

공통: `BASE=https://graph.instagram.com/v27.0`, `TOKEN`은 파일에서 읽기, `IG=$(cat ~/insta-auto/.secrets/ig_id.txt)`. 파일은 「세팅 7」의 공개 주소에 올려 둔 뒤 그 주소를 씁니다.

1. 남은 한도 확인: `curl -s "$BASE/$IG/content_publishing_limit?fields=quota_usage,config&access_token=$TOKEN"`
2. **릴스**
   ```bash
   curl -s -X POST "$BASE/$IG/media" \
     --data-urlencode "media_type=REELS" \
     --data-urlencode "video_url=https://<아이디>.github.io/insta-media/reel.mp4" \
     --data-urlencode "cover_url=https://<아이디>.github.io/insta-media/thumb.jpg" \
     --data-urlencode "caption@posts/<폴더>/caption.txt" \
     --data-urlencode "share_to_feed=true" \
     --data-urlencode "access_token=$TOKEN"
   # → {"id": "<컨테이너ID>"}
   ```
3. **카드뉴스(여러 장)**: 장마다 `is_carousel_item=true`와 `image_url`로 컨테이너를 만들고(최대 20장), 그 ID들을 쉼표로 이어 `media_type=CAROUSEL`, `children=<ID,ID,...>`, `caption`으로 묶음 컨테이너를 만듭니다.
4. **상태 확인**: `curl -s "$BASE/<컨테이너ID>?fields=status_code&access_token=$TOKEN"` → `FINISHED`가 될 때까지 1분마다, 최대 5분 확인합니다(`ERROR` · `EXPIRED`면 멈추고 알림).
5. **게시**: `curl -s -X POST "$BASE/$IG/media_publish" --data-urlencode "creation_id=<컨테이너ID>" --data-urlencode "access_token=$TOKEN"` → 게시물 ID를 `post.json`에 저장하고, `permalink`를 읽어 사용자에게 알립니다.
6. 공개 주소의 파일을 지우고 푸시합니다.
- 선택: AI로 만든 사실적인 영상 · 음성이면 컨테이너에 `is_ai_generated=true`를 넣으면 「AI 콘텐츠」 표시가 붙습니다(카드뉴스는 묶음 컨테이너에만).

## ④ 자동답글 · 자동DM

- **A(댓글 DM 서비스)**: 새 게시물마다 키워드 · 답글 문구 · DM 문구 · 버튼 링크를 정리해 사용자에게 보여 주고, 허락을 받으면 서비스 화면에서 등록을 돕습니다. 게시 전에 「다음 업로드 게시물」로 등록합니다.
- **B(공식 기능으로 직접, 사용자 허락 뒤 켬)**: 정해 둔 시간마다(예: 10분) 아래를 반복합니다. 같은 댓글에 두 번 보내지 않게 처리한 댓글 ID를 `posts/<폴더>/replied.json`에 적습니다.
  1. 새 댓글 읽기: `curl -s "$BASE/<게시물ID>/comments?fields=id,text,username,timestamp&access_token=$TOKEN"`
  2. 키워드가 있는 댓글에 공개 답글: `curl -s -X POST "$BASE/<댓글ID>/replies" --data-urlencode "message=<답글>" --data-urlencode "access_token=$TOKEN"`
  3. 같은 댓글에 비공개 답장(DM, 댓글 하나에 한 번, 댓글 7일 안):
     ```bash
     curl -s -X POST "$BASE/$IG/messages" -H "Content-Type: application/json" \
       -d '{"recipient":{"comment_id":"<댓글ID>"},"message":{"text":"<DM 문구와 링크>"}}' \
       -H "Authorization: Bearer $TOKEN"
     ```
  - 악성 댓글은 사용자 허락을 받고 숨깁니다: `curl -s -X POST "$BASE/<댓글ID>" --data-urlencode "hide=true" --data-urlencode "access_token=$TOKEN"`

## ⑤ 성과관리

- 게시물마다 인사이트를 읽습니다(공식 인사이트 기능, 권한 `instagram_business_manage_insights`).
  ```bash
  curl -s "$BASE/<게시물ID>/insights?metric=views,reach,saved,shares,likes,comments,total_interactions&access_token=$TOKEN"
  ```
  릴스는 `ig_reels_avg_watch_time`(평균 시청 시간)도 함께 읽습니다. 지표 이름이 바뀌었다는 오류가 나오면 메타 개발자 문서의 Insights 쪽을 열어 지금 이름으로 바꿉니다.
- `reports/YYYY-MM-DD.md`에 표(게시물 · 날짜 · 조회수 · 도달 · 저장 · 공유 · 좋아요 · 댓글)와 한눈에 보이는 그래프(HTML 한 장)를 만들고, 잘된 게시물의 공통점과 다음 소재 제안을 세 줄로 적습니다.
- 「성과 리포트 보여 줘」라고 하면 최근 게시물부터 정리하고, 지난 리포트와 비교합니다.

## 막힐 때

| 상황 | 확인할 것 |
|---|---|
| `/me`가 오류 | 토큰을 다시 붙여 넣었는지, 60일이 지났는지(지났으면 대시보드에서 새로 만들기) |
| 게시가 `ERROR` | 공개 주소가 열리는지(브라우저로 열어 봄), 사진이 JPEG인지, 영상이 세로 9:16 · H.264인지 |
| 인사이트가 권한 오류 | 토큰을 만들 때 `instagram_business_manage_insights`를 허용했는지 |
| DM이 안 감 | 댓글이 7일 안인지, 그 댓글에 이미 보냈는지, 앱에 `instagram_business_manage_messages`가 있는지 |
| 리모션 렌더 실패 | `node --version` 18 이상인지, `npx remotion versions`로 버전이 맞는지 |

출처: 메타 개발자 문서 Instagram Platform(Content Publishing · Instagram API with Instagram Login · Insights · Comment Moderation · Private Replies), 리모션 공식 스킬 `remotion-dev/skills`. 확인 날짜 2026-11-14. 문의: dplanner@outlook.kr
