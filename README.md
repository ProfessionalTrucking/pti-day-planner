# PTI Day Planner — Setup

A standalone, installable day planner for PTI instructors. No database, no accounts.
Each instructor's data is saved on their own phone (in the browser), so it stays private to them.

## Files
- `index.html` — the app
- `manifest.webmanifest` — makes it installable as a home-screen app
- `service-worker.js` — caches the app so it works offline
- `icon-*.png` — app icons (navy/gold PTI mark)

## Hosting it (required for the "app" behavior)
A PWA must be served over **HTTPS** from a web address — it will not install when opened
as a local file. Any static host works. Options:

- **GitHub Pages** — push this folder to a repo, enable Pages. Done.
- **A static route on your existing Railway service** — drop the folder in and serve it
  (e.g. `app.use(express.static('pti-planner'))`), then point a URL at it.
- Netlify / Cloudflare Pages / Vercel — drag-and-drop the folder.

Make sure all files sit in the **same folder** and are served from the same path,
since the manifest and service worker use relative URLs.

## Installing on a phone (instructors)
1. Open the hosted URL in the phone browser.
   - iPhone: **Safari**
   - Android: **Chrome**
2. **iPhone:** tap the Share button → **Add to Home Screen** → Add.
   **Android:** tap the ⋮ menu → **Install app** (or **Add to Home screen**).
3. A "PTI" icon appears on the home screen. Tapping it opens the planner full-screen,
   like a native app — and it works without a signal once loaded.

## Updating the app later
Edit the files and re-upload. Bump the cache name in `service-worker.js`
(e.g. `pti-planner-v1` → `pti-planner-v2`) so phones pick up the new version.

## Note on data
Data lives in each phone's browser storage. Clearing the browser's site data,
or removing the app, clears that phone's entries. There is no shared/central copy —
that would require the database connection, which this build intentionally does not use.
