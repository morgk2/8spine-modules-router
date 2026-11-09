# 8spine-modules-router

Simple Vercel router that **proxies** all traffic to The Module Library at `https://8spine-modules.pages.dev` (path-preserving). The browser URL stays on the Vercel domain — no redirect.

## How it works

- `vercel.json` → `rewrites`: `/(.*)` → `https://8spine-modules.pages.dev/$1` (server-side proxy, URL unchanged)
- `public/index.html` → static "we've moved" notice page served at `/` (Vercel serves files before rewrites), with a link and button to The Module Library (deep-link paths preserved)

## Add custom routes later

Add entries **before** the catch-all in `vercel.json`:

```json
{
  "rewrites": [
    { "source": "/docs", "destination": "https://8spine-modules.pages.dev/docs" },
    { "source": "/(.*)", "destination": "https://8spine-modules.pages.dev/$1" }
  ]
}
```

## Deploy

1. Push to GitHub (already configured)
2. Import at https://vercel.com/new → select `8spine-modules-router` → Deploy (no build settings needed)
3. Optional: `npx vercel --prod` from this folder

## Test locally

```sh
npx vercel dev
# then: curl -i http://localhost:3000/index.json
# expect: 200 with the upstream JSON body (no Location header)
```
