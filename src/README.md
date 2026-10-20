# SGIA Connect (DEMO prototype)

Working PWA prototype of a membership app for the Singapore Indian Association. **Synthetic data only. Not an official SGIA credential.**

Stack: Next.js 16 (App Router) · React 19 · TypeScript · Tailwind 4 · PostgreSQL (embedded PGlite locally, any managed Postgres via `DATABASE_URL`) · bcrypt + server-side sessions · `qrcode` / `html5-qrcode` · `web-push` (VAPID) · service worker.

## Run locally
```bash
npm install
cp .env.example .env.local        # fill APP_URL, VAPID keys (npx web-push generate-vapid-keys), CRON_SECRET
npm run db:reset                  # creates schema + 43 fictional members; writes .secrets/demo-credentials.md (git-ignored)
npm run build && npm start        # http://localhost:3000
```
## Test
```bash
npm test                          # unit tests (vitest)
bash tests/run-e2e.sh             # 88 end-to-end checks against a throwaway DB + production server on :3100
```
Evidence: `docs/test-evidence/`. Full handover: `docs/HANDOVER.md`.

## Layout
`src/app/(app)` authenticated pages · `src/app/api` JSON APIs (every handler enforces role server-side via `api([...roles], …)`) · `src/lib` db, auth, status, push, admin jobs · `public/sw.js` service worker · `scripts/seed.ts` synthetic data.
