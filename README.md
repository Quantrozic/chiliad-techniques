# Techniques encyclopedia - static mirror (lite edition, no comment sections)

A fully self-contained, offline mirror of the Chiliad Compendium **/techniques**
page, generated Jul 06, 2026.

- `index.html` - the techniques browser (search, category filters, sorting),
  mirroring the in-app page.
- `techniques/<id>.html` - one page per technique (298 total) with its
  complete metadata and **every** documented archive case.
- `threads/<postId>.html` - one page per documented r/chiliadmystery thread
  (4384 total) with the full post body (comment sections omitted in this edition; each page links to the discussion on Reddit).
- `assets/` - shared stylesheet and tool logos.

No server needed; open `index.html` in a browser.

Regenerate with:

```
node --import tsx scripts/export-techniques-full.ts <scratch>/techniques-full.json
python <scratch>/extract_threads.py
python scripts/build-techniques-site.py <scratch> --out techniques-site-lite --no-comments
```
