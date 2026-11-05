# Threadboard product site

Static HTML, CSS, and a small JavaScript module. Dark is the first-visit default; the theme toggle remembers a local preference and switches the diagrams and actual product captures together. The site works with its bundled scripts and fonts. In production, Cloudflare adds its privacy-preserving Web Analytics beacon; the content security policy allows that script and its same-origin `/cdn-cgi/rum` endpoint.

The hero is the real `src/ui/main.tsx` app and its original stylesheet, compiled with a website-only transport. The demo uses example cards in browser memory: visitors can create, edit, move, archive, filter, and review tasks or simulate a chat handoff. These actions stay in the browser and make no MCP calls, real Codex chats, model requests or database writes. Reset restores the examples. The page theme also switches the live app. To regenerate the fixture after changing the product examples, run `npx tsx site/scripts/seed-demo.ts` from the repository root.

```sh
npm ci
npm ci --prefix site
npm run build
npm run verify --prefix site
npm run dev --prefix site
```

The local preview is `http://127.0.0.1:4400`. Run `npm test --prefix site` for theme persistence, keyboard handoffs, screenshots, installation commands, package checksums, accessibility, and responsive layouts from 320 to 1440 pixels. Use `npm run graphics --prefix site` to regenerate the social card from its editable SVG. Chromium is required: `npx playwright install chromium`.

Build output is `site/dist/`. The build copies the current real UI captures from `docs/images/`, self-hosts Instrument Sans with its OFL license, and packages the compiled plugin with its verified installer. ZIP generation runs in Node using a build-only dependency, so the host needs no system ZIP utility. The website ZIP and checksum are always generated from the same source version. Regenerate product captures with the repository's `npm run graphics` before rebuilding the site.

Cloudflare Pages project: `threadboard-web`. GitHub source: `vrnrn/Threadboard`, production branch `main`, root `site`, build command `npm run verify`, output `dist`, Node 24. Public domain: `threadboard.vrnrn.com`.

Download and checksum URLs include the package content hash. This keeps cached preview downloads matched to their checksum even when two source builds share a preview version.

Styles, scripts, demo pages, and product images carry a build content hash in their URLs. Returning visitors receive the matching assets after a deployment, including when switching themes or resetting the demo.

The website is independent of Threadboard's fully local runtime. Hosting the page and downloadable installer does not introduce board synchronization or a hosted MCP server.
