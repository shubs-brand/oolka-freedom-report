# India's Financial Freedom Report — oolka.in page

The web edition of India's Financial Freedom Report, from Oolka. Lives at
**https://oolka.in/freedom-report**.

`index.html` + `assets/` + `FreedomReport.pdf`. The page renders complete with
no JavaScript; all motion and interaction sits behind an `html.js` gate inside
a reduced-motion guard.

## Build

This folder is BUILD OUTPUT, never hand-edited. The source of truth is the card
deck: `python3 build_deck.py && python3 build_web.py` regenerates everything
here. Every line of copy is extracted from the deck cards and asserted back
against them at build time, so edit the card builders, not this HTML.

## Where it actually deploys from

**This repo is not the deploy source.** The page ships inside the main website
repo, `Sixdis-Oolka/oolka-web`, as a static folder at `public/freedom-report/`,
so it goes out through the normal review and deploy pipeline. See
[oolka-web#201](https://github.com/Sixdis-Oolka/oolka-web/pull/201).

An earlier plan cloned this repo onto the server and pointed an nginx `alias`
at it. That was dropped: it put the page outside code review and left two
copies to keep in sync.

To publish a change: rebuild here, then copy `index.html` and `assets/` into
`public/freedom-report/` in oolka-web and raise a PR.

Two things follow from Next.js serving the page, and both will break if
reverted:

- **Asset paths are root-absolute** (`/freedom-report/assets/...`). Relative
  paths only resolve under a trailing slash, and oolka-web runs
  `trailingSlash:false`, so `/freedom-report/` 308s to `/freedom-report` where
  a relative `assets/map.png` resolves against `/` and 404s.
- **Canonical, `og:url` and the JSON-LD `url` carry no trailing slash**, so they
  point at a 200 rather than a 308.

## The PDF

The 10 MB PDF is not committed to oolka-web. It is served from the CloudFront
distribution that already fronts Oolka's static assets, at
`production/reports/FreedomReport.pdf`, and should carry
`Content-Disposition: attachment` so the "Download the report" CTAs actually
download rather than opening a tab. The copy in this repo is the source file
for that upload.

## Still owed

- Spot-check Indic text on Windows (Nirmala UI), especially Ol Chiki and
  Meetei Mayek. macOS is verified live, Android by forcing the Noto stack.
