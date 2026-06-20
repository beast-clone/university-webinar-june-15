# goocampus-domain-hub

The source for **`goocampusevents.com`** — the homepage and the routing rules that send visitors to country-specific landing pages.

This repo is connected to the Netlify project `goocampus-university-webinar` (the project name is historical — don't be fooled by it). Every push to `main` auto-deploys to `goocampusevents.com`.

## What lives here

| File | What it does |
|---|---|
| `index.html` | The actual homepage of `goocampusevents.com` ("Global Opportunities for Doctors Abroad") |
| `_redirects` | Routing rules — sends visitors of `/nz-pathway/*` and similar paths to the standalone landing pages |
| `GC Logos.png`, `WhatsApp Image …jpeg` | Assets used by the homepage |

## What does NOT live here

The country landing pages **are not in this repo.** They are independent deployments — this repo only forwards visitors to them.

| Path on goocampusevents.com | Where the actual page lives |
|---|---|
| `/` | this repo (`index.html`) |
| `/amc-pathway/*` | a separate AMC deployment (set up earlier by the team) |
| `/nz-pathway/*` | repo: [`beast-clone/nz-pathway`](https://github.com/beast-clone/nz-pathway) → Netlify project: `goocampus-nz-pathway` → URL: `goocampus-nz-pathway.netlify.app` |

So you can think of this repo as a **mailroom**: it greets visitors at the front door and decides which country page to send them to.

## How to add a new country (template)

1. Build the country landing page in its own GitHub repo (e.g. `beast-clone/uk-pathway`).
2. Deploy it to its own Netlify project (e.g. `goocampus-uk-pathway`).
3. Add a single line to this repo's `_redirects` file:
   ```
   /uk-pathway/*  https://goocampus-uk-pathway.netlify.app/:splat  200!
   ```
4. Push. Netlify auto-deploys this repo. `goocampusevents.com/uk-pathway/` is live in ~1 minute.

The new country landing page must also build with Astro `base: '/uk-pathway/'` and include its own internal rewrite (`/uk-pathway/*  /:splat  200!`) so assets resolve correctly. See `beast-clone/nz-pathway` for the pattern.

## Current `_redirects`

```
/nz-pathway/*  https://goocampus-nz-pathway.netlify.app/:splat  200!
```

Add more rules below the existing one — one line per country.
