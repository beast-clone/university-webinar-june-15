# goocampus-domain-hub

The source for **`goocampusevents.com`** — the homepage and every country landing page that lives under it.

This repo is connected to the Netlify project `goocampus-university-webinar` (the project name is historical — don't be fooled by it). Every push to `main` auto-deploys to `goocampusevents.com`.

## Layout

| Path on goocampusevents.com | Where it lives in this repo |
|---|---|
| `/` | `index.html` (the "Global Opportunities for Doctors Abroad" homepage) |
| `/amc-pathway/*` | `amc-pathway/` folder — Astro build output of [`beast-clone/amc-blueprint-landing`](https://github.com/beast-clone/amc-blueprint-landing) |
| `/nz-pathway/*` | `nz-pathway/` folder — Astro build output of [`beast-clone/nz-pathway`](https://github.com/beast-clone/nz-pathway) |

Every country page is **physically inside this repo**, so a Git deploy never wipes anything. One repo, one source of truth.

## How to update each section

### Homepage
Edit `index.html` directly. Push. Live in ~30 seconds.

### `/amc-pathway/` (Australia)
1. Clone or pull [`beast-clone/amc-blueprint-landing`](https://github.com/beast-clone/amc-blueprint-landing)
2. Make sure `astro.config.mjs` has `base: '/amc-pathway'`
3. `npm install && npm run build`
4. Copy contents of `dist/` into this repo's `amc-pathway/` folder (replacing existing files)
5. Commit and push this repo

### `/nz-pathway/` (New Zealand)
1. Clone or pull [`beast-clone/nz-pathway`](https://github.com/beast-clone/nz-pathway)
2. Make sure `astro.config.mjs` has `base: '/nz-pathway/'`
3. `npm install && npm run build`
4. Copy contents of `dist/` into this repo's `nz-pathway/` folder (replacing existing files) — **do not copy the `_redirects` file from the NZ build, it isn't needed here**
5. Commit and push this repo

## Adding a new country

1. Build the country landing page in its own GitHub repo (e.g. `beast-clone/uk-pathway`).
2. Configure Astro with `base: '/uk-pathway/'`.
3. Build it (`npm run build`).
4. Copy `dist/*` into this repo as `uk-pathway/` folder.
5. Commit and push. Live at `goocampusevents.com/uk-pathway/` in ~1 minute.

That's it. No Netlify dashboard work, no proxy rules, no separate sites to manage.

## About `_redirects`

The `_redirects` file at the repo root is currently empty (just comments). Add proxy rules there only if a country launches as a separate Netlify site instead of being baked in. The "physically inside this repo" pattern is preferred.
