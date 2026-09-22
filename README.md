# Maziyar Habibkhoda — Portfolio

A standard Vite + React + TypeScript + Tailwind app. No Manus-specific tooling, no backend server required.

## Run it

```bash
npm install
npm run dev       # http://localhost:3000
npm run build     # outputs to /dist
npm run preview   # preview the production build
```

## ⚠️ One thing you need to fix: the case-study images

The original Manus export linked images through Manus's own hosting
(`/manus-storage/...`), and those actual image files were **not** included in
the exported zip — only the links to them. So this version ships with plain
color placeholder images in `public/images/` just so the site renders without
broken-image icons.

To use your real screenshots:

1. Get the original files back from Manus — open the project there and look for
   an "Assets" / "Files" panel, or right-click each image in the case-study
   pages and save it.
2. Drop them into `public/images/`, using these exact filenames (or edit the
   paths in `src/App.tsx` under `export const assets = {...}` to match
   whatever you name them):

   - `autumn-01-foundations.png`
   - `autumn-02-components.png`
   - `autumn-03-buttons.png`
   - `autumn-04-navigation.png`
   - `winter-01-old-home.png`
   - `winter-02-new-home.png`
   - `spring-01-old-upload.png`
   - `spring-02-new-upload.png`
   - `spring-03-qr-scanner.png`
   - `spring-04-empty-upload.png`
   - `summer-01-old-settings.png`
   - `summer-02-old-query.png`
   - `summer-03-new-settings.jpg`
   - `summer-04-dashboard.png`
   - `summer-05-new-report.jpg`

## What changed from the Manus export

- **Flattened the folder structure.** Manus split the project into `client/`
  (frontend) and `server/` (a tiny Express server that only served the built
  files). That split is only useful if you deploy to a Node host. Since this
  is a static site, everything now lives at the project root like a normal
  Vite app (`src/`, `public/`, `index.html` at the top level), and the
  Express server + `server/`, `shared/`, `dist/index.js` are gone.
- **Removed Manus-only dev tooling** from `vite.config.ts`: the debug-log
  collector, the JSX source-location plugin, the `manus-storage` proxy, and
  the `manus.computer` dev-host allowlist. None of that does anything outside
  Manus's own environment.
- **Removed unused leftover boilerplate**: `ManusDialog.tsx` and `Map.tsx`
  (unused components), `const.ts` / `shared/const.ts` (an OAuth login helper
  the portfolio never calls), and the `__manus__` debug script in `public/`.
- **Switched from pnpm to plain npm** and dropped the `wouter` patch — it only
  existed to feed Manus's internal route-tracking, which you don't need.
- **package.json / build script** simplified: `vite build` alone, no bundling
  a server with esbuild.
- Removed the placeholder analytics `<script>` tag in `index.html` (it pointed
  at unset Manus env vars and would've been a dead reference).

Everything else — every page, component, and all your actual case-study copy —
is untouched.

## Deploying

Since this is a plain static site, you can deploy the contents of `dist/`
(after `npm run build`) to Vercel, Netlify, GitHub Pages, Cloudflare Pages, or
any static host. No server process needed.
