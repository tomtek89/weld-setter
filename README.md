# Weld Setter — PWA package

This folder is a complete, installable Progressive Web App. It's the same
Weld Setter app, packaged so it can be self-hosted and then submitted to
Google Play and the Microsoft Store.

## What's inside

- `index.html` — the app (standalone document, not the Claude-artifact version)
- `manifest.json` — PWA manifest (name, icons, colors, display mode)
- `sw.js` — service worker for offline support
- `icons/` — app icons (192px, 512px, maskable variants, Apple touch icon)

## Step 1 — Host it on your own domain (required)

App stores need this served over HTTPS from a domain you control — a
`claude.ai` link won't work. Easiest free options:

- **GitHub Pages**: create a repo, upload these files, turn on Pages in
  repo Settings → Pages. You'll get a URL like
  `https://yourname.github.io/weld-setter/`.
- **Netlify** or **Vercel**: drag-and-drop this folder onto
  [app.netlify.com/drop](https://app.netlify.com/drop) (or connect a repo)
  for an instant HTTPS URL.
- **Cloudflare Pages**: similar drag-and-drop flow.

Any of these works — just note the final URL, you'll need it in Step 2.

## Step 2 — Verify it's a valid, installable PWA

Open your hosted URL in Chrome, then run it through
[PWABuilder.com](https://www.pwabuilder.com) — paste in your URL and it
will check the manifest, service worker, icons, and HTTPS setup, and flag
anything missing (it may suggest a higher Lighthouse score before Google
Play will accept it — that's a quality bar Google enforces, not something
this package can pre-solve for you).

## Step 3 — Package for each store

Still on PWABuilder.com, after your PWA passes its checks:

- **Google Play**: click "Package for Stores" → Android. It generates a
  signed `.aab` file (via Google's Bubblewrap tool under the hood) ready
  to upload to [Google Play Console](https://play.google.com/console)
  (requires a one-time $25 developer registration fee).
- **Microsoft Store**: same page → Windows. It generates an `.msix`
  package for [Partner Center](https://partner.microsoft.com/dashboard)
  (individual developer registration is currently free).

## Step 4 — Submit

Upload the generated package in each store's console, fill in the store
listing (screenshots, description, privacy policy URL — you'll need a
simple privacy policy page even for an app that collects no data), and
submit for review. Google Play review is typically hours to a couple of
days; Microsoft Store is usually similar.

## Notes

- The service worker caches the app shell so it keeps working offline
  after the first load.
- If you update the app later, bump `CACHE_NAME` in `sw.js` (e.g.
  `weld-setter-v2`) so returning users get the new version instead of a
  stale cached copy.
- The calculator data and all content are unchanged from the Claude
  artifact version — this is purely a packaging step.
