# KESPA-BENCH-004 — Clean Pilot Retrieval Gate and Contamination-Metric Correction

**Date:** 2026-09-02  
**Status:** Published historical benchmark record  
**Project:** KESPA AI / NexLabs Studios

## Purpose

Before scaling the Knowledge Factory beyond its first clean pilot, KESPA tested whether a small evidence-bound corpus
could retrieve the intended knowledge reliably.

The candidate index contained **30 verified clean pilot cards**.

The benchmark used **30 queries** with **top-k = 5** retrieval.

## Candidate index

The isolated candidate Chroma collection was built from `retrieval_text` using:

- embedding model: `all-MiniLM-L6-v2`
- dimension: **384**
- normalized embeddings: **YES**
- distance: **cosine**
- candidate cards: **30**
- verified=true: **30**
- trust assigned: **NO**
- production_ready=true: **0**
- high-stakes cards: **8**
- safety-sensitive cards: **2**
- read-back integrity: **PASS**

The production collection was not mutated.

## Retrieval result

The clean pilot achieved:

- expected card @1: **28/30 = 93.3%**
- expected card @3: **30/30 = 100%**
- expected card @5: **30/30 = 100%**
- expected topic @1: **30/30 = 100%**
- expected topic @3: **30/30 = 100%**
- expected topic @5: **30/30 = 100%**

So every query retrieved the correct topic at rank 1, even though two queries ranked the alternate card from the same topic above the exact expected card.

## The first gate said NO-GO

The original `forge-kb-v2-retrieval-benchmark-001` run reported:

- candidate contamination flags: **20/150 top-5 results**
- affected candidate queries: **14/30**
- scale-rebuild gate: **NO-GO**

The retrieval accuracy itself was already strong.

The problem was the definition of contamination.

## Metric defect

The first benchmark treated legitimate cross-topic retrieval inside the new clean corpus as though it were hard synthetic contamination.

That was too broad.

A retrieval benchmark should distinguish:

`another clean, evidence-bound topic appeared in top-5`

from:

`old synthetic/forbidden contamination appeared in retrieval`

Those are not the same failure.

## Benchmark v002 correction

`benchmark_candidate_retrieval.py` was revised from v001 to v002.

The correction:

- separated **hard contamination** from ordinary cross-topic retrieval;
- stopped failing the gate merely because another clean topic appeared in top-5;
- added a whole-candidate hard-contamination scan;
- made legacy production-topic matching tolerant of generated topic prefixes.

The candidate and production Chroma collections remained query-only.

There were:

- **no Brain changes**
- **no corpus changes**

## Corrected public checkpoint

After the metric correction, the canonical KESPA research checkpoint recorded:

- clean pilot cards: **30**
- exact-card retrieval @1: **93.3%**
- expected-topic retrieval @1: **100%**
- hard synthetic flags in pilot top-5: **0 / 150**
- clean-corpus scale gate: **GO**

This is the result later surfaced on the KESPA public landing page as a pilot measurement.

## Why this matters

This benchmark contains both a positive retrieval result and a useful measurement failure.

The initial NO-GO was not simply discarded.

Instead, KESPA identified that the gate was measuring the wrong thing, tightened the metric, and preserved the distinction between:

`retrieval diversity`

and:

`synthetic contamination`

That correction matters because overly broad safety metrics can reject good systems just as easily as weak safety metrics can admit bad ones.

## Safety boundary

The benchmark did not authorize production replacement.

The supplied run explicitly recorded:

- production mutation methods used: **0**
- candidate writes during benchmark: **0**
- Brain changes: **0**

The scale gate only answered whether the clean retrieval design was suitable to continue scaling.

## Limitations

This was a **30-query pilot**, not a production-scale benchmark.

It measured retrieval behavior, not full answer quality.

The final corrected `0/150` / `GO` checkpoint is preserved in the public KESPA research-positioning record; the supplied raw transcript preserves the earlier v001 run before the contamination metric was corrected.
