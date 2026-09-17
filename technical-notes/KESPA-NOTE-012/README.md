# KESPA-NOTE-012 — Trusted Research Release Promotion Pipeline

**Date:** 2026-09-14  
**Status:** Verified — end-to-end release proof completed  
**Project:** KESPA AI / NexLabs Studios

## Purpose

Before the later natural knowledge-gap automation was built, KESPA had already proven a separate research-release
path for moving evidence-backed research into trusted knowledge.

The path separated research construction from production promotion:

`evidence -> audit -> claims -> support verification -> release policy -> frozen release -> candidate -> trusted knowledge -> index -> NexLedger`

## Research-release stages

The historical pipeline contained distinct stages for:

1. safe evidence acquisition;
2. evidence-quality audit;
3. evidence-bound claim construction;
4. claim-support verification;
5. research-release policy;
6. trusted release packaging.

The resulting release could then cross into the application lifecycle as a `research_release` candidate.

That separation matters because research output was not allowed to become trusted merely because a model produced it.

## End-to-end systemd proof

The verified proof used:

`What is systemd?`

Recorded release:

`forge-release-b668d809f8b517bb46cdb92b`

The release contained:

- **6 verified claims**
- **1 evidence record**

Application-side result:

- candidate: **#80**
- candidate source type: `research_release`
- trusted knowledge: **#72**
- status: **active / public / indexed**

The live Brain subsequently retrieved the new trusted card.

Importantly, the recorded live response did **not** rely exclusively on that one card; normal response composition still operated.

## NexLedger proof

The promoted trusted record also completed NexLedger attestation:

- attestation: **#73**
- token: **TK121**
- asset: **FORGEAI#TK121V1**
- ledger height: **91**

The existing generic NexLedger worker remained untouched.

## Why this mattered

This proved that KESPA could maintain a clean boundary between:

`research artifact`

and:

`production trusted knowledge`

A research result had to survive explicit release gating before entering the authoritative trusted-knowledge store and local semantic index.

The later autonomous natural-gap lifecycle reused the same general research principle, but was intentionally implemented as an isolated path rather than by modifying these older shared scripts.

## Evidence boundary

Search snippets were not accepted as evidence.

The evidence path depended on fetched/audited source material and explicit claim-support verification.

## Limitation

This is one end-to-end promotion proof, not a population-level accuracy study.

The historical systemd release used one evidence record for six verified claims. Later natural-research work adopted stricter independent-source requirements; this note preserves the earlier pipeline as it actually operated rather than applying later policy retroactively.
