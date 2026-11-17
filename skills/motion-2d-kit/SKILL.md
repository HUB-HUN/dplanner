---
name: motion-2d-kit
description: 말로 부탁하면 그림 파일 없이 코드만으로 2D 애니메이션 영상을 만들어요. 모션 타이포그래피(글자가 튀어나오고 춤춤), 플로우차트 애니메이션(상자가 차례로 나타나고 선이 그려지고 빛이 흐름), 판타지풍 풍경(셀 셰이딩 하늘 · 뭉게구름 · 부유섬 · 흔들리는 풀 · 반딧불), 게임 타이틀 화면(판타지 풍경 위에 게임 제목 · 메뉴)을 Remotion(React)으로 그리고 mp4로 뽑아요. 2D 애니메이션 · 모션그래픽 · 키네틱 타이포 · 움직이는 플로우차트 · 판타지 배경 영상 · 게임 타이틀 · 로딩 화면 영상을 부탁받으면 이 스킬을 써요.
---

# 2D 모션 키트 (디플래너, 2026-11-05 판)

디플래너가 실제 쇼츠 화면을 만들 때 쓰는 방식이에요. 아래 템플릿 네 개는 실제로 영상으로 뽑아 확인한 코드예요. 사용자의 요청에 맞는 템플릿을 고르고, 문구 · 색 · 길이 · 크기만 바꿔 시작해요.

## 0. 준비 (처음 한 번)

1. Node.js 18 이상과 ffmpeg가 필요해요. 없으면 무엇을 왜 설치하는지 사용자에게 말하고 동의를 받은 뒤 공식 방법으로 설치해요.
2. `npx create-video@latest`로 Remotion 빈 프로젝트를 만들어요.
   - Remotion 라이선스: 개인, 직원 3명 이하 영리 조직, 비영리 단체는 무료예요. 그 밖의 회사는 회사 라이선스가 필요해요(https://www.remotion.dev/license). 사용자에게 한 번 알려요.
3. 한글 글꼴: Pretendard처럼 상업적으로 쓸 수 있는 글꼴(OFL)을 `public/fonts/`에 두고 CSS `@font-face`로 불러와요. 템플릿의 `FONT`에 그 이름을 넣어요.

## 1. 순서

1. 무엇을 만들지 물어요: 종류(타이포 · 플로우차트 · 풍경 · 게임 타이틀 화면 · 섞기), 들어갈 문구, 길이(기본 6초), 크기(쇼츠 1080 × 1920, 정사각 1080 × 1080, 템플릿 기본 1020 × 840).
2. 템플릿을 `src/Motion2D.jsx`로 저장하고, 아래 등록 코드를 `src/Root.jsx`에 넣어요. 문구 · 색 · 크기를 바꿔요.
3. `npx remotion studio`로 미리 보여 줘요(브라우저에서 바로 재생).
4. 뽑기: `npx remotion render src/index.ts FantasyScene out/fantasy.mp4 --codec=h264 --crf=16`
5. 확인: `ffmpeg -ss 1 -i out/fantasy.mp4 -frames:v 1 t1.jpg` 처럼 1 · 3 · 5초 장면을 뽑아 글자 넘침 · 겹침 · 빈 화면을 보고, 사용자에게 영상과 장면을 함께 보여 줘요.
6. 피드백을 말로 받으면 고쳐서 다시 뽑아요.

## 2. 원칙 (디플래너가 실제로 받은 피드백에서 나온 것)

- 글자만 두지 말고 아이콘을 크게 같이 둬요.
- 움직임은 `spring`(감쇠 8~12)으로 튀게 하고, 여러 요소는 3~6프레임 간격으로 차례로 등장시켜요. 한 화면은 3초 이상 보여 줘요.
- 색: 어두운 배경에 강조색 하나(예: 형광연두 #CCFF00). 풍경은 셀 셰이딩처럼 밝은 면 · 그림자 면 두 톤으로 칠해요.
- 판타지 풍경 레이어 순서(뒤 → 앞): 하늘 그라데이션 → 해 · 빛줄기 → 구름(두 톤) → 먼 섬 · 새 떼 → 먼 산(멀수록 연하게) → 안개 → 부유섬 → 들판(두 톤 + 밝은 테두리) → 꽃 → 풀잎(sin으로 흔들림) → 반딧불 → 꽃잎 → 비네트. 카메라는 천천히 다가가고, 레이어마다 다른 속도로 옆으로 움직여요(패럴랙스).
- 같은 결과가 나오도록 무작위 값은 Remotion의 `random('이름')`을 써요(`Math.random` 금지).
- 프레임마다 바뀌는 그라데이션에 `background-clip: text`를 쓸 때는 `background` 줄임 속성 대신 `backgroundImage`로 넣어요. React가 프레임마다 `background`만 다시 넣으면 자르기 설정이 처음 값으로 돌아가 글자 대신 네모 상자가 칠해져요.
- 가짜 게임 이름 · 메뉴 문구는 뜻 없는 서정적 이름(예: 「잿빛 들판」)보다 보는 사람이 웃을 패러디가 잘 통해요. 예: 「기획의 전설: 야근의 숨결」, 메뉴 「출근하기 · 야근 이어하기 · 퇴사하기(잠김)」. 실제 작품의 이름 · 로고는 쓰지 않아요.
- 한계: 사람 캐릭터가 걷고 뛰는 수준의 애니메이션은 코드로 만들기 어려워요. 풍경 · 사물 · 글자 · 도형 중심으로 만들고, 사람이 필요하면 AI 영상 도구로 따로 만든 영상을 겹쳐요. 특정 게임 · 작품의 캐릭터 · 로고 · 고유 디자인은 쓰지 않고, 판타지풍 같은 장르 화풍으로 그려요. 게임에 쓸 때는 영상(타이틀 · 로딩 화면 배경, 트레일러 컷)을 만들고, 게임 자체(조작 · 점수 · 판정)는 만들지 않아요.

## 3. 템플릿 코드 (`src/Motion2D.jsx`, 실제로 뽑아 확인한 코드)

```jsx
import React from 'react';
import {AbsoluteFill, Easing, interpolate, random, spring, useCurrentFrame} from 'remotion';
// 한글 글꼴(예: Pretendard, OFL)을 public/fonts에 두고 CSS @font-face로 불러온 뒤 그 이름을 적습니다.
const FONT = 'Pretendard';
const TRACKING = '-0.03em';
// 글꼴을 CSS로 불러오므로 따로 할 일이 없습니다(디플래너 프로젝트에서는 글꼴을 미리 불러오는 함수를 씁니다).
const useFonts = () => {};

// 2D 애니메이션 템플릿 네 가지(디플래너, 2026-11-05). 실제로 영상으로 뽑아 확인한 코드입니다.
// 크기 1020 × 840(쇼츠 PIP 카드 안쪽), 30fps, 6초. 코드만으로 그린다(이미지 · 외부 그림 없음).
// 판타지풍 화풍(셀 셰이딩 두 톤, 맑은 하늘, 부유섬, 넓은 들판)만 따르고, 특정 게임의 캐릭터 · 로고 같은 고유 디자인은 쓰지 않는다.

const FPS = 30;
const W = 1020;
const H = 840;
const LIME = '#CCFF00';
const clamp = {extrapolateLeft: 'clamp', extrapolateRight: 'clamp'};
const ease = {...clamp, easing: Easing.inOut(Easing.cubic)};
const pop = (f, at, damping = 11) => spring({frame: f - at, fps: FPS, config: {damping, stiffness: 180}});

const ICONS = {
  chat: <path d="M4 5h16v11H10l-5 4v-4H4z" />,
  script: (
    <>
      <path d="M6 3h9l4 4v14H6z" />
      <path d="M15 3v4h4M9 11h7M9 15h7M9 19h4" />
    </>
  ),
  mic: (
    <>
      <rect x="9" y="3" width="6" height="11" rx="3" />
      <path d="M5.5 11a6.5 6.5 0 0 0 13 0M12 17.5V21M8.5 21h7" />
    </>
  ),
  video: (
    <>
      <rect x="3" y="5" width="18" height="14" rx="3" />
      <path d="M10 9l5 3-5 3z" />
    </>
  ),
  upload: <path d="M12 15V4M7.5 8.5L12 4l4.5 4.5M4 16v4h16v-4" />,
  check: <path d="M5 12.5l4.5 4.5L19 7.5" />,
};
const Icon = ({name, size, color}) => (
  <svg width={size} height={size} viewBox="0 0 24 24" fill="none" stroke={color} strokeWidth="2.2" strokeLinecap="round" strokeLinejoin="round">
    {ICONS[name]}
  </svg>
);

// ── 1. 모션 타이포그래피: 글자가 튀어나오고, 한 글자씩 떨어져 튀고, 미끄러져 들어온다 ──
export const MotionType = () => {
  useFonts();
  const f = useCurrentFrame();
  const zoomOut = interpolate(f, [150, 180], [1, 1.06], ease);
  const gridShift = (f * 1.2) % 60;
  const l1 = pop(f, 4, 9);
  const l3 = interpolate(f, [52, 70], [1, 0], {...clamp, easing: Easing.out(Easing.cubic)});
  const bar = interpolate(f, [78, 98], [0, 1], ease);
  const word2 = '춤추는';
  return (
    <AbsoluteFill style={{background: 'radial-gradient(ellipse 80% 70% at 50% 45%, #18233A 0%, #0A0D16 70%)', fontFamily: `${FONT}, 'Noto Sans CJK KR', sans-serif`, overflow: 'hidden'}}>
      <style>{`.mt, .mt * { letter-spacing: ${TRACKING}; }`}</style>
      <AbsoluteFill style={{backgroundImage: 'linear-gradient(rgba(255,255,255,0.05) 1px, transparent 1px), linear-gradient(90deg, rgba(255,255,255,0.05) 1px, transparent 1px)',
        backgroundSize: '60px 60px', backgroundPosition: `${gridShift}px ${gridShift}px`}} />
      {/* 퍼지는 고리 */}
      {[118, 128, 138].map((at, k) => {
        const r = interpolate(f, [at, at + 30], [0, 520], {...clamp, easing: Easing.out(Easing.cubic)});
        const o = interpolate(f, [at, at + 30], [0.7, 0], clamp);
        return f >= at ? <div key={k} style={{position: 'absolute', left: W / 2 - r, top: 420 - r, width: r * 2, height: r * 2, borderRadius: '50%', border: `${6 - k * 1.5}px solid ${LIME}`, opacity: o}} /> : null;
      })}
      {/* 흩날리는 조각 */}
      {f >= 118
        ? Array.from({length: 26}).map((_, k) => {
            const a = random(`ang${k}`) * Math.PI * 2;
            const d = interpolate(f, [118, 175], [0, 260 + random(`d${k}`) * 260], {...clamp, easing: Easing.out(Easing.quad)});
            const o = interpolate(f, [118, 128, 175], [0, 1, 0], clamp);
            return (
              <div key={k} style={{position: 'absolute', left: W / 2 + Math.cos(a) * d, top: 420 + Math.sin(a) * d, width: 16, height: 16, borderRadius: k % 3 ? 3 : 8,
                background: k % 2 ? LIME : '#FFFFFF', opacity: o, transform: `rotate(${f * 6 + k * 40}deg)`}} />
            );
          })
        : null}
      <div className="mt" style={{position: 'absolute', inset: 0, transform: `scale(${zoomOut})`}}>
        {/* 1행: 튀어나오며 기울었다 바로 선다 */}
        <div style={{position: 'absolute', left: 0, right: 0, top: 120, textAlign: 'center', fontSize: 150, fontWeight: 800, color: '#F5F5F5',
          transform: `scale(${l1}) rotate(${(1 - l1) * -12}deg)`, opacity: Math.min(1, l1 * 1.5)}}>글자가</div>
        {/* 2행: 한 글자씩 위에서 떨어져 튀고, 이어서 파도처럼 흔들린다 */}
        <div style={{position: 'absolute', left: 0, right: 0, top: 300, display: 'flex', justifyContent: 'center', gap: 6}}>
          {word2.split('').map((ch, k) => {
            const s = pop(f, 22 + k * 5, 8);
            const wave = f > 90 ? Math.sin((f - 90) / 6 - k * 0.9) * 14 : 0;
            return (
              <span key={k} style={{display: 'inline-block', fontSize: 190, fontWeight: 900, color: LIME, textShadow: '0 10px 40px rgba(204,255,0,0.35)',
                transform: `translateY(${(1 - s) * -260 + wave}px) rotate(${(1 - s) * 30}deg)`, opacity: Math.min(1, s * 2)}}>{ch}</span>
            );
          })}
        </div>
        {/* 3행: 오른쪽에서 미끄러져 들어오며 잔상이 남는다 */}
        <div style={{position: 'absolute', left: 0, right: 0, top: 560, textAlign: 'center', fontSize: 130, fontWeight: 800, color: '#F5F5F5',
          transform: `translateX(${l3 * 700}px) skewX(${l3 * -24}deg)`, opacity: f >= 52 ? 1 : 0,
          textShadow: l3 > 0.02 ? `${l3 * 60}px 0 0 rgba(204,255,0,0.45), ${l3 * 120}px 0 0 rgba(204,255,0,0.2)` : 'none'}}>모션 타이포</div>
        <div style={{position: 'absolute', left: (W - 640 * bar) / 2, top: 720, width: 640 * bar, height: 16, borderRadius: 8, background: LIME}} />
      </div>
    </AbsoluteFill>
  );
};

// ── 2. 플로우차트 애니메이션: 상자가 차례로 나타나고, 선이 그려지고, 선 위로 빛이 흐른다 ──
const NODES = [
  {x: 175, y: 210, label: '아이디어', icon: 'chat'},
  {x: 510, y: 210, label: '대본', icon: 'script'},
  {x: 845, y: 210, label: '목소리', icon: 'mic'},
  {x: 845, y: 580, label: '화면', icon: 'video'},
  {x: 510, y: 580, label: '업로드', icon: 'upload'},
];
const NODE_AT = (i) => 6 + i * 22;
const NW = 292;
const NH = 130;
const edgePts = (a, b) => {
  // 상자 가장자리에서 가장자리까지
  const A = NODES[a];
  const B = NODES[b];
  if (A.y === B.y) {
    const dir = Math.sign(B.x - A.x);
    return [A.x + (dir * NW) / 2, A.y, B.x - (dir * NW) / 2, B.y];
  }
  return [A.x, A.y + NH / 2, B.x, B.y - NH / 2];
};
export const FlowAnim = () => {
  useFonts();
  const f = useCurrentFrame();
  const done = pop(f, 128, 9);
  return (
    <AbsoluteFill style={{background: 'radial-gradient(ellipse 80% 70% at 50% 45%, #13202F 0%, #090C12 75%)', fontFamily: `${FONT}, 'Noto Sans CJK KR', sans-serif`, overflow: 'hidden'}}>
      <AbsoluteFill style={{backgroundImage: 'radial-gradient(rgba(255,255,255,0.08) 1.5px, transparent 1.5px)', backgroundSize: '34px 34px'}} />
      <svg width={W} height={H} style={{position: 'absolute', inset: 0}}>
        {NODES.slice(0, -1).map((_, i) => {
          const [x1, y1, x2, y2] = edgePts(i, i + 1);
          const len = Math.hypot(x2 - x1, y2 - y1);
          const at = NODE_AT(i) + 10;
          const k = interpolate(f, [at, at + 12], [0, 1], ease);
          const flowOn = f > at + 12;
          return (
            <g key={i}>
              <line x1={x1} y1={y1} x2={x2} y2={y2} stroke="#2E3F55" strokeWidth="8" strokeLinecap="round" />
              <line x1={x1} y1={y1} x2={x2} y2={y2} stroke={LIME} strokeWidth="8" strokeLinecap="round" strokeDasharray={len} strokeDashoffset={len * (1 - k)} />
              {flowOn
                ? [0, 1, 2].map((p) => {
                    const t = ((f - at - 12) / 24 + p / 3) % 1;
                    return <circle key={p} cx={x1 + (x2 - x1) * t} cy={y1 + (y2 - y1) * t} r="9" fill="#FFFFFF" opacity={Math.sin(t * Math.PI)} style={{filter: 'drop-shadow(0 0 8px #CCFF00)'}} />;
                  })
                : null}
            </g>
          );
        })}
      </svg>
      {NODES.map((n, i) => {
        const s = pop(f, NODE_AT(i), 10);
        const lit = f >= NODE_AT(i) + 4;
        return (
          <div key={i} style={{position: 'absolute', left: n.x - NW / 2, top: n.y - NH / 2, width: NW, height: NH, borderRadius: 26, background: '#111A26',
            border: `5px solid ${lit ? LIME : '#2E3F55'}`, boxShadow: lit ? '0 0 34px rgba(204,255,0,0.25)' : 'none', display: 'flex', alignItems: 'center', gap: 14, padding: '0 18px',
            transform: `scale(${0.4 + 0.6 * s})`, opacity: Math.min(1, s * 1.6)}}>
            <div style={{width: 62, height: 62, borderRadius: '50%', background: 'rgba(204,255,0,0.12)', display: 'flex', alignItems: 'center', justifyContent: 'center', flexShrink: 0}}>
              <Icon name={n.icon} size={40} color={LIME} />
            </div>
            <div style={{fontSize: 42, fontWeight: 800, color: '#F5F5F5', letterSpacing: TRACKING, whiteSpace: 'nowrap'}}>{n.label}</div>
          </div>
        );
      })}
      {/* 끝: 완성 배지 */}
      {f >= 126 ? (
        <div style={{position: 'absolute', left: 175 - 120, top: 580 - 70, width: 240, height: 140, borderRadius: 30, background: LIME, display: 'flex', alignItems: 'center', justifyContent: 'center', gap: 12,
          transform: `scale(${0.3 + 0.7 * done}) rotate(${(1 - done) * -20}deg)`, boxShadow: '0 0 60px rgba(204,255,0,0.5)'}}>
          <Icon name="check" size={60} color="#0A0A0A" />
          <div style={{fontSize: 50, fontWeight: 900, color: '#0A0A0A'}}>완성</div>
        </div>
      ) : null}
      {f >= 118 ? (
        <svg width={W} height={H} style={{position: 'absolute', inset: 0}}>
          {(() => {
            const [x1, y1] = [510 - NW / 2, 580];
            const [x2, y2] = [175 + 120, 580];
            const len = x1 - x2;
            const k = interpolate(f, [118, 128], [0, 1], ease);
            return <line x1={x1} y1={y1} x2={x2} y2={y2} stroke={LIME} strokeWidth="8" strokeLinecap="round" strokeDasharray={len} strokeDashoffset={len * (1 - k)} />;
          })()}
        </svg>
      ) : null}
    </AbsoluteFill>
  );
};

// ── 3. 판타지 풍경(판타지풍): 셀 셰이딩 두 톤 하늘 · 구름 · 부유섬 · 들판, 흔들리는 풀, 빛줄기, 반딧불 ──
const Cloud = ({x, y, s}) => (
  <g transform={`translate(${x} ${y}) scale(${s})`}>
    {/* 그림자 톤(아래) */}
    <g fill="#C7D3F2">
      <circle cx="-70" cy="22" r="52" />
      <circle cx="0" cy="18" r="70" />
      <circle cx="78" cy="24" r="50" />
      <rect x="-122" y="22" width="250" height="50" rx="25" />
    </g>
    {/* 밝은 톤(위) */}
    <g fill="#FFFFFF">
      <circle cx="-70" cy="4" r="48" />
      <circle cx="-8" cy="-24" r="66" />
      <circle cx="70" cy="2" r="46" />
      <rect x="-118" y="4" width="236" height="40" rx="20" />
    </g>
  </g>
);
export const FantasyScene = () => {
  const f = useCurrentFrame();
  const p = interpolate(f, [0, 180], [0, 1]);
  const bob = Math.sin(f / 18) * 9;
  const wind = Math.sin(f / 26) * 6;
  return (
    <AbsoluteFill style={{overflow: 'hidden', background: '#87CEEB'}}>
      <svg width={W} height={H} viewBox={`0 0 ${W} ${H}`} style={{position: 'absolute', inset: 0, transform: `scale(${1.04 + p * 0.03})`, transformOrigin: '50% 60%'}}>
        <defs>
          <linearGradient id="sky" x1="0" y1="0" x2="0" y2="1">
            <stop offset="0" stopColor="#2F86C6" />
            <stop offset="0.55" stopColor="#8FD3F0" />
            <stop offset="1" stopColor="#FFE2B0" />
          </linearGradient>
          <radialGradient id="sun" cx="0.5" cy="0.5" r="0.5">
            <stop offset="0" stopColor="#FFFDF2" stopOpacity="1" />
            <stop offset="0.35" stopColor="#FFF3C4" stopOpacity="0.8" />
            <stop offset="1" stopColor="#FFF3C4" stopOpacity="0" />
          </radialGradient>
          <linearGradient id="hillA" x1="0" y1="0" x2="0" y2="1">
            <stop offset="0" stopColor="#8FD37A" />
            <stop offset="1" stopColor="#5BAA52" />
          </linearGradient>
          <linearGradient id="hillB" x1="0" y1="0" x2="0" y2="1">
            <stop offset="0" stopColor="#6BBF5E" />
            <stop offset="1" stopColor="#3F8D44" />
          </linearGradient>
          <radialGradient id="vig" cx="0.5" cy="0.45" r="0.75">
            <stop offset="0.6" stopColor="#000" stopOpacity="0" />
            <stop offset="1" stopColor="#0A1A2A" stopOpacity="0.45" />
          </radialGradient>
        </defs>
        {/* 하늘 · 해 · 빛줄기 */}
        <rect width={W} height={H} fill="url(#sky)" />
        <g transform={`rotate(${f * 0.15} 820 170)`} opacity="0.11">
          {Array.from({length: 7}).map((_, k) => (
            <polygon key={k} points="820,170 1500,140 1500,200" fill="#FFF8D6" transform={`rotate(${k * 51} 820 170)`} />
          ))}
        </g>
        <circle cx="820" cy="170" r="170" fill="url(#sun)" />
        <circle cx="820" cy="170" r="46" fill="#FFF8E1" />
        {/* 구름(셀 셰이딩 두 톤) */}
        <Cloud x={-80 + ((f * 0.9) % 1300)} y={150} s={1.05} />
        <Cloud x={420 + ((f * 0.5) % 900) - 300} y={95} s={0.7} />
        <Cloud x={1180 - ((f * 0.6) % 1400)} y={300} s={0.85} />
        {/* 멀리 떠 있는 작은 섬(대기 원근으로 연하게) */}
        <g transform={`translate(${760 - p * 15} ${360 + Math.sin(f / 22 + 1) * 6}) scale(0.42)`} opacity="0.75">
          <path d="M-120 0 Q-60 150 0 190 Q60 150 120 0 Z" fill="#9C93A8" />
          <ellipse cx="0" cy="0" rx="128" ry="30" fill="#9CCB9A" />
          <circle cx="30" cy="-52" r="34" fill="#86BC8C" />
        </g>
        {/* 새 떼 */}
        {Array.from({length: 5}).map((_, k) => {
          const x = ((f * 2.2 + k * 46) % 1300) - 140;
          const y = 140 + k * 14 + Math.sin(f / 9 + k) * 6;
          const flap = Math.sin(f / 3 + k) * 7;
          return <path key={`b${k}`} d={`M${x - 14} ${y + flap} Q${x - 6} ${y - 4} ${x} ${y} Q${x + 6} ${y - 4} ${x + 14} ${y + flap}`} fill="none" stroke="#3B5A7A" strokeWidth="3" strokeLinecap="round" />;
        })}
        {/* 먼 산(대기 원근: 멀수록 연하다) */}
        <path d={`M${-40 - p * 20} 470 L120 330 L230 420 L360 280 L520 430 L640 340 L800 450 L930 310 L1100 470 Z`} fill="#A9BCE6" />
        <path d={`M${-40 - p * 35} 500 L80 410 L210 470 L330 380 L470 480 L600 400 L760 490 L900 390 L1100 500 Z`} fill="#8EA6D8" />
        {/* 부유섬: 윗면 풀 두 톤, 아래 바위 두 톤, 작은 폭포 */}
        <g transform={`translate(${300 - p * 30} ${280 + bob})`}>
          <path d="M-120 0 Q-60 150 0 190 Q60 150 120 0 Z" fill="#8C7A68" />
          <path d="M0 0 Q20 120 0 190 Q60 150 120 0 Z" fill="#6E5E50" />
          <ellipse cx="0" cy="0" rx="128" ry="30" fill="#7CC96B" />
          <ellipse cx="0" cy="-6" rx="118" ry="22" fill="#A3DE84" />
          <rect x="70" y="10" width="12" height="150" rx="6" fill="#E9F7FF" opacity="0.85" />
          <rect x="72" y={(f * 4) % 140 + 10} width="8" height="26" rx="4" fill="#FFFFFF" />
          <rect x="-20" y="-60" width="10" height="46" rx="5" fill="#6B4E3A" />
          <circle cx="-15" cy="-74" r="36" fill="#4FA35A" />
          <circle cx="-5" cy="-84" r="24" fill="#7BCB6E" />
        </g>
        {/* 산과 들 사이 안개 */}
        <rect x="0" y="440" width={W} height="110" fill="#FFFFFF" opacity={0.28 + Math.sin(f / 30) * 0.05} style={{filter: 'blur(18px)'}} />
        {/* 들판(가운데 · 앞) */}
        <path d={`M${-60 - p * 50} 560 Q200 470 430 540 T880 520 T1180 560 L1180 ${H} L-60 ${H} Z`} fill="url(#hillA)" />
        <path d={`M${-60 - p * 50} 560 Q200 470 430 540 T880 520 T1180 560`} fill="none" stroke="#B9EBA0" strokeWidth="6" />
        <path d={`M${-80 - p * 80} 680 Q240 600 520 660 T1120 640 L1180 ${H} L-80 ${H} Z`} fill="url(#hillB)" />
        <path d={`M${-80 - p * 80} 680 Q240 600 520 660 T1120 640`} fill="none" stroke="#8FD37A" strokeWidth="6" />
        {/* 작은 꽃 */}
        {Array.from({length: 14}).map((_, k) => {
          const x = 40 + k * 72 + random(`fx${k}`) * 30 - p * 80;
          const y = 690 + random(`fy${k}`) * 70;
          const c = ['#FFFFFF', '#FFD6E7', '#FFF1A8'][k % 3];
          return (
            <g key={k} transform={`translate(${x} ${y})`}>
              {[0, 72, 144, 216, 288].map((a) => <circle key={a} cx={Math.cos((a * Math.PI) / 180) * 6} cy={Math.sin((a * Math.PI) / 180) * 6} r="5" fill={c} />)}
              <circle r="4" fill="#FFC23C" />
            </g>
          );
        })}
        {/* 흔들리는 풀잎 */}
        {Array.from({length: 150}).map((_, k) => {
          const x = (k / 150) * (W + 80) - 40 + random(`gx${k}`) * 10;
          const h = 95 + random(`gh${k}`) * 95;
          const sway = Math.sin(f / 11 + x * 0.04) * 10 + wind;
          const col = ['#2E7A35', '#45A04A', '#A6E08A'][k % 3];
          return <path key={k} d={`M${x - 5} ${H} Q${x + sway * 0.4} ${H - h * 0.55} ${x + sway} ${H - h} Q${x + sway * 0.3} ${H - h * 0.5} ${x + 5} ${H} Z`} fill={col} />;
        })}
        {/* 반딧불 · 꽃가루 */}
        {Array.from({length: 40}).map((_, k) => {
          const x0 = random(`px${k}`) * W;
          const y0 = 300 + random(`py${k}`) * 520;
          const x = x0 + Math.sin(f / 25 + k) * 24 + f * 0.4;
          const y = y0 - ((f * (0.6 + random(`ps${k}`) * 0.8)) % 260);
          const o = 0.35 + 0.65 * (0.5 + 0.5 * Math.sin(f / 7 + k * 1.7));
          return <circle key={k} cx={x % W} cy={y} r={2.5 + random(`pr${k}`) * 3} fill="#FFF6B8" opacity={o} style={{filter: 'drop-shadow(0 0 6px #FFF3A0)'}} />;
        })}
        {/* 바람에 날리는 꽃잎 */}
        {Array.from({length: 12}).map((_, k) => {
          const t = ((f + k * 15) % 180) / 180;
          const x = -40 + t * (W + 80);
          const y = 200 + random(`ly${k}`) * 380 + Math.sin(t * 9 + k) * 40;
          return <ellipse key={k} cx={x} cy={y} rx="9" ry="5" fill="#FFC6DA" transform={`rotate(${f * 5 + k * 30} ${x} ${y})`} opacity="0.9" />;
        })}
        <rect width={W} height={H} fill="url(#vig)" />
      </svg>
    </AbsoluteFill>
  );
};

// ── 4. 게임 타이틀 화면: 판타지 풍경 위에 게임 제목 · 메뉴를 얹는다(게임 타이틀 · 로딩 화면 배경 영상, 트레일러 컷용) ──
// 가짜 게임 이름 · 메뉴는 보는 사람이 웃을 패러디로 짓는다(예: 직장인 패러디). 실제 작품의 이름 · 로고는 쓰지 않는다.
// 이 스킬은 영상(mp4)을 만든다. 게임 자체(조작 · 판정)는 만들지 않는다.
const GAME_TITLE = ['기', '획', '의', ' ', '전', '설'];
const GAME_SUB = '야근의 숨결';
const GAME_MENU = ['출근하기', '야근 이어하기', '퇴사하기'];
const GAME_LOCKED = 2; // 퇴사하기는 잠겨 있다
export const GameTitle = () => {
  useFonts();
  const f = useCurrentFrame();
  const sub = interpolate(f, [34, 50], [0, 1], ease);
  const shine = interpolate(f, [70, 112], [125, -25], clamp);
  const sel = 0.5 + 0.5 * Math.sin(f / 6);
  const arrow = Math.sin(f / 5) * 6;
  const floatY = Math.sin(f / 20) * 4;
  const logo = {fontSize: 148, fontWeight: 900, lineHeight: 1.1, whiteSpace: 'pre'};
  const gold = {background: 'linear-gradient(180deg, #FFFBE6 0%, #FFE07A 50%, #F5A53A 100%)', WebkitBackgroundClip: 'text', backgroundClip: 'text', color: 'transparent'};
  return (
    <AbsoluteFill style={{overflow: 'hidden', fontFamily: `${FONT}, 'Noto Sans CJK KR', sans-serif`}}>
      <style>{`.gt, .gt * { letter-spacing: ${TRACKING}; }`}</style>
      <FantasyScene />
      {/* 글자가 잘 보이게 위 · 아래를 어둡게 */}
      <AbsoluteFill style={{background: 'linear-gradient(180deg, rgba(10,24,52,0.6) 0%, rgba(10,24,52,0) 44%, rgba(10,24,52,0) 54%, rgba(8,18,40,0.72) 100%)'}} />
      {/* 게임 제목: 한 글자씩 위에서 떨어지며 튀고, 빛 띠가 한 번 지나간다 */}
      <div className="gt" style={{position: 'absolute', left: 0, right: 0, top: 96 + floatY, display: 'flex', flexDirection: 'column', alignItems: 'center'}}>
        <div style={{position: 'relative', display: 'flex'}}>
          {GAME_TITLE.map((ch, i) => {
            const p = pop(f, 6 + i * 4, 9);
            return (
              <span key={i} style={{...logo, ...gold, display: 'inline-block', opacity: Math.min(1, p * 1.5), transform: `translateY(${(1 - p) * -120}px) scale(${0.4 + 0.6 * p})`, filter: 'drop-shadow(0 7px 0 #5B3413) drop-shadow(0 0 26px rgba(255,214,120,0.55))'}}>
                {ch}
              </span>
            );
          })}
          {/* 빛 띠는 글자 모양으로만 보이게 background-clip: text를 건다. 움직이는 그라데이션은 background 줄임 속성이 아니라 backgroundImage로 넣는다.
              (React가 프레임마다 background만 다시 넣으면 background-clip이 처음 값으로 돌아가 빛 띠가 네모 상자로 보인다.)
              */}
          {f >= 66 ? (
            <div style={{...logo, position: 'absolute', left: 0, top: 0, backgroundImage: `linear-gradient(110deg, rgba(255,255,255,0) ${shine - 12}%, rgba(255,255,255,0.95) ${shine}%, rgba(255,255,255,0) ${shine + 12}%)`, WebkitBackgroundClip: 'text', backgroundClip: 'text', color: 'transparent'}}>
              {GAME_TITLE.join('')}
            </div>
          ) : null}
        </div>
        {/* 부제: 제목 아래에서 올라온다 */}
        <div style={{marginTop: 10, opacity: sub, transform: `translateY(${(1 - sub) * 14}px)`, display: 'flex', alignItems: 'center', gap: 22}}>
          <div style={{width: 64, height: 4, borderRadius: 2, background: 'rgba(234,246,255,0.9)'}} />
          <span style={{fontSize: 60, fontWeight: 900, color: '#EAF6FF', textShadow: '0 4px 0 #1C3A66, 0 0 22px rgba(120,190,255,0.75)'}}>{GAME_SUB}</span>
          <div style={{width: 64, height: 4, borderRadius: 2, background: 'rgba(234,246,255,0.9)'}} />
        </div>
      </div>
      {/* 메뉴: 아래에서 차례로 올라오고, 고른 칸은 빛나며 화살표가 움직인다. 마지막 칸(퇴사하기)은 잠겨 있다. */}
      <div className="gt" style={{position: 'absolute', left: 0, right: 0, top: 492, display: 'flex', flexDirection: 'column', alignItems: 'center', gap: 16}}>
        {GAME_MENU.map((m, i) => {
          const p = pop(f, 48 + i * 6, 12);
          const on = i === 0;
          const locked = i === GAME_LOCKED;
          return (
            <div key={m} style={{
              position: 'relative', width: 360, height: 74, borderRadius: 18, display: 'flex', alignItems: 'center', justifyContent: 'center', gap: 12,
              fontSize: 36, fontWeight: 800, color: on ? '#10210F' : locked ? '#A3AEC0' : '#FFFFFF',
              background: on ? `rgba(204,255,0,${0.82 + 0.12 * sel})` : locked ? 'rgba(10,24,52,0.5)' : 'rgba(10,24,52,0.62)',
              border: on ? '3px solid #F4FFB8' : locked ? '2px dashed rgba(255,255,255,0.3)' : '2px solid rgba(255,255,255,0.4)',
              boxShadow: on ? `0 0 ${18 + 16 * sel}px rgba(204,255,0,0.65)` : '0 8px 20px rgba(0,0,0,0.3)',
              opacity: Math.min(1, p * 1.4), transform: `translateY(${(1 - p) * 40}px)`,
            }}>
              {on ? (
                <svg width="30" height="30" viewBox="0 0 24 24" style={{position: 'absolute', left: -50 + arrow, top: 22}}>
                  <path d="M6 3l14 9-14 9z" fill="#FFFFFF" stroke="#10210F" strokeWidth="1.5" strokeLinejoin="round" />
                </svg>
              ) : null}
              {locked ? (
                <svg width="30" height="30" viewBox="0 0 24 24" fill="none" stroke="#A3AEC0" strokeWidth="2.4" strokeLinecap="round" strokeLinejoin="round">
                  <rect x="5" y="11" width="14" height="10" rx="2" />
                  <path d="M8 11V8a4 4 0 0 1 8 0v3" />
                </svg>
              ) : null}
              {m}
              {locked ? (
                <span style={{position: 'absolute', right: -84, top: 19, padding: '4px 12px', borderRadius: 14, background: 'rgba(255,90,90,0.9)', color: '#FFFFFF', fontSize: 22, fontWeight: 800}}>잠김</span>
              ) : null}
            </div>
          );
        })}
      </div>
      <div style={{position: 'absolute', right: 28, bottom: 22, color: 'rgba(255,255,255,0.78)', fontSize: 22, fontWeight: 600, opacity: sub}}>Ver 0.1 · 월요일 패치</div>
    </AbsoluteFill>
  );
};
```

## 4. 등록 코드 (`src/Root.jsx`)

```jsx
import {Composition} from 'remotion';
import {FantasyScene, FlowAnim, GameTitle, MotionType} from './Motion2D';

export const RemotionRoot = () => (
  <>
    <Composition id="MotionType" component={MotionType} width={1020} height={840} fps={30} durationInFrames={180} />
    <Composition id="FlowAnim" component={FlowAnim} width={1020} height={840} fps={30} durationInFrames={180} />
    <Composition id="FantasyScene" component={FantasyScene} width={1020} height={840} fps={30} durationInFrames={180} />
    <Composition id="GameTitle" component={GameTitle} width={1020} height={840} fps={30} durationInFrames={180} />
  </>
);
```

크기를 바꿀 때는 템플릿 위쪽 `W` · `H`와 등록 코드의 `width` · `height`를 함께 바꾸고, 글자 크기 · 상자 위치를 비율에 맞춰 고쳐요.

## 5. 이렇게 부탁해 보세요

- 「motion-2d-kit 스킬로 '오늘 할 일 3가지'를 모션 타이포 6초로 만들어 줘. 쇼츠 크기로.」
- 「우리 서비스 가입 흐름(방문 → 가입 → 첫 결제 → 재방문)을 움직이는 플로우차트로 만들어 줘.」
- 「노을 지는 들판에 반딧불이 떠다니는 판타지풍 풍경을 10초로, 위에 '새로운 시작' 글자를 얹어 줘.」
- 「'기획의 전설: 야근의 숨결'이라는 직장인 패러디 게임의 타이틀 화면을 판타지 풍경 위에 6초로 만들어 줘. 메뉴는 출근하기 · 야근 이어하기 · 퇴사하기(잠김)로.」

## 받은 피드백

- (사용자 피드백을 원문으로 적고 다음 영상부터 지켜요.)

---
만든 곳: 디플래너(dplanner@outlook.kr). 2026-11-05 디플래너 쇼츠 제작에 실제로 쓴 코드예요.
ⓒ 디플래너. 이 스킬 파일과 노션 가이드의 상업적 이용 · 무단 배포는 금지예요. 내 클로드에 설치해 쓰는 것은 괜찮아요.
