# FORGE-NOTE-014 — Blinded Quality Judging and Offline Gold-Metadata Repair

**Date:** 2026-09-04  
**Status:** Verified — user environment  
**Project:** FORGE AI / NexLabs

## Problem discovered after the raw benchmark

The A/B/C runtime benchmark completed successfully:

- **54 cases**
- **3 arms**
- **162/162 successful raw rows**

But a harness metadata defect was discovered afterward:

`162/162 raw rows had empty gold_claim_ids`

The underlying issue was that `reference_claim_ids` had been omitted from the gold-ID extraction path.

The benchmark answers themselves were already complete.

## What FORGE did not do

The experiment was **not rerun** merely to make the metadata prettier.

The original `raw_results.jsonl` remained unchanged.

Recorded raw-results SHA-256:

`C9CD588A1308D58710680A536C9E2509315B7B122A1B574357E6B6C2675C3049`

That preserved the original execution evidence.

## Offline repair

Gold associations were reconstructed offline from the already locked `reference_claim_ids`.

Validation recorded:

- frozen evaluation hash: **PASS**
- frozen verified-claim corpus hash: **PASS**
- raw matrix: **54 × 3 = 162**
- empty raw gold-ID arrays confirmed: **162/162**
- gold association repaired offline: **PASS**
- evaluation gold claims restored: **336**
- raw results modified: **NO**

This separated:

`original experimental output`

from:

`repaired evaluation metadata`

## Blinded judging

The repair pipeline then built **162 one-answer judge inputs**.

The judge inputs contained no:

- A/B/C arm labels;
- runtime metrics;
- system identity.

Judge:

`Qwen/Qwen3.6-35B-A3B`

Completed:

- **162/162 judgments**
- **461,717 reported judge tokens**
- estimated judge cost: **$0.140612**

## Repaired retrieval metrics

The offline gold repair also restored retrieval evaluation:

### B — plain verified top-6

- Hit@1: **54/54**
- Hit@3: **54/54**
- Hit@6: **54/54**
- gold micro recall: **79.17%**

### C — cards actually used

- Hit@1: **27/54**
- Hit@3: **27/54**
- Hit@6: **27/54**
- gold micro recall: **22.02%**

## Why this matters

A tempting response to a benchmark defect is to rerun everything.

That can be worse than the original bug because the new model outputs, runtime conditions, and random effects may no longer represent the frozen experiment.

FORGE instead preserved the original run and repaired only metadata that could be reconstructed from already locked artifacts.

That creates a cleaner audit trail:

`raw execution -> immutable`

`metadata repair -> explicit / offline / reproducible`

`quality judging -> blinded`

## Boundary

During the repair/judging process:

- production Chroma opened: **NO**
- production Chroma modified: **NO**
- Brain modified: **NO**
- database modified: **NO**
- raw results modified: **NO**

## Limitation

The final quality scores still depend on one LLM judge.

Blinding and deterministic metadata repair improve benchmark integrity, but they do not turn model-based evaluation into objective ground truth.
