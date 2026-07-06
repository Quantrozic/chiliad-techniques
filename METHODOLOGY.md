# Methodology

How the Chiliad Techniques Encyclopedia (v1.1.0, built Jul 06, 2026) was made: corpus provenance, matching rules, audit criteria, and the exact division of labor between human and AI. The rendered version of this document is published at https://quantrozic.github.io/chiliad-techniques/methodology.html.

## What this site is

A self-contained static mirror of the investigation-methods encyclopedia from the Chiliad Compendium,
an archive project about the Grand Theft Auto V "Mount Chiliad Mystery" and the r/chiliadmystery community
that has pursued it since 2013. The site catalogs 298 investigation techniques and links each to the
real, archived subreddit threads where the community used it (the lite edition (published on GitHub Pages) omits comment sections; the full edition mirrors complete comment trees).

This page documents where every number on the site comes from, how threads were matched to techniques,
what the badges mean, and what was machine-generated versus human-curated. Reputable references show their
pipeline; here is ours, verifiable against the published dataset.

## Source corpus

The underlying corpus is a complete export of the r/chiliadmystery subreddit obtained via
Arctic Shift
(a maintained Reddit archive of the historical Pushshift dumps plus ongoing ingestion), supplemented by
live ingestion for the most recent posts:

- 24,953 posts, spanning September 24, 2013 to July 1, 2026;

- 343,182 comment records attached to those posts (raw archive lines;
deleted/removed stubs included in the count but excluded from matching).

Post scores, comment counts, flairs and author names are as of capture and are not updated live.
Of the 24,953 posts searched, the 4,384 threads that matched at
least one technique are bundled on this site as thread pages; the rest of the corpus is searched but not mirrored here.

## The technique entries

The 298 entries come from two labeled tiers:

- 59 hand-curated methods, researched and written by the site maintainer.
Sixteen of these were added in July 2026 after the corpus audit (below) surfaced heavily-used community
methods the encyclopedia had missed (Snapmatic cataloguing, Director Mode testing, karma runs, tide watching, and others).

- 239 AI-generated entries (curation tier "community-index"): bulk-written by a large
language model (Anthropic Claude, driven through Claude Code) to enumerate plausible method variants. They are
uniquely worded but not individually researched, are badged "AI-generated" on every surface, and are
hidden by default behind the toggle next to the search box.

268 of the 298 entries have at least one archived case attached.

## How threads were matched to techniques

Matching is a deterministic keyword/IDF algorithm
(source: scripts/match-technique-cases.py
in the app repository); no AI model scores or selects matches. For every technique and every post:

- The searchable text is the post title, its selftext, and up to 4,000 characters of its comments.

- Candidate terms come from the technique's own title, a hand-maintained synonym list for methods whose titles
undersell their community vocabulary, and the technique's tags. Terms are weighted by inverse document frequency
(IDF) across the whole corpus, so distinctive words count far more than common ones.

- Every match must hit an anchor: a term derived from the technique's title or synonyms, or a tag
distinctive enough in the corpus (IDF ≥ 3.0). Generic process words ("analysis", "tracking", "testing", …)
never qualify as anchors.

- A candidate needs a minimum combined score of 7.0, and either a technique term in the post title or a
combined score ≥ 11.0, to be accepted at all.

This produced 10,760 technique↔thread links across the 4,384
bundled threads. Every accepted match is then tiered by confidence (next section). The full match list, with its
weak/strong labels, is in the published dataset, so the matching is auditable.

## Match tiers: what a case link actually claims

A keyword match proves vocabulary co-occurrence, not that the thread genuinely demonstrates the
method. The site therefore labels every case link with one of three tiers, and the technique pages sort them
in this order:

 | ✓ verified
 | A named person read the thread in full and confirmed it demonstrates the method. The badge carries the
verifier's name and date. This is the only tier that should be treated as a citation.
 | 0

 | (unlabeled)
 | A strong keyword match: a specific technique term in the post title (IDF ≥ 3.8), a very distinctive
term in the body corroborated by a second specific anchor (IDF ≥ 4.8), or a broad multi-term match (≥ 3 anchors,
IDF ≥ 3.5, score ≥ 12). Good reading suggestions; still machine-selected.
 | 5,116

 | weak match
 | Only generic or uncorroborated vocabulary backs the match. Possibly a false positive; shown for
completeness and clearly labeled.
 | 5,644

Tier thresholds were calibrated by hand-reviewing stratified samples of matches during the July 2026 audit.
As of v1.1.0 (built Jul 06, 2026), no matches have been human-verified yet: the tier ships with this release and verification is starting with the public launch. Until verified badges appear, every case link on this site should be read as machine-suggested evidence, not a citation. Want to help? See the corrections page.

## The corpus audit (the “No corpus evidence” and “Unverified” badges)

In July 2026 every AI-generated entry was audited against the complete corpus
(audit_corpus.py; one pass over all 24,953 posts and 343,182 comments). The audit computed
token document-frequencies for each entry's distinctive method vocabulary, swept ~150 hand-picked candidate
phrases, and mined method-suffix bigrams to catch phrasings the entries didn't use. The verdicts:

- "No corpus evidence" (29 entries): the entry's distinctive vocabulary appears
nowhere in thirteen years of community discussion under any tested phrasing. These entries are excluded
from case matching entirely (attaching keyword matches to them would manufacture false evidence) and are hidden
by default.

- "Unverified" (4 entries): only weak keyword matches exist, and manual review of
those matches found no genuine demonstration of the method. Hidden by default.

The same audit ran in reverse: mining the corpus for heavily-used methods missing from the encyclopedia,
which produced the sixteen archive-mined curated entries mentioned above.

## What AI did, and what it did not do

For transparency, the exact division of labor:

- AI-generated (239 entries): the "community-index" encyclopedia entries were written by a
large language model (Anthropic Claude, via Claude Code sessions in June–July 2026). Always badged, hidden by default.

- AI-assisted: the build tooling (matcher, audit script, this site generator) was written with
Claude Code, and the 59 curated entries were drafted with AI assistance against archive sources, then
reviewed by the maintainer.

- No AI at match time: thread↔technique matching, tiering, and the corpus audit are
deterministic Python over the corpus. Two runs on the same corpus give the same output.

- Human-only: the verified-citation tier. A verified badge is never assigned by a model.

## Known limitations

- Case links below the verified tier are co-occurrence evidence, and the 5,644 weak matches in
particular may be false positives.

- Comment text beyond 4,000 characters per post is invisible to the matcher, so comment-driven demonstrations
in very long threads can be missed.

- Scores, flairs and comment counts are frozen at capture (July 1, 2026 for the newest posts).

- The corpus is one subreddit; GTAForums, wikis and YouTube investigation work is referenced by some entries
but not systematically mined.

- AI-generated entries, even corpus-supported ones, describe plausible method variants rather than
individually-researched history.

## The dataset

The data behind this site is published, versioned with it, and reusable under CC BY 4.0
(data/):

- data/techniques.json: every technique entry with its full metadata, case-ID lists,
weak-match subsets, and human verifications.

- data/threads.csv: one row per bundled thread (id, title, author, UTC date, score, comment count,
flair, permalink) with the technique IDs it is documented under and its weak-match subset.

If you build something on this data, an attribution link back here is all the license asks.

## Versioning & how to cite

The site carries a version number (currently v1.1.0) in every footer; every change,
including corrections and who reported them, is listed in the changelog. Releases are
tagged in the GitHub repository and snapshots are
submitted to the Wayback
Machine, so any cited state of the site stays retrievable.

Suggested citation: Chiliad Techniques Encyclopedia v1.1.0 (Jul 06, 2026), https://quantrozic.github.io/chiliad-techniques/, CC BY 4.0.
