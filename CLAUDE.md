# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

The GitHub Pages site for the **RunCat Developers** GitHub Organization (`runcat-dev`), served at `https://runcat-dev.github.io/`. It is an onboarding page introducing the community and its projects (RunCat Neo for macOS, RunCat 365 for Windows, gba-runcat, playdate-runcat).

## Stack: lobster.js (no build step)

The site is three static files plus images. There is no bundler, package manager, test suite, or build pipeline. [lobster.js](https://hacknock.github.io/lobsterjs/) is a browser-side Markdown renderer imported as an ES module from the upstream CDN — it fetches `content.md` at runtime and renders it into `#content`, producing semantic HTML where every element carries a predictable `lbs-*` class.

### File responsibilities

- `index.html` — lobster.js shell. The body is essentially `<div id="content"></div>` plus the module import. **Do not restructure** — all content lives in `content.md`.
- `content.md` — every word of page copy, in lobster.js extended Markdown (`:::header`, `:::footer`, `:::warp`, `:::details`, sized images via `=96x`).
- `style.css` — targets the `lbs-*` class hierarchy that lobster.js emits. No JS, no inline styles.

## Local preview & deployment

```sh
python3 -m http.server 8000   # then open http://localhost:8000/
```

`file://` will not work — `fetch('./content.md')` requires HTTP.

Deployment is **`git push origin main`**. GitHub Pages (Source = `main` / root) rebuilds automatically; no Actions workflow is involved. The `<org>.github.io` repo name makes this the org's root site, so relative paths (`./content.md`, `./style.css`, `./images/...`) resolve at `https://runcat-dev.github.io/` without a sub-path prefix.

## lobster.js gotchas to respect

These constraints come from lobster.js's HTML output. If the `lobster-init` and `lobster-css` skills are installed, they hold the full syntax reference.

- **Warp multi-column grids** (`:::warp col-name` blocks declared via `~ | [~col-a] | [~col-b] |`) render inside `<thead><tr><th>`, **not** `<tbody><tr><td>`. CSS for cards must target `.lbs-table-silent th`. Never apply `display: none` to `thead` on silent tables — it hides all Warp content.
- Do not use `border-collapse: separate` + `border-spacing` on silent tables. The current `style.css` uses `display: grid` on the `tr` to get column gaps without breaking layout, plus `:has(th:nth-child(3))` to flip from a 2-column row to 3 columns automatically when a third card is present.
- The lobster.js base URL is `https://hacknock.github.io/lobsterjs/` — never include a `docs/` segment.

## Page voice & policy (already encoded in content.md)

If you edit `content.md`, the page's own **Philosophy** section is the editorial rulebook: *Simple, Cute, Useful* — hobby software for the general public, not power users. Keep copy short, friendly, non-technical.

The **Discord** section is explicit that Discord is for contributor teamwork only; bug reports and feature requests must stay on GitHub Issues / Pull Requests. Preserve this distinction in any copy changes.
