# FORGE-BENCH-001 — A/B/C Verified-Intelligence Quality and Compute Benchmark

**Date:** 2026-09-04  
**Status:** Verified — user environment  
**Project:** FORGE AI / NexLabs

## Research question

Under the same frozen evaluation workload, how do three approaches compare?

- **A — Raw local 7B**
- **B — Clean verified atomic retrieval**
- **C — Then-current FORGE orchestration / legacy retrieval path**

The benchmark was designed to test whether FORGE mechanisms materially improve useful small-model
output per unit compute rather than assuming that more orchestration or more stored data is automatically better.

## Frozen evaluation

- **54 locked evaluation questions**
- **3 arms**
- **162 system executions**
- **162 blinded quality judgments**
- clean corpus: **423 verified atomic claims**
- linked frozen evidence: **56 excerpts**

All three runtime arms completed **54/54** cases.

The quality judge was blinded to A/B/C identity, runtime metrics, and system identity until scoring was complete.

## Results

| Metric | A — Raw local 7B | B — Verified retrieval | C — FORGE orchestration |
|---|---:|---:|---:|
| Composite quality | **20.71** | **54.22** | **27.71** |
| Mean latency | 3.757 s | **1.675 s** | 9.066 s |
| Mean GPU energy | 0.2450 Wh | **0.1085 Wh** | 0.5759 Wh |
| Retrieval Hit@1 | — | **54/54** | 27/54 |
| Gold retrieval recall | — | **79.17%** | 22.02% |
| Case-quality wins | 2 | **39** | 3 |

Ties: **10**

Within this benchmark, Arm B's composite quality score was about **2.62×** Arm A's score while
mean latency was about **55.4% lower** and mean GPU energy about **55.7% lower**.

Those ratios describe this benchmark only. They are not claims that FORGE made the language model
itself 2.62× more intelligent.

## Retrieval policy was frozen before evaluation

A separate **12-question calibration set** was used before the 54 locked evaluation questions.

The final policy freeze selected `plain_vector_top6`:

- Hit@1: **12/12**
- claim recall: **67/87**
- retrieval precision: **93.1%**
- mean latency: **22.74 ms**

The comparison atomic ranking path produced:

- Hit@1: **12/12**
- claim recall: **66/87**
- retrieval precision: **91.7%**
- mean latency: **49.89 ms**

The locked 54-question evaluation set was not parsed during that calibration.

## Important benchmark repair

The raw execution completed successfully, but a harness metadata defect omitted `reference_claim_ids`
from the gold-ID extraction path. As a result, all **162 raw rows** contained empty `gold_claim_ids`.

The repair was performed **offline** using the already locked `reference_claim_ids`. The original
`raw_results.jsonl` was left unchanged.

This matters because the retrieval and quality evaluation could be repaired without rerunning or
post-hoc tuning the model outputs.

## Finding

The strongest result was not simply that retrieval helped.

It was that **clean, verified, atomic retrieval outperformed both the raw-model path and the more
expensive orchestration path on the reported composite quality measure while also requiring less
latency and GPU energy**.

The benchmark therefore motivated FORGE V2's emphasis on:

- verified externalized intelligence;
- trusted-retrieval fast paths;
- selective rather than always-on orchestration;
- compute-aware escalation.

## Limitations

This is a controlled system benchmark, not a universal model leaderboard.

It used one frozen corpus/workload, one local-model/hardware configuration, and one evidence-bound
LLM judge. Composite quality scores are benchmark scores and must not be interpreted as absolute
factual-accuracy percentages.
