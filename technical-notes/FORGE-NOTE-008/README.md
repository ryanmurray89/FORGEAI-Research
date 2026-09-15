# FORGE-NOTE-008 — Chroma Corpus Compatibility and Retrieval Equivalence

**Date:** 2026-09-04  
**Status:** Verified — compatibility validation passed  
**Project:** FORGE AI / NexLabs

## Purpose

Before the clean verified corpus could be used for retrieval calibration and the A/B/C benchmark, FORGE
needed to prove that moving the corpus into a Brain-compatible Chroma layout did not silently change the
knowledge records or the retrieval behavior.

The validated corpus contained **423 verified atomic claims**.

## Structural comparison

The compatibility check recorded:

- IDs exact: **423/423**
- documents exact: **423/423**
- metadata exact: **423/423**

Combined structural result:

`423/423 exact`

That meant the isolated benchmark index represented the same claim records, not a rewritten or transformed
copy with materially different metadata.

## Retrieval-equivalence check

FORGE then compared retrieval behavior across the compatible representations.

Recorded result:

- top-1 / top-10 retrieval checks: **32/32 matched**
- result: **PASS**

This supported treating the isolated Brain-compatible Chroma collection as a valid retrieval substrate for
the later policy calibration and benchmark work.

## Embedding round-trip differences

The embeddings were not perfectly byte-identical after storage/round-trip:

- **43/423** embeddings had a nonzero numeric delta
- maximum absolute delta: **1.49011611938e-08**

Those differences were at float-roundtrip scale.

Critically, they did **not** produce a mismatch in the 32 tested top-1/top-10 retrieval comparisons.

## Why this mattered

Without this validation, a later benchmark could be confounded by the index-conversion process itself.

The compatibility test established that:

`clean verified corpus -> Brain-compatible Chroma`

preserved the tested record and retrieval semantics closely enough for controlled evaluation.

## Boundary

This validation did **not** modify:

- production Chroma;
- Brain API code;
- the production database;
- knowledge trust assignments.

It was an isolated compatibility check, not a production migration.
