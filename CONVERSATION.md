# api-job-finder — Conversation Log

## Changes made

### Session 1 — Initial fixes (3 bugs)
- **Arbeitnow search param**: Added `&search=` query to API URL
- **Error i18n**: Added `error_loading` key to all 5 languages, used in catch block
- **Hardcoded French perf line**: Added `perf` i18n key with `{n}{t}{a}{f}{c}{r}` placeholders

### Session 2 — Added Careerjet + Remotive APIs
- Added Careerjet (later replaced) and Remotive as 3rd/4th API sources
- CSS badges, normalize functions, search functions, i18n updates

### Session 3 — Replaced Careerjet → RemoteOK
- Careerjet requires an API key (Basic Auth), not usable client-side
- Replaced with RemoteOK (`remoteok.com/api`) — free, public, no key

### Session 4 — switchLang not updating rendered content
- Added `lastPerfStats` to store search stats
- Added `updatePerfInfo()` to rebuild perf line on language switch
- Added `renderJobs()` call in `switchLang()` to re-render job cards

### Session 5 — Fix CORS (Failed to fetch)
- Freehire, RemoteOK, Remotive blocked by CORS in browser
- Added Vercel `rewrites` to proxy API calls server-side
- Changed API endpoints to `/api/proxy/*` (same origin, no CORS)

## Final 4 APIs
| Source | Endpoint | Type | Access |
|--------|----------|------|--------|
| Arbeitnow | `arbeitnow.com/api/job-board-api` | EU jobs | Direct (CORS `*`) |
| Freehire | `/api/proxy/freehire` → `freehire.dev` | Global | Via Vercel proxy |
| RemoteOK | `/api/proxy/remoteok` → `remoteok.com` | Remote | Via Vercel proxy |
| Remotive | `/api/proxy/remotive` → `remotive.com` | Remote | Via Vercel proxy |
