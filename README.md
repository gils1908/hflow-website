# hflow-website

Static marketing site (`index.html` + React via Babel in the browser).

**Public URLs (Vercel project `hflow-website`):** [https://www.hflow.pro](https://www.hflow.pro/), [https://web.hflow.pro](https://web.hflow.pro/), [https://hflow-website-sigma.vercel.app](https://hflow-website-sigma.vercel.app/) (apex `hflow.pro` redirects to `www`). Pushing `main` redeploys.

The demo form’s **`<meta name="hflow-api-origin">`** in `index.html` is set to **`https://app.hflow.pro`** (no trailing slash). On the **hFlow app** Vercel project (`app.hflow.pro`), **`DEMO_REQUEST_ALLOWED_ORIGINS`** must include **every** marketing origin users load the page from (see below), or the browser blocks the request (CORS).

## Request a demo

The demo form POSTs to the main hFlow Next.js app.

1. **API URL:** In [`index.html`](index.html), set the **`<meta name="hflow-api-origin" content="…">`** tag to your deployed app origin with **no trailing slash** (e.g. `https://app.hflow.pro` or your `*.vercel.app` URL).  
   - If you omit the meta **and** open the site from `localhost` / `127.0.0.1`, the form uses `http://localhost:3000`.  
   - **HTTPS marketing pages cannot call `http://localhost`** (browser security); you must point the meta at a live **https** app URL.

2. **CORS:** On the **app** project Vercel env (`app.hflow.pro`), set **`DEMO_REQUEST_ALLOWED_ORIGINS`** to a comma-separated list of marketing **origins** (scheme + host; trailing slashes are OK and are normalized server-side). Include at least:
   - `https://www.hflow.pro`
   - `https://web.hflow.pro`
   - `https://hflow-website-sigma.vercel.app`
   - Optional: `https://hflow.pro` (apex; usually redirects to `www`)
   
   Example: `https://hflow-website-sigma.vercel.app,https://www.hflow.pro,https://web.hflow.pro,https://hflow.pro`

3. Optional: **`DEMO_REQUEST_TO`**, notification inbox (defaults to `hflow@hflow.pro`).

The app needs **`RESEND_API_KEY`**, **`RESEND_FROM`**, and **`SUPABASE_SERVICE_ROLE_KEY`**; apply migrations for `demo_request_submissions` (base `20260429180000_demo_request_submissions.sql`, optional `phone` `20260429213000_add_demo_request_phone.sql`). The form posts `name`, `email`, `school`, and optional `phone`.

### If the form shows a connection / CORS error

- Confirm **`hflow-api-origin`** matches your real Next deployment (HTTPS if the marketing site is HTTPS).
- Confirm **`DEMO_REQUEST_ALLOWED_ORIGINS`** on Vercel includes your marketing URL exactly (including `www` vs bare domain).
