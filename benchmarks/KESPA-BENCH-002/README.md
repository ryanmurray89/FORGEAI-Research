# KESPA-BENCH-002 — Adaptive Inference D v001

**Date:** 2026-09-05  
**Status:** Verified — user environment  
**Primary preregistered result:** **FAIL**  
**Project:** KESPA AI / NexLabs Studios

## Research question

Can KESPA's adaptive inference path retain near-best observed answer quality while reducing latency,
energy, and model-call cost under a preregistered set of retrieval, efficiency, and escalation constraints?

## Frozen workload

D v001 used the same **54-case** benchmark family as the prior A/B/C experiment.

The final scoring protocol was:

`Frozen A + frozen B + C-envelope with D answer; C slot = D`

The blinded evaluator processed **162 answer rows**.

Judge:

`Qwen/Qwen3.6-35B-A3B`

## D v001 result

- Composite quality: **55.2586**
- Mean latency: **2443.03 ms**
- Mean GPU energy: **0.153616 Wh**
- Retrieval Hit@1: **42/54**
- Gold micro recall: **59.5238%**
- Mean LLM calls: **1.0185**
- Escalation rate: **62.9630%**
- Quality/sec: **22.618858**
- Quality/Wh: **359.718120**

Same-batch comparison:

- A quality: **23.2600**
- B quality: **56.2379**
- D quality: **55.2586**

So D came very close to B's same-batch composite quality while meeting its latency and energy budgets.

## Preregistered checks

| Check | Threshold | Observed | Result |
|---|---:|---:|---|
| Quality | >= 51.50 | 55.2586 | PASS |
| Hit@1 | >= 50/54 | 42/54 | **FAIL** |
| Gold micro recall | >= 75% | 59.5238% | **FAIL** |
| Mean latency | <= 2500 ms | 2443.03 ms | PASS |
| Mean energy | <= 0.1600 Wh | 0.153616 Wh | PASS |
| Mean inference calls | <= 1.30 | 1.0185 | PASS |
| Escalation rate | <= 25% | 62.9630% | **FAIL** |
| Quality/sec | > C | 22.618858 | PASS |
| Quality/Wh | > C | 359.718120 | PASS |

## Primary result

**FAIL.**

That result is intentionally preserved rather than reframed as a success.

D v001 passed **6 of 9** preregistered checks, including quality, latency, energy, model-call count,
quality/sec, and quality/Wh. But the experiment failed three important operational targets:

- retrieval Hit@1;
- gold micro recall;
- escalation rate.

The **62.963% escalation rate** was particularly important because the adaptive design was intended to
avoid expensive escalation on most requests.

## Why the negative result matters

The run showed that adaptive inference was promising, but the tested routing/retrieval policy was not yet good enough.

It demonstrated a useful separation:

- answer quality and compute efficiency could be strong;
- retrieval coverage and escalation behavior could still violate the intended architecture.

That is more informative than optimizing the policy until every metric turns green.

## Judge integrity

The historical finalization recorded:

- **162** blinded judgments;
- **461,717** reported judge tokens;
- estimated judge cost **$0.140612**;
- raw results SHA-256  
  `EC4717DA7745532124C8F02BC256501B85C01CAC346A63E837BE89C9E72D028E`;
- judge prompts exposed A/B/C identity: **NO**;
- raw results modified: **NO**.

A previously known harness metadata defect left `gold_claim_ids` empty. Gold association was repaired
offline from the locked `reference_claim_ids` without modifying the raw result file.

## Boundary

This benchmark did not modify production Chroma, Brain, or the database.

It is evidence about one frozen adaptive-inference design, not a universal claim about all KESPA routing policies.
