# Fly Swift Tail — Semi‑Private Form Demo

A static, mobile‑first demo page to capture intent for **semi‑private (book‑by‑the‑seat) flights**. It ships as plain HTML/CSS/JS so you can upload to GitHub and deploy to Vercel quickly.

## Files
- `index.html` — main search form (prefills origin from `?city=`).
- `explore/index.html` — placeholder for the AI "Explore deals" page.
- `results/index.html` — shows submitted payload (for demo).
- `vercel.json` — optional routing niceties.

## Local preview
Just open `index.html` in a browser. Try adding `?city=Islip` to prefill the origin.

## Deploy (GitHub → Vercel)

### 1) Create a new GitHub repo
1. Go to GitHub → New repository → name it **fst-semi-private-form-demo** (public is fine).
2. Do **not** initialize with README (we already provide one), or do it and replace later.

### 2) Upload files
Drag & drop the contents of this folder into the repo root:
```
index.html
explore/index.html
results/index.html
vercel.json
README.md
```
Commit to `main`.

### 3) Import to Vercel
1. Log in to Vercel → **Add New… → Project** → **Import Git Repository**.
2. Select your new repo.
3. Framework preset: **Other** (static site). No build command. Output directory: **/** (root).
4. Click **Deploy**.

Vercel will give you a preview URL like `https://fst-semi-private-form-demo.vercel.app/`.

### 4) Test
- Open the URL and try the form. You’ll be redirected to `/results` which echoes your payload.
- Try `?city=Islip` to prefill origin.

### 5) Wire real endpoints (Istvan)
- On submit, `index.html` currently does a simple redirect.
- Replace that with:
```js
await fetch('/api/leads', { method: 'POST', headers: { 'Content-Type': 'application/json' }, body: JSON.stringify(payload) });
location.href = '/results?lead_id=...';
```
- Add Slack/email fan‑out and store the alert if `flex=true`.

## Routing notes
- We included `vercel.json` to ensure clean paths like `/explore` and `/results` work as folders.
- Keep everything static until the feed is ready.
