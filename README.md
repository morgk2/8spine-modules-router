# 8spine-modules-router

Simple Vercel router that redirects **all traffic** to `https://8spine-modules.pages.dev` (path-preserving, 308 Permanent).

## How it works

- `vercel.json` → `redirects`: `/(.*)` → `https://8spine-modules.pages.dev/$1` (`permanent: true` = 308)
- `public/index.html` → fallback `<meta refresh>` + `location.replace()` in case edge redirect is bypassed

## Add custom routes later

Add entries **before** the catch-all in `vercel.json`:

```json
{
  "redirects": [
    { "source": "/docs", "destination": "https://8spine-modules.pages.dev/docs", "permanent": false },
    { "source": "/(.*)", "destination": "https://8spine-modules.pages.dev/$1", "permanent": true }
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
# then: curl -I http://localhost:3000/some-path
# expect: 308 Location: https://8spine-modules.pages.dev/some-path
```
