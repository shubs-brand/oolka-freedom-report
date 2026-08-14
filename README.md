# India's Financial Freedom Report — oolka.in page

Static site, no JavaScript. `index.html` + `assets/` + `FreedomReport.pdf`.

This folder is BUILT, never hand-edited. Source of truth is the card deck in
the Brand Track workspace: `python3 build_deck.py && python3 build_web.py`
regenerates everything here, and every line of copy is asserted against the
deck cards, so edit the card builders, not this HTML.

Before it goes live under oolka.in:
- set `og:image` and `og:url` to absolute URLs (marked in the head)
- add the canonical tag for the final path
- spot-check Indic text once on Windows (Nirmala UI) and Android (Noto),
  especially Ol Chiki and Meetei Mayek
