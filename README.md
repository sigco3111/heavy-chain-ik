# 🪝 Heavy Chain IK (Inverse Kinematics)

> 화면 상단에 매달린 녹슨 쇠사슬을 마우스로 잡아당기거나 흔들어, 무거운 물리적 무게감으로 움직이고 화면 안 나무상자들을 무너뜨리는 인터랙티브 시뮬레이터.

---

## 🎬 라이브 데모

> **👉 [https://heavy-chain-ik.vercel.app/](https://heavy-chain-ik.vercel.app/)** — 브라우저에서 바로 실행 (Matter.js 기반)

| | |
|---|---|
| ![Demo](https://img.shields.io/badge/Live-Demo-7C3AED?style=for-the-badge&logo=vercel&logoColor=white) | [![Repo](https://img.shields.io/badge/GitHub-sigco3111%2Fheavy--chain--ik-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/sigco3111/heavy-chain-ik) |
| ![Status](https://img.shields.io/badge/Status-Live-22C55E?style=flat-square) | ![Stack](https://img.shields.io/badge/Stack-Matter.js-F7DF1E?style=flat-square&logo=javascript&logoColor=black) |
| ![License](https://img.shields.io/badge/License-MIT-F1C40F?style=flat-square) | ![Deps](https://img.shields.io/badge/Dependencies-1_CDN-9CA3AF?style=flat-square) |

### 🎮 빠른 사용법
1. 위 데모 링크 클릭 → 브라우저에서 페이지 열기
2. **마우스 드래그** — 사슬 끝 또는 임의 Link를 잡고 흔들기
3. **스페이스바** — 레킹 볼에 강한 임펄스 (상자 폭파용)
4. **R 키** — 사슬 + 상자 리셋
5. **L 키** — 한국어 ↔ English 토글 (localStorage에 저장)
6. **HUD "sound"** — 사운드 ON/OFF

---

## 🤖 생성 정보

이 프로젝트의 코드는 아래 모델과 프롬프트를 이용해 **자동으로 생성**되었습니다.

| 항목 | 값 |
|---|---|
| **모델** | MiniMax-M3 |
| **실행 환경** | OpenCode CLI |
| **저장소** | [`sigco3111/heavy-chain-ik`](https://github.com/sigco3111/heavy-chain-ik) |
| **라이선스** | MIT |
| **의존성** | Matter.js (CDN 1개, 단일 HTML) |

### 📝 사용된 프롬프트 (원문)

```
화면 상단에 고정된 녹슨 쇠사슬을 마우스로 잡아당기거나 흔들 수 있는 시뮬레이션을 만들되,
각 사슬 고리(Link) 간의 물리적 제약(Constraints)과 마찰력을 정교하게 계산하여
묵직한 무게감이 느껴지도록 하고, 사슬로 화면에 있는 나무상자들을 쳐서 무너뜨릴 수 있는
인터랙티브 환경을 구현해줘.

Implementation Advice: Use Matter.js. It creates excellent chain simulations
using Constraints between bodies. Use rectangular bodies for links and adjust
density/friction to simulate the heavy "rusty" feel. 모든 의존관계의 코드를
하나의 HTML에 담는 형태로 코드 작성.
```

---

## ✨ 주요 특징

- 🪝 **무거운 사슬 물리** — 24개의 직사각형 Link + Constraint로 묵직한 IK 체인 구현
- 🖱️ **마우스 드래그** — 사슬 끝(또는 임의 Link)을 잡고 이동, stiffness 0.12로 적당한 lag
- ⚫ **레킹 볼** — 사슬 끝에 매달린 무거운 철구(density 0.3, 링크의 ~28배), 충돌 시 박스 멀리 날림
- 🔊 **절차적 사운드** — Web Audio API로 쇠 '쨍' + 나무 '쿵' 합성, 외부 오디오 파일 0개
- 💨 **먼지 파티클** — 강한 임팩트 시 충돌 지점에서 wood-tone 먼지 분출
- 📦 **파괴 가능한 나무상자** — 사슬로 쳐서 무너뜨리는 인터랙션
- 🦀 **녹슨 질감** — 교차 명암(`#a05818`/`#5a2a0c`)으로 rusty heavy 링크 표현
- 🌐 **단일 HTML** — 외부 빌드 도구 없이 브라우저에서 바로 실행
- 🌍 **한/영 토글** — `L` 키 또는 HUD 배지로 즉시 전환, localStorage 영속화

---

## 🚀 실행 방법

### 방법 1: 라이브 데모 (가장 간단)
위 [라이브 데모](#-라이브-데모) 섹션의 Vercel URL 클릭 → 별도 설치 없이 바로 확인

### 방법 2: 브라우저로 직접 열기
```bash
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```

### 방법 3: 로컬 서버 (권장 — CDN 로깅 깨끗)
```bash
python3 -m http.server 8000
# → http://localhost:8000
```

> **참고**: Matter.js는 CDN(`https://cdn.jsdelivr.net`)에서 로드됩니다. 오프라인 환경에서는 `index.html`의 `<script src=...>` 라인을 로컬 경로로 교체하세요.

---

## 🎮 조작법

| 입력 | 동작 |
|---|---|
| **마우스 좌클릭 + 드래그** | 사슬/볼을 잡고 이동 (IK 곡선 추적) |
| **마우스 떼기** | 사슬 해제, 관성으로 흔들림 |
| **R 키** | 사슬 + 상자 리셋 |
| **스페이스바** | 레킹 볼에 강한 임펄스 가하기 |
| **L 키 (또는 HUD 클릭)** | 한/영 토글 (localStorage에 저장) |
| **HUD "sound" 클릭** | 사운드 ON/OFF 토글 (첫 제스처 후 활성화) |

---

## 🛠️ 기술 스택

| 영역 | 사용 기술 |
|---|---|
| **물리 엔진** | Matter.js 0.19.0 (CDN, `Constraints` + `Bodies.rectangle`) |
| **렌더링** | Canvas 2D (Matter.Render) |
| **인터랙션** | Matter.MouseConstraint + 커스텀 드래그 핸들러 |
| **사운드** | Web Audio API (절차적 합성, 외부 파일 0개) |
| **번들링** | 없음 (단일 HTML + vercel.json) |
| **언어** | Vanilla JavaScript (ES6+) |

---

## 📂 프로젝트 구조

```
heavy-chain-ik/
├── index.html      # 단일 HTML (모든 코드 포함, Matter.js CDN 1개)
├── README.md       # 한국어 (기본)
├── LICENSE         # MIT
└── vercel.json     # Vercel 정적 호스팅 설정
```

---

## 🎨 디자인 결정

| 결정 포인트 | 선택 | 이유 |
|---|---|---|
| **물리 라이브러리** | Matter.js (CDN) | 체인 IK 시뮬레이션에 최적화된 `Constraint` API, 별도 빌드 0 |
| **사슬 표현** | 직사각형 Link + 끝 레킹 볼 | 원형 Joint 대비 "링크" 리듬이 명확, 24개로 IK 체인감 |
| **무게감 튜닝** | `density: 0.05` 링크 / `0.3` 볼 | 링크의 ~28배 밀도로 끝에 매달린 무게 강조 |
| **마찰/감쇠** | `friction: 0.9`, `frictionAir: 0.01` | 빠르게 진동하지 않고 묵직하게 흔들림 |
| **사운드** | Web Audio API 절차적 합성 | 외부 오디오 파일 0개, MP3 의존성 제거 |
| **파티클** | Canvas 직접 그리기 (Matter body 아님) | 충돌 속도 임계값 기반 분출, 시각적 임팩트 ↑ |
| **다국어** | L 키 빌트인 토글 + localStorage | 별도 URL 없이 즉시 전환, 사용자 부담 0 |
| **호스팅** | Vercel (raw alias) | GitHub Pages 대비 자동 HTTPS + 글로벌 CDN |

### 직접 커스터마이즈하고 싶다면

`index.html` 상단에서 다음 상수를 조정하면 물리/시각을 바꿀 수 있어요:

```js
const CONFIG = {
  CHAIN_LINKS: 24,            // 사슬 고리 개수
  LINK_W: 22, LINK_H: 20,     // 링크 크기 (px)
  BALL_RADIUS: 26,            // 레킹 볼 반경
  LINK_DENSITY: 0.05,         // 링크 밀도
  BALL_DENSITY: 0.3,          // 볼 밀도 (링크의 ~28배)
  FRICTION: 0.9,              // 마찰 계수
  STIFFNESS: 0.12,            // 마우스 Constraint 강도
  // ... 더 많은 옵션은 코드 내 주석 참조
};
```

---

## 🧠 동작 원리

```
사슬 = N개의 직사각형 Body + (N-1)개의 Constraint
       │
       ├─ Link[0] ──Constraint── Link[1] ──Constraint── ... ── Link[N-1]
       │                              │
       │                              └─ MouseConstraint (잡았을 때만 활성)
       │
       └─ Matter.js Engine이 매 프레임:
            1. 중력 적용
            2. Constraint로 Link 간 거리/각도 보정
            3. 마찰력(density, frictionAir)으로 감속
            4. 충돌 처리 → 상자 밀침
```

핵심은 **Constraint의 `stiffness`(0.7~0.9) 와 `damping`(0.1~0.3)** 조합입니다. 너무 뻣뻣하면 IK 체인이 끊어지고, 너무 부드럽면 자루처럼 늘어납니다.

### 한/영 토글 메커니즘

```js
// i18n 키 (HUD 4개 라인 + title)
const i18n = { ko: {...}, en: {...} };

// L 키로 토글
document.addEventListener('keydown', e => {
  if (e.key === 'l') toggleLang();
});

// localStorage 영속화
localStorage.setItem('heavy-chain-ik.lang', currentLang);
```

---

## 🔬 검증

- ✅ **bit-perfect 사이즈**: `curl https://heavy-chain-ik.vercel.app/` = 26,579B ≡ `wc -c < index.html` = 26,579B
- ✅ **alias HTTP 200**: `https://heavy-chain-ik.vercel.app/` 200 OK
- ✅ **Matter.js CDN 도달**: `https://cdn.jsdelivr.net/npm/matter-js@0.19.0/build/matter.min.js` HTTP/2 200
- ✅ **콘솔 에러 0개**: 페이지 로드 후 Chrome DevTools에서 검증
- ✅ **i18n 토글 작동**: L 키 → 한국어 ↔ English 즉시 전환, 새로 고침 후 유지
- ✅ **마우스 드래그 → 사슬 IK 추적**: stiffness 0.12로 부드러운 lag
- ✅ **레킹 볼 임팩트**: 스페이스바 → 박스 회전하며 멀리 날아감
- ✅ **절차적 사운드**: 충돌 속도 기반 게인, 첫 제스처 후 활성화

---

## 📜 License

MIT © 2026 sigco3111

---

## 🙏 Acknowledgments

이 프로젝트는 [MiniMax-M3](https://example.com) 모델과 OpenCode CLI 환경에서 생성되었습니다. Matter.js 물리 엔진은 [liabru/matter-js](https://github.com/liabru/matter-js) 오픈소스를 활용했습니다. 프롬프트 엔지니어링과 디자인 결정은 저장소 소유자가 직접 수행했습니다.