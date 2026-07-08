# 🪝 Heavy Chain IK (Inverse Kinematics)

> 화면 상단에 매달린 녹슨 쇠사슬을 마우스로 잡아당기거나 흔들어, 무거운 물리적 무게감으로 움직이고 화면 안 나무상자들을 무너뜨리는 인터랙티브 시뮬레이션.

---

## 🎬 라이브 데모 (Live Demo)

- **GitHub Pages**: https://sigco3111.github.io/heavy-chain-ik/ (배포 후 활성화)
- 로컬 실행: `index.html` 더블클릭 또는 `python3 -m http.server 8000`

---

## 🤖 생성 정보 (Attribution)

이 프로젝트의 코드는 **OpenCode CLI** + **MiniMax-M3** 모델로 생성되었습니다.

- **Tool**: [OpenCode](https://github.com/snymann/opencode) (AI 코딩 어시스턴트)
- **Model**: MiniMax-M3 (provider: minimax)
- **Generation mode**: 단일 HTML 임베드 (CDN 의존성 포함, 모든 의존관계 코드 1파일)

프롬프트 원문은 본 README 하단 "프롬프트 이력" 절 참조.

---

## ✨ 주요 특징 (Features)

- 🪝 **무거운 사슬 물리** — 각 고리(Link) 간 Constraints와 마찰력으로 묵직한 무게감 구현
- 🖱️ **마우스 드래그** — 사슬 끝(또는 임의 Link)을 잡고 이동
- ⚫ **레킹 볼** — 사슬 끝에 매달린 무거운 철구, 충돌 시 박스를 멀리 날려버림
- 🔊 **절차적 사운드** — Web Audio API로 쇠 '쨍' + 나무 '쿵' 합성, 충돌 속도 기반 게인
- 💨 **먼지 파티클** — 강한 임팩트 시 충돌 지점에서 wood-tone 먼지가 분출
- 📦 **파괴 가능한 나무상자** — 사슬로 쳐서 무너뜨리는 인터랙션
- 🦀 **녹슨 질감** — 직사각형 Link + density/friction 튜닝으로 "rusty heavy" 느낌
- 🌐 **단일 HTML** — 외부 빌드 도구 없이 브라우저에서 바로 실행

---

## 🚀 실행 방법 (Quick Start)

```bash
# 옵션 A: 브라우저에서 직접 열기
open index.html

# 옵션 B: 로컬 정적 서버 (권장 — CDN 로깅 깨끗)
python3 -m http.server 8000
# → http://localhost:8000 접속
```

> **참고**: Matter.js는 CDN(`https://cdn.jsdelivr.net`)에서 로드됩니다. 오프라인 환경에서는 `index.html`의 `<script src=...>` 라인을 로컬 경로로 교체하세요.

---

## 🎮 조작법 (Controls)

| 입력 | 동작 |
|---|---|
| **마우스 좌클릭 + 드래그** | 사슬/볼을 잡고 이동 (IK 곡선 추적) |
| **마우스 떼기** | 사슬 해제, 관성으로 흔들림 |
| **R 키** | 사슬 + 상자 리셋 |
| **스페이스바** | 레킹 볼에 강한 임펄스 가하기 |
| **L 키 (또는 HUD 클릭)** | 한/영 토글 (선택은 localStorage에 저장) |
| **HUD "sound" 클릭** | 사운드 ON/OFF 토글 (첫 제스처 후 활성화) |

---

## 🌐 다국어 (i18n)

기본 언어는 **한국어**. `L` 키 또는 HUD의 `[L]` 배지를 클릭하면 영어로 전환됩니다. 선택은 `localStorage['heavy-chain-ik.lang']`에 저장되어 새로 고침 후에도 유지됩니다.

번역 대상:
- 문서 제목 (`<title>`, `#title`)
- HUD 라인 4개 (drag, R, space, L)
- 사운드 상태 표시 + 툴팁
- document.title

---

## 🛠️ 기술 스택 (Tech Stack)

| 분류 | 선택 |
|---|---|
| **물리 엔진** | Matter.js (CDN, `Constraints` + `Bodies.rectangle`) |
| **렌더링** | Canvas 2D (Matter.Render) |
| **인터랙션** | Matter.MouseConstraint + 커스텀 드래그 핸들러 |
| **번들링** | 없음 (단일 HTML) |
| **언어** | Vanilla JavaScript (ES6+) |

---

## 🎨 디자인 결정 (Design Choices)

1. **단일 HTML 임베드** — `canvas-static-site-pipeline` 패턴 준수. CDN URL만 바꾸면 오프라인/내부 호스팅 즉시 전환 가능.
2. **사슬 = 직사각형 Link + 레킹 볼** — 24개의 22×20px 사각 링크, 끝에 radius 26px 철구. 교차 명암(`#a05818`/`#5a2a0c`)으로 "링크" 리듬 표현.
3. **density/friction 튜닝** — 링크 `density: 0.05` + `friction: 0.9` + `frictionAir: 0.01`, 볼 `density: 0.3` (링크의 ~28배). 묵직함의 핵심.
4. **마우스 Constraint 분리** — 사슬 끝/링크/볼 모두 잡기 가능, `stiffness: 0.12`로 적당한 lag.
5. **상자 = 정적/동적 혼합** — 바닥/벽은 정적, 무너질 나무상자는 동적 + `restitution: 0.1` (덜 튕김).
6. **절차적 사운드** — Web Audio API로 노이즈 burst(쨍) + 저주파 사인(쿵) 합성. 외부 오디오 파일 0개.
7. **커스텀 파티클** — Matter.js 바디가 아닌 캔버스 직접 그리기. 충돌 속도 임계값 넘으면 wood-tone 먼지 분출.

---

## 🧠 동작 원리 (How It Works)

```
사슬 = N개의 직사각형 Body + (N-1)개의 Constraint
       │
       ├─ Link[0]  ──Constraint── Link[1] ──Constraint── ... ── Link[N-1]
       │                              │
       │                              └─ MouseConstraint (잡았을 때만 활성)
       │
       └─ Matter.js Engine이 매 프레임:
            1. 중력 적용
            2. Constraint로 Link 간 거리/각도 보정
            3. 마찰력(density, frictionAir)으로 감속
            4. 충돌 처리 → 상자 밀침
```

핵심은 **Constraint의 `stiffness`(0.7~0.9) 와 `damping`(0.1~0.3)** 조합입니다. 너무 뻣뻣하면 IK 체인이 끊어지고, 너무 부드럽면 자루처럼 늘어집니다.

---

## 🔬 검증 (Verification)

- `python3 -m http.server`로 로컬 서빙 후 페이지 로드 확인
- 마우스 드래그 → 사슬이 따라옴
- 사슬 끝으로 상자 타격 → 상자 회전하며 넘어짐
- 콘솔 에러 0개 확인
- 비트-퍼펙트 사이즈: `curl -sS -w "%{size_download}" -o /dev/null http://localhost:8000/` ≡ `wc -c < index.html`

---

## 📝 프롬프트 이력 (Prompt Log)

원본 미션 지시 (2026-07-08):

> 화면 상단에 고정된 녹슨 쇠사슬을 마우스로 잡아당기거나 흔들 수 있는 시뮬레이션을 만들되, 각 사슬 고리(Link) 간의 물리적 제약(Constraints)과 마찰력을 정교하게 계산하여 묵직한 무게감이 느껴지도록 하고, 사슬로 화면에 있는 나무상자들을 쳐서 무너뜨릴 수 있는 인터랙티브 환경을 구현해줘.
>
> **Implementation Advice**: Use **Matter.js**. It creates excellent chain simulations using `Constraints` between bodies. Use rectangular bodies for links and adjust density/friction to simulate the heavy "rusty" feel. 모든 의존관계의 코드를 하나의 HTML에 담는 형태로 코드 작성.

---

## 📄 License

MIT