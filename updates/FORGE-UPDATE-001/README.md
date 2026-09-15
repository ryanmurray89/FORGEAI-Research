# FORGE-UPDATE-001 — FORGE V2 Research Program

**Date:** 2026-09-05  
**Status:** Published research-program update  
**Project:** FORGE AI / NexLabs

## Why V2 changed

The completed A/B/C benchmark produced a strong architectural signal:

- Raw local model quality: **20.71**
- Clean verified retrieval quality: **54.22**
- Then-current FORGE orchestration quality: **27.71**

The clean verified-retrieval arm also recorded:

- **1.675 s** mean latency
- **0.1085 Wh** mean GPU energy
- **54/54** retrieval Hit@1
- **79.17%** gold retrieval recall
- **39** case-quality wins

The important conclusion was not "FORGE built a better language model."

It was that **the intelligence supplied to a small model, and the policy used to retrieve and trust it, can materially change useful system behavior and compute cost**.

## V2 research thesis

The program was reframed around this question:

> Can an intelligence-management system improve reliability, efficiency, provenance, and practical
> usefulness of relatively small/local language models by supplying and maintaining verified intelligence,
> selectively allocating compute, and preventing untrusted information from silently becoming persistent knowledge?

## Architecture direction

V2 made several ideas explicit:

- verified externalized intelligence over uncontrolled accumulation;
- trusted retrieval as a fast path;
- adaptive rather than always-on orchestration;
- evidence, trusted knowledge, and memory as separate data classes;
- provenance-preserving continuous knowledge growth;
- quality, latency, energy, and compute measured together.

In short:

> **The model reasons. FORGE supplies and maintains the intelligence.**

## Research hypotheses

### H1 — Verified knowledge can improve small-model usefulness

Initial A/B/C evidence supported this on the frozen workload, but replication across other workloads and
models remained necessary.

### H2 — Verified retrieval can reduce recurring inference compute

The initial B arm was both higher-scoring and less expensive in latency/energy than A and C.

That made retrieval quality an efficiency question, not merely a relevance question.

### H3 — More orchestration is not automatically better

The then-current orchestration arm consumed substantially more latency and energy without matching the
verified-retrieval arm's benchmark quality.

V2 therefore moved away from always-on orchestration.

### H4 — Adaptive compute should be tested directly

Instead of running every mechanism on every request, FORGE should escalate only when the request or
available intelligence justifies the additional compute.

At the time of this V2 revision, that hypothesis had not yet been validated. D v001 was run afterward.

### H5 — Continuous learning needs a trust lifecycle

A system that continuously stores model output will eventually recreate the contamination problem unless it separates:

`candidate -> provenance -> evidence -> verification -> conflict detection -> trust decision -> promotion`

At the time of the V2 revision this was a program objective. It was later operationalized.

### H6 — Knowledge quality may substitute for some model scale

FORGE's longer-term question is whether better verified intelligence and reusable solved work can allow
smaller local models to cover useful bounded workloads without always requiring larger inference models.

That remains a research hypothesis, not a universal established result.

## What V2 did not claim

V2 did not claim that:

- FORGE trained a superior foundation model;
- one benchmark proved general intelligence gains;
- verified retrieval always beats larger models;
- adaptive inference was already solved;
- future NSF or other funding was guaranteed.

It converted the initial benchmark evidence into a more rigorous research program with falsifiable
questions and measurable system-level tradeoffs.
