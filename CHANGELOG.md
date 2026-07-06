# Changelog

All notable changes to the Chiliad Techniques Encyclopedia static site. Current version: v1.1.0.

## v1.1.0 - 2026-07-06

- Reputability release.
- Published the full pipeline methodology (methodology page / METHODOLOGY.md): corpus provenance, matching rules and thresholds, corpus-audit criteria, and exactly what AI did and did not do.
- Public corrections policy: errors are now reported and tracked through GitHub issues, not DMs (corrections page).
- Added a human-verified citation tier: a named person reads a matched thread in full and confirms it demonstrates the method; verified cases carry the verifier's name and sort first. Infrastructure ships in this release; verification begins with the public launch, volunteers welcome via the corrections page.
- Versioning: site version and build date now appear in every footer and each technique's metadata panel, with this changelog published on-site.
- Licensing: encyclopedia text and the dataset are CC BY 4.0; the build code and page scripts are MIT; archived Reddit posts remain their authors' (LICENSE.md).
- Machine-readable dataset published at data/ (techniques.json + threads.csv) so the underlying data can be reused independently of this site.
- Fixed: technique pages in the lite edition claimed each case's "full thread and comments" were mirrored locally, contradicting the edition's omission of comment sections. Reported by pre-launch reputability review.
- Fixed: corpus figures were rounded inconsistently across pages ("~25k posts, ~314k comments") and the searched-corpus vs bundled-thread counts were never reconciled. All pages now state the exact figures: 24,953 posts searched, of which the 4,384 threads documented under at least one method are bundled. Reported by pre-launch reputability review.

## v1.0.1 - 2026-07-06

- Republished the site with a clean repository history.
- AI-generated encyclopedia entries and entries that failed the corpus audit are now hidden by default behind labeled toggles; the default view shows only community-evidenced methods.
- Added per-technique case sorting (strongest match / most upvotes).

## v1.0.0 - 2026-07-05

- Initial public release of the static mirror (lite edition): 298 technique entries, 4,384 mirrored r/chiliadmystery threads, keyword-matched archive cases with weak-match labeling, and corpus-audit badges on unsupported entries.
