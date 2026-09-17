# KESPA-BENCH-003 — Atomic Knowledge Retrieval Policy Calibration

**Date:** 2026-09-04  
**Status:** Verified — user environment  
**Project:** KESPA AI / NexLabs Studios

## Research question

Do retrieval safeguards designed for long synthetic/legacy cards remain appropriate after KESPA moves
to short, strictly verified atomic claims?

## Context

KESPA had moved to an isolated corpus of **423 verified atomic claims**.

Before the locked 54-question benchmark could be run, retrieval policy had to be calibrated using a
separate **12-question calibration set**.

The 54 locked evaluation questions were hash-verified but **not parsed** during calibration.

## Initial calibration

### Plain vector top-6

- Hit@1: **12/12**
- Hit@3: **12/12**
- Hit@6: **12/12**
- empty retrievals: **0/12**
- claim recall: **67/87 (77.0%)**
- retrieval precision: **93.1%**
- mean question recall: **80.6%**
- MRR: **1.0000**
- average returned: **6.00**
- mean latency: **29.15 ms**

### Legacy KESPA minimum-length policy (`min150`)

- Hit@1: **4/12**
- empty retrievals: **8/12**
- claim recall: **10/87 (11.5%)**
- retrieval precision: **100%**
- MRR: **0.3333**
- average returned: **0.83**
- mean latency: **60.03 ms**

### Atomic-compatible reduced floor (`min40`)

- Hit@1: **8/12**
- empty retrievals: **4/12**
- claim recall: **21/87 (24.1%)**
- retrieval precision: **100%**
- MRR: **0.6667**
- average returned: **1.75**
- mean latency: **45.61 ms**

## Why the legacy policy failed

A separate compatibility validation found that the old **150-character minimum length floor excluded
260 of 423 verified claims**.

That filter had made sense as a defensive heuristic against weak/short legacy cards. After KESPA moved
to deliberately atomic verified claims, it became destructive.

This is an important architecture lesson:

> A quality heuristic can become a quality defect when the knowledge unit changes.

## Final policy freeze

The final 12-question policy comparison selected:

`plain_vector_top6`

Recorded final comparison:

| Policy | Hit@1 | Claim recall | Precision | Mean latency |
|---|---:|---:|---:|---:|
| Plain vector top-6 | **12/12** | **67/87** | **93.1%** | **22.74 ms** |
| Atomic-compatible KESPA ranking | **12/12** | 66/87 | 91.7% | 49.89 ms |

The more complex ranking path matched Hit@1, but did not equal plain-vector claim recall and was more
than twice as slow in the final recorded policy-freeze comparison.

KESPA therefore froze **plain_vector_top6** for the later A/B/C evaluation.

## Supporting index validation

Before policy freeze, isolated benchmark Chroma compatibility was checked:

- IDs/documents/metadata exact: **423/423**
- top-1/top-10 retrieval-equivalence checks: **32/32**
- 43/423 embeddings differed only by float round-trip precision
- maximum observed embedding delta: **1.49e-08**

Those numerical differences were treated as harmless rather than as corpus corruption.

## Boundary

No production Chroma, Brain API, or database state changed during this work.

The purpose was calibration and policy selection for a frozen research benchmark.
