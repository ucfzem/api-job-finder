# api-job-finder — Conversation Log

## Changes made

### Session 1 — Initial fixes (3 bugs)
- **Arbeitnow search param**: Added `&search=` query to API URL
- **Error i18n**: Added `error_loading` key to all 5 languages, used in catch block
- **Hardcoded French perf line**: Added `perf` i18n key with placeholders

### Session 2 — Added Careerjet + Remotive APIs
- Added Careerjet (later replaced) and Remotive as 3rd/4th API sources

### Session 3 — Replaced Careerjet → RemoteOK
- Careerjet requires API key, not usable client-side
- Replaced with RemoteOK (free, public, no key)

### Session 4 — switchLang not updating rendered content
- Added `lastPerfStats` + `updatePerfInfo()` + re-call `renderJobs()`

### Session 5 — Fix CORS with Vercel rewrites
- Added Vercel `rewrites` to proxy API calls server-side (didn't work for static)

### Session 6 — Stripped to only Arbeitnow
- Vercel external rewrites don't work for `framework: null`
- Removed all non-CORS sources, kept only Arbeitnow

### Session 7 — Proper Vercel serverless proxy + 4 sources
- Created `api/proxy.js` serverless function — proxies requests server-side (always works)
- Added Himalayas (free, no key, supports keyword + countryCode filter)
- Added RemoteOK (free, no key, slices off first notice array element)
- Restored Remotive (free, no key)
- All non-CORS APIs route through `/api/proxy?url=ENCODED_URL`
- Dynamic perf line — builds per-source counts dynamically from stats object
- Corrected normalizeHimalayas to match actual API fields (companyName, locationRestrictions, applicationLink, employmentType, category, pubDate)

## Current Sources
| Source | Endpoint | Access |
|--------|----------|--------|
| Arbeitnow | `arbeitnow.com/api/job-board-api` | Direct (CORS `*`) |
| Himalayas | `himalayas.app/jobs/api/search` | Via serverless proxy |
| RemoteOK | `remoteok.com/api` | Via serverless proxy |
| Remotive | `remotive.com/api/remote-jobs` | Via serverless proxy |
