# FORGE-EXP-005 — Claim-Level Verification and Clean Corpus Consolidation

**Date:** 2026-09-04  
**Status:** Verified — user environment  
**Project:** FORGE AI / NexLabs

## Research question

Does strict claim-level verification preserve independently supportable knowledge that would be lost
if generated knowledge is accepted or rejected only at whole-card granularity?

## Background

FORGE's earlier generation pipeline produced multi-claim cards.

That creates a trust-boundary problem: one unsupported claim can make the whole card unsafe to trust,
even when several other claims in that same card are independently supported by frozen evidence.

The diagnostic experiment therefore moved the verification boundary from:

`card -> accept/reject`

to:

`claim -> evidence -> strict verification -> retain/reject`

## Result

The clean consolidation produced:

- **423 verified atomic claims**
- from **66 source cards**
- spanning **66 topics**
- linked to **56 frozen evidence excerpts**
- **331 claims rescued from cards that otherwise failed**
- recorded strict claim survival: **48.0%**

The 331 rescued claims represent about **78.3%** of the final 423-claim corpus.

## Why this matters

A whole-card verifier can throw away valid knowledge simply because a neighboring claim fails.

Claim-level verification gave FORGE a finer trust boundary:

- unsupported claims could be rejected;
- independently supportable claims could survive;
- each surviving claim remained linked to frozen evidence/provenance.

That 423-claim corpus later became the clean baseline used for the retrieval and A/B/C benchmark work.

## Safety / production boundary

This consolidation step did **not**:

- modify production Chroma;
- modify Brain API behavior;
- write to the production database;
- assign production trust;
- mark the corpus production-ready.

The historical result was a clean candidate corpus suitable for controlled benchmarking and later promotion decisions.

## Limitation

The diagnostic set covered **100 generated cards**, not the full **1,075-candidate** generation population.

The result therefore supports claim-level verification as the better trust boundary for this diagnostic
subset; it does not establish a universal survival rate for all future FORGE knowledge.
