# hflow-website

Static marketing site (`index.html` + React via Babel in the browser).

## Request a demo

The demo form POSTs to the main hFlow Next.js app:

1. In [`index.html`](index.html), set **`DEMO_REQUEST_API_BASE`** to the app origin with **no trailing slash** (e.g. `https://app.hflow.pro` or `http://localhost:3000` for local testing).
2. On the app, set **`DEMO_REQUEST_ALLOWED_ORIGINS`** to a comma-separated list of origins that may call the API from the browser (e.g. `https://www.hflow.pro,https://hflow.pro`). Include any local static-server origin you use (e.g. `http://127.0.0.1:8080`).
3. Optional: **`DEMO_REQUEST_TO`** — notification inbox (defaults to `hflow@hflow.pro`).

The app must have **`RESEND_API_KEY`**, **`RESEND_FROM`**, and **`SUPABASE_SERVICE_ROLE_KEY`** configured; apply migration `20260429180000_demo_request_submissions.sql` so the `demo_request_submissions` table exists.
