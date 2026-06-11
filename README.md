# runcat-dev.github.io

The GitHub Pages site for the [RunCat Developers](https://github.com/runcat-dev) organization, served at <https://runcat-dev.github.io/>.

It is an onboarding page introducing the community and its projects (RunCat Neo for macOS, RunCat 365 for Windows, gba-runcat, playdate-runcat).

## Stack

The site is built with [lobster.js](https://hacknock.github.io/lobsterjs/), a browser-side Markdown renderer. There is no build step — all page copy lives in `content.md`, which lobster.js fetches and renders at runtime.

- `index.html` — lobster.js shell
- `content.md` — page content (lobster.js extended Markdown)
- `style.css` — styles targeting lobster.js's `lbs-*` classes

## Local preview

```sh
python3 -m http.server 8000   # then open http://localhost:8000/
```

`file://` will not work — lobster.js fetches `content.md` over HTTP.

## Deployment

Push to `main`. GitHub Pages (Source = `main` / root) rebuilds automatically.

## License

Released under the [MIT License](./LICENSE).
