# hflow-website

Static marketing site (`index.html` + React via Babel in the browser).

**Current public URL:** [https://hflow-website-sigma.vercel.app](https://hflow-website-sigma.vercel.app/) (Vercel). Pushing `main` redeploys it.

The demo form’s **`<meta name="hflow-api-origin">`** in `index.html` is set to **`https://app.hflow.pro`** (no trailing slash). With **`DEMO_REQUEST_ALLOWED_ORIGINS`** on the app including `https://hflow-website-sigma.vercel.app`, the form can POST cross-origin successfully.

## Request a demo

The demo form POSTs to the main hFlow Next.js app.

1. **API URL:** In [`index.html`](index.html), set the **`<meta name="hflow-api-origin" content="…">`** tag to your deployed app origin with **no trailing slash** (e.g. `https://app.hflow.pro` or your `*.vercel.app` URL).  
   - If you omit the meta **and** open the site from `localhost` / `127.0.0.1`, the form uses `http://localhost:3000`.  
   - **HTTPS marketing pages cannot call `http://localhost`** (browser security); you must point the meta at a live **https** app URL.

2. **CORS:** On the app (e.g. Vercel env for `app.hflow.pro`), set **`DEMO_REQUEST_ALLOWED_ORIGINS`** to every marketing **origin** (no path, no trailing slash). Right now the site may live at **[https://hflow-website-sigma.vercel.app](https://hflow-website-sigma.vercel.app/)**, so include at least:
   - `https://hflow-website-sigma.vercel.app`  
   When you move to a custom domain, **append** those origins too (comma-separated), e.g. `https://hflow-website-sigma.vercel.app,https://www.hflow.pro,https://hflow.pro`.

3. Optional: **`DEMO_REQUEST_TO`** — notification inbox (defaults to `hflow@hflow.pro`).

The app needs **`RESEND_API_KEY`**, **`RESEND_FROM`**, and **`SUPABASE_SERVICE_ROLE_KEY`**; apply migration `20260429180000_demo_request_submissions.sql` so `demo_request_submissions` exists.

### If the form shows a connection / CORS error

- Confirm **`hflow-api-origin`** matches your real Next deployment (HTTPS if the marketing site is HTTPS).
- Confirm **`DEMO_REQUEST_ALLOWED_ORIGINS`** on Vercel includes your marketing URL exactly (including `www` vs bare domain).
