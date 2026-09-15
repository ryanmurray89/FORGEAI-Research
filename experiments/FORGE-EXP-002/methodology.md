# Methodology

## Experimental sequence

This public record reconstructs three historical FORGE evidence-discovery iterations performed on
2026-09-02 against the same deterministic 28-slot representative smoke set.

### v001

Purpose: test the original evidence-acquisition path under bounded live network conditions.

The collector could perform search/discovery and fetch approved source pages. Source-policy,
SSRF/private-network blocking, redirect handling, robots.txt behavior, excerpt limits, and explicit
`noai`/`noimageai` exclusions remained active.

### v001.1

Purpose: isolate discovery after two mechanical ranking/eligibility defects were identified.

Changes were limited to discovery mechanics:

- priority alone could no longer make a source family eligible;
- canonical-topic matching replaced generic title/scope matching;
- topic matching became boundary-aware;
- source queries became concise;
- Google CSE used native site restriction;
- provider diagnostics were recorded.

No source-trust policy was broadened.

### v001.2

Purpose: test whether known authoritative source families could be located without requiring general search.

The smoke used `provider=none`, disabling Google and DuckDuckGo. Candidate discovery used:

- catalog URL hints;
- known first-party entrypoints;
- robots.txt sitemap declarations;
- common sitemap locations;
- bounded same-host navigation.

Unknown hosts remained review-required. Candidate discovery did not itself authorize evidence ingestion.

## Success interpretation

The experiment compares discovery coverage, not answer quality.

A candidate URL is only a locator. It is not trusted evidence until separately fetched, audited, and passed
through the evidence-quality lifecycle.
