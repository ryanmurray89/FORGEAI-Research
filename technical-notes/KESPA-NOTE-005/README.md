# KESPA-NOTE-005 — Legacy Corpus Recovery and Clean Rebuild Boundary

**Date:** 2026-09-01  
**Status:** Published technical note  
**Project:** KESPA AI / NexLabs Studios

## Why this work was necessary

KESPA had accumulated a very large synthetic knowledge corpus.

At this point in the project, the historical record reports:

- **442,577 synthetic cards**
- uneven or synthetic trust assumptions
- known contamination concerns
- a need to preserve useful topic coverage without treating the generated card bodies as production truth

The response was not to delete the research history.

It was to separate **topic recovery** from **knowledge trust**.

## Recovered taxonomy

KESPA recovered all **729 original subject areas** from the legacy corpus.

The first recovery manifest classified topics into:

- `TECH_REVIEW`
- `REBUILD_FROM_SOURCE`
- `MANUAL_CLASSIFY`

There were **121 ambiguous classifications** requiring explicit resolution.

Those were resolved as:

- **81 -> TECH_REVIEW**
- **40 -> REBUILD_FROM_SOURCE**

Final recovered taxonomy:

- **484 TECH_REVIEW topics**
- **245 REBUILD_FROM_SOURCE topics**
- **0 MANUAL_CLASSIFY**
- **729 total topics**

## What was preserved

The recovery work preserved:

- per-topic corpus statistics;
- contamination statistics;
- classification-source metadata;
- the legacy synthetic corpus itself as an immutable archive.

It did **not** rewrite or silently sanitize the old corpus and then call it trusted.

## What was rejected

The **442,577 synthetic cards were explicitly rejected for clean production indexing**.

That is the key architectural boundary.

KESPA retained them as:

- historical material;
- research evidence;
- discovery/reference material.

But the clean production direction required new evidence-backed knowledge.

## Clean rebuild policy

The subsequent Knowledge Factory plan added:

- authoritative source policies by domain;
- topic-specific source hints;
- freshness/revalidation rules;
- high-stakes detection;
- primary-source requirements;
- independent cross-check requirements;
- technical code/command validation;
- evidence-based trust instead of synthetic fixed trust;
- focused retrieval-text contracts.

This meant KESPA could preserve *what subjects it knew it should cover* without preserving *unverified synthetic statements as truth*.

## Research significance

This recovery created the experimental boundary used by the later project:

`legacy synthetic corpus -> archive / history`

`recovered topic taxonomy -> research plan`

`new authoritative evidence -> candidate knowledge`

`verification -> trusted knowledge`

That separation is what made later clean-corpus and A/B/C experiments meaningful.

## Snapshot note

The **442,577-card** figure belongs to this September 1 recovery snapshot.

Later production-cutover records reference approximately **441,197** legacy cards after intervening system changes. This public record intentionally preserves the historical values rather than forcing them into one count.
