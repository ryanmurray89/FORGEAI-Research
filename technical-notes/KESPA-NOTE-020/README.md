# KESPA-NOTE-020 — Always-On Orchestration Overhead in the Locked A/B/C Runtime Run

**Date:** 2026-09-04  
**Status:** Verified — user environment  
**Project:** KESPA AI / NexLabs Studios

## Purpose

The final A/B/C benchmark established the quality-versus-compute result.

This note preserves a narrower architecture finding from the **raw runtime execution**:

> What did the then-current full KESPA orchestration path actually do per request, and how much compute did that behavior cost?

The answer became one of the reasons V2 moved toward **adaptive inference** rather than always-on orchestration.

## Locked execution

The runtime experiment used:

- **54 locked evaluation cases**
- **3 arms**
- **162 total executions**
- **162/162 successful executions**

The three paths were:

- **A** — raw local model
- **B** — verified atomic retrieval fast path
- **C** — then-current full KESPA orchestration

## Raw latency and energy

| Arm | Mean latency | Mean GPU energy |
| --- | ---: | ---: |
| A — raw local model | 3.757 s | 0.2450 Wh |
| B — verified retrieval | 1.675 s | 0.1085 Wh |
| C — full orchestration | 9.066 s | 0.5759 Wh |

Relative to B, C used approximately:

- **5.413×** the latency
- **5.308×** the GPU energy

B was also approximately:

- **55.4% lower latency** than A
- **55.7% lower GPU energy** than A

## What Arm C actually did

Across 54 cases, Arm C recorded:

- total LLM passes: **65**
- RAG searched: **54/54**
- RAG actually used: **28/54**
- planner used: **8/54**
- reviewer used: **3/54**
- inference avoided: **0/54**

That profile is important.

The system paid for broad orchestration infrastructure on every request even though:

- retrieved knowledge was used on only about half the cases;
- planner/reviewer stages were needed on a minority of cases; and
- no evaluation case avoided inference entirely.

## Later quality context

The later blinded quality stage reported:

- A quality: **20.71**
- B quality: **54.22**
- C quality: **27.71**
- B case wins: **39/54**

So the expensive C path did not recover enough quality in this workload to justify its runtime cost.

This is not a claim that orchestration is useless.

It is a claim that:

> **orchestration should earn its compute.**

## V2 architecture consequence

The raw runtime profile supported a shift away from:

`every request -> full orchestration`

toward:

`trusted fast path -> escalate only when signals justify more compute`

That is the conceptual bridge from the V1 C arm to the later D adaptive-inference experiment.

The model remains available for difficult cases.

The architectural change is that KESPA should not automatically pay for every available reasoning stage on every request.

## Safety / isolation

The benchmark changed no production state:

- Production Chroma: **NO**
- Brain modification: **NO**
- database writes: **NO**
- private memory: **OFF**
- external web/cloud: **OFF**
- trust callback: **OFF**

## Limitations

This was one model, one RTX 3070-class environment, one verified corpus, and one frozen 54-case workload.

The result should therefore be read as evidence against **indiscriminate orchestration in this tested architecture**, not as a universal result against multi-stage reasoning.
