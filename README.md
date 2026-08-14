# India's Financial Freedom Report — oolka.in page

The web edition of India's Financial Freedom Report, from Oolka. Lives at
**https://oolka.in/freedom-report/**.

`index.html` + `assets/` + `FreedomReport.pdf`. Everything is relative paths;
the page renders complete with no JavaScript, and every motion and interaction
sits behind an `html.js` gate inside a reduced-motion guard.

## Build

This folder is BUILT, never hand-edited. The source of truth is the card deck:
`python3 build_deck.py && python3 build_web.py` regenerates everything here.
Every line of copy is extracted from the deck cards and asserted back against
them at build time, so edit the card builders, not this HTML.

## Deploy

oolka.in is self-hosted Next.js behind nginx. Clone this repo on that box and
alias the path to it:

```
sudo git clone https://github.com/shubs-brand/oolka-freedom-report.git /var/www/oolka-freedom-report
```

Then inside the oolka.in `server` block:

```
location = /freedom-report { return 301 /freedom-report/; }
location /freedom-report/ {
    alias /var/www/oolka-freedom-report/;
    index index.html;
}
```

`sudo nginx -t && sudo systemctl reload nginx`. Updates are `git pull` in that
directory.

Canonical, `og:url` and `og:image` are already absolute and point at
https://oolka.in/freedom-report/ — nothing needs editing at deploy time.

## Still owed

- Spot-check Indic text on Windows (Nirmala UI), especially Ol Chiki and
  Meetei Mayek. macOS and Android are verified.
- Add `/freedom-report/` to the oolka.in sitemap by hand — the nginx alias
  makes it invisible to Next's route-generated sitemap.
