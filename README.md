# Chiliad Techniques Encyclopedia - static mirror (lite edition, no comment sections)

**v1.1.2**, built Jul 06, 2026. A fully self-contained, offline mirror of the
Chiliad Compendium **/techniques** page. Live at https://quantrozic.github.io/chiliad-techniques/

- `index.html` - the techniques browser (search, category filters, sorting),
  mirroring the in-app page.
- `techniques/<id>.html` - one page per technique (298 total) with its
  complete metadata and **every** documented archive case.
- `threads/<postId>.html` - one page per documented r/chiliadmystery thread
  (4384 total) with the full post body (comment sections omitted in this edition; each page links to the discussion on Reddit).
- `methodology.html` / [METHODOLOGY.md](METHODOLOGY.md) - full pipeline provenance:
  corpus, matching rules, audit criteria, AI/human division of labor.
- `corrections.html` - public corrections policy (GitHub issues), thread-verification
  process, reviewer recruitment.
- `changelog.html` / [CHANGELOG.md](CHANGELOG.md) - versioned change history with
  correction credits.
- `data/` - machine-readable dataset (techniques.json, threads.csv), CC BY 4.0.
- `assets/` - shared stylesheet and tool logos.

Licensing: see [LICENSE.md](LICENSE.md) (encyclopedia text & dataset CC BY 4.0,
code MIT, archived Reddit posts remain their authors').

Corrections: https://github.com/Quantrozic/chiliad-techniques/issues

No server needed; open `index.html` in a browser.

Regenerate with (from the Chiliad Compendium app repo):

```
node --import tsx scripts/export-techniques-full.ts <scratch>/techniques-full.json
python <scratch>/extract_threads.py
python scripts/build-techniques-site.py <scratch> --out techniques-site-lite --no-comments
```
