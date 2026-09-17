# KESPA-EXP-002 — Evidence Discovery: From Search Dependency to Source-First Discovery

**Date:** 2026-09-02  
**Status:** Verified historical experiment  
**Project:** KESPA AI / NexLabs Studios

## Research question

Can KESPA reliably locate candidate evidence for a fixed representative smoke set using general web
search as a required dependency, and if not, does deterministic first-party source discovery provide
materially better coverage without weakening source trust policy?

## Fixed test context

The same representative smoke set covered:

- **28 evidence slots**
- **24 cards**
- **24 canonical topics**

The larger validated blueprint behind the smoke contained:

- **4,807 evidence slots**
- **3,982 cards**
- **759 canonical topics**

The smoke runs were intentionally bounded. None of these runs wrote cards, embeddings, Chroma data,
Brain state, or production database records.

## Iteration 1 — v001 live evidence smoke

The initial design used search/discovery followed by bounded evidence fetching.

Observed result:

- Network requests: **112**
- Candidates: **12**
- Evidence excerpts: **1**
- `NO_CANDIDATE`: **25** slots
- `DISCOVERY_FAILED HTTP 403`: **2** slots
- Cards passing evidence gate: **1 / 24**

**Verdict:** do not scale the design to the full 4,807-slot queue.

## Iteration 2 — v001.1 search repair

The next revision fixed two mechanical discovery defects:

1. source-family priority could no longer make an unrelated source eligible;
2. generic scope/title language could no longer overpower canonical topic matching.

The source trust policy was not loosened.

The discovery-only rerun then produced:

- Search attempts: **136**
- Network requests: **136**
- Candidates: **0**
- Candidate slots: **0 / 28**

Provider diagnostics:

- Google CSE: **68 attempts, 0 result-bearing queries, 68 errors**
- DuckDuckGo: **68 attempts, 0 result-bearing queries, 17 errors**

**Verdict:** general web search was not reliable enough to remain a required locator in the tested runtime.

## Iteration 3 — v001.2 source-first discovery

General search was disabled for the bounded smoke (`provider=none`).

KESPA instead tried candidate location in this order:

1. catalog topic-specific URL hints;
2. catalog first-party entrypoints;
3. first-party `robots.txt` sitemap declarations;
4. common first-party sitemap locations;
5. bounded same-host navigation/link discovery.

Observed result:

- Network requests: **275**
- Discovery attempts: **297**
- Candidates discovered: **249**
- Slots with candidates: **26 / 28 (92.9%)**
- `DISCOVERED_APPROVED_CANDIDATE`: **18**
- `DISCOVERED_REVIEW_REQUIRED`: **8**
- `NO_SEARCH_RESULT`: **2**

First-party discovery diagnostics:

- Navigation: **84 attempts / 75 result-bearing / 7 errors**
- robots.txt: **36 attempts / 17 result-bearing / 7 errors**
- Sitemap discovery: **177 attempts / 76 result-bearing / 95 errors**

## Result

The experiment did **not** show that search engines are universally bad discovery tools.

It showed something narrower and more useful:

> In this KESPA runtime and fixed smoke set, general web search was not reliable enough to be a required
> evidence locator, while bounded source-first discovery produced candidate coverage for 26 of 28 slots
> without weakening the source-trust policy.

Search could therefore remain an optional fallback rather than a critical dependency.

## Trust boundaries preserved

Across the revisions:

- source-policy catalog: **60 hosts**
- auto-fetch-approved hosts: **37**
- unknown/new publishers remained **REVIEW_REQUIRED**
- locator metadata was **not evidence**
- no source family gained automatic trust merely because discovery improved

## What this does not prove

This was a bounded discovery experiment, not a full-corpus acquisition run. It does not establish:

- full 4,807-slot coverage;
- evidence quality for every discovered candidate;
- universal superiority of source-first discovery;
- general search-provider performance outside the tested runtime.

The next gate after successful source-first discovery was evidence-quality auditing, not automatic knowledge generation.
