# FORGE-NOTE-002 — Clean Verified Knowledge Production Baseline

**Date:** 2026-09-13  
**Status:** Verified — production cutover completed  
**Project:** FORGE AI / NexLabs

## What changed

FORGE retired the legacy **~441,197-card** corpus from live production retrieval and replaced it with the
clean **423-claim verified atomic corpus**.

The legacy corpus was retained as historical/research material rather than copied into the new live knowledge index.

## Clean Chroma build

The clean retrieval index was built from:

`D:\forge\verified_corpus\clean_verified_claim_corpus_v001`

into:

`D:\forge\chroma_db_clean_v001`

with:

- collection: `forge_cards`
- verified claims indexed: **423**
- embedding model: `all-MiniLM-L6-v2`
- distance: **cosine**
- build result: **PASS**

Expected claims and indexed cards matched exactly:

`423 == 423`

## Retrieval smoke validation

Before production cutover, the clean Chroma database was opened and queried against a known verified claim.

Observed:

- clean cards: **423**
- expected claim ranked: **#1**
- top similarity: **0.8409**
- verified metadata: **true**
- claim verdict: **SUPPORTED**
- expected terms present: **4/4**
- Chroma writes during validation: **0**

This was a smoke validation, not a full retrieval benchmark.

## Production cutover

The production cutover then:

- retired the legacy ~441k corpus from live retrieval;
- promoted the clean 423-claim index into production;
- copied **0 legacy cards** into the new dataset;
- preserved **13 chat-memory records**;
- preserved **5 user-memory records**;
- changed **no source code** during the cutover itself.

## Architecture boundary

After the cutover:

> **MySQL `trusted_knowledge` is authoritative. Chroma is the rebuildable retrieval index.**

This is important because an embedding database should not become the sole source of truth for trusted knowledge.

Trusted knowledge can be re-indexed into Chroma while retaining its canonical provenance, verification,
approval, and lifecycle state elsewhere.

## First live knowledge growth

The first manually trained/promoted trusted record was indexed after the clean baseline:

`423 -> 424`

Subsequent operational records later observed:

`423 -> 424 -> 425 -> 426`

as trusted knowledge entered the live index.

Those counts are operational milestones, not a controlled quality experiment.

## Research relevance

The cutover operationalized the result of the earlier corpus and retrieval experiments:

- large uncontrolled accumulation was removed from the live path;
- the verified atomic corpus became the starting production baseline;
- later knowledge growth had to enter through the trusted-knowledge lifecycle rather than silently expanding the retrieval corpus.

This created the production boundary needed for longitudinal contamination and autonomous-learning research.
