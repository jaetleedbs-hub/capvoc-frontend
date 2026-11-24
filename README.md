# capvoc-frontend

CAPVOC 화면. **Vite + React** (Create React App 아님).

---

## 처음 체크아웃했다면

> 이 절은 **사람과 에이전트 모두** 이것만 보고 띄울 수 있게 쓰여 있다.
> 막히는 자리가 있으면 여기를 고친다 — 다음 사람이 같은 데서 막힌다.

```bash
yarn install
yarn dev            # http://localhost:18031
```

**설정 파일을 만들 필요가 없다.** 기본값이 `vite.config.js` 에 들어 있고,
그 값이 로컬 capvoc-backend 를 가리킨다.

### ★ `--port` 를 붙이지 않는다

```bash
yarn dev            # ⭕
vite --port 18030   # ⛔ capvoc-backend 의 포트를 뺏는다
```

CLI `--port` 가 `vite.config.js` 의 `18031` 을 이긴다. `18030` 으로 띄우면 이 dev 서버가
capvoc-backend 자리를 차지하고, `/api` 프록시 대상이 기본값 `localhost:18030` = **자기 자신**이
되어 요청이 제자리를 돌다 **500** 이 된다. `strictPort` 도 막지 못한다 —
백엔드가 안 떠 있으면 포트가 비어 있어 그냥 붙기 때문이다.

### 백엔드를 다른 곳으로 보내려면

| | |
|---|---|
| 손잡이 | **`VITE_PROXY_TARGET`** (기본 `http://localhost:18030`) |
| 어디에 | `.env.local` — **gitignore 대상이라 개인 설정용이다** |

```bash
echo 'VITE_PROXY_TARGET=http://172.20.30.212:61205' > .env.local
```

> ⚠ 저장소에 커밋된 `.env` 의 `REACT_APP_API_URL` 은 **효력이 없다.**
> Create React App 시절의 잔재이고, Vite 는 `VITE_` 접두만 읽는다.
> 그 값을 고쳐도 아무 일도 일어나지 않는다 — 위의 `VITE_PROXY_TARGET` 을 쓴다.

> ⚠ **`VITE_` 접두 값은 빌드 시 번들에 인라인된다** — 브라우저에서 그대로 보인다.
> 진짜 시크릿을 이 접두로 넣지 않는다.

### 짝이 되는 것

| | 포트 | 없으면 |
|---|---|---|
| capvoc-backend | 18030 | 화면은 뜨지만 모든 API 가 실패한다 |

capvoc-backend 기동은 그 저장소 README 의 **「처음 체크아웃했다면 — 환경설정」** 을 따른다
(거기서는 `.env` 를 만들어야 한다).

---

## 빌드

```bash
yarn build
yarn preview
```

---

## 규약

착수 전에 **`docs/CLAUDE.md`** 를 읽는다. 여기에 복사하지 않는다.
