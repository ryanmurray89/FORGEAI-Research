# FORGE-NOTE-009 — Frozen Evidence Identity: Canonical URL + SHA-256

**Date:** 2026-09-04  
**Status:** Published technical note  
**Project:** FORGE AI / NexLabs

## Problem

The scale verifier originally resolved frozen evidence by canonical URL.

That became ambiguous once FORGE encountered authoritative pages that legitimately produced more than one
bounded frozen evidence excerpt.

The historical scale dataset contained:

- **17 authoritative URLs** mapping to multiple frozen excerpts;
- **16 of those URLs** referenced by generated candidates.

URL alone was therefore not a sufficiently precise evidence identifier.

## Correction

The scale claim/evidence verifier changed its lookup identity from:

`canonical URL`

to:

`canonical URL + SHA-256`

The URL identifies the source location.

The hash identifies the exact frozen evidence content used by the candidate.

Together they preserve excerpt-level identity without pretending that every URL can map to only one evidence record.

## Why this matters

Consider one authoritative documentation page containing several sections.

Two claims may legitimately use different frozen excerpts from the same page.

With URL-only matching, a verifier can resolve the wrong excerpt even though the source URL itself is correct.

Using:

`source location + frozen content hash`

makes the evidence binding substantially more precise and auditable.

## Scope of the change

The historical record explicitly limits the correction to the new **scale verifier**.

It did **not** mutate:

- candidates;
- frozen evidence;
- production Chroma;
- Brain;
- the database.

The canonical pilot verifier was left untouched.

## Contamination guard

The same correction preserved the strict `deadlock 1213` contamination guard.

The only exception was where the approved blueprint explicitly permitted the `deadlock-1213` topic itself.

That is an important distinction: fixing evidence identity did not weaken the general contamination boundary.

## Research significance

FORGE's evidence pipeline treats provenance as more than a source URL.

A defensible frozen evidence record needs to answer both:

1. **Where did this come from?**
2. **Which exact frozen content was used?**

This correction moved the verifier closer to that contract.

## Limitation

SHA-256 proves identity of frozen bytes, not factual quality.

Authority, relevance, scope fit, independence, and claim support still require their own checks.
