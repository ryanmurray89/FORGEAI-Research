# FORGE-NOTE-007 — Evidence-Bound Candidate Generation and Provider Rate-Limit Resilience

**Date:** 2026-09-02  
**Status:** Published technical note  
**Project:** FORGE AI / NexLabs

## Purpose

Once the 15-topic / 30-card clean pilot had authoritative evidence and an explicit card blueprint, FORGE
needed a generator that could use model output **without treating model output as truth**.

The generator therefore operated under an evidence-bound contract.

## Candidate-generation contract

The historical pilot generator included:

- frozen evidence SHA-256 verification before generation;
- DeepInfra and local Ollama provider support;
- a four-card cross-domain canary mode;
- a strict evidence-only system prompt;
- atomic claim-to-source mappings;
- separate focused `retrieval_text`;
- candidate schema and length validation;
- long verbatim-copy detection;
- regression guards for known synthetic contamination;
- high-stakes personalized-advice guards;
- generation audit/failure logs.

Generated candidates remained:

- `verified = false`
- `production_ready = false`

Trust assignment was explicitly deferred.

## Why that boundary matters

A model can synthesize useful prose from good evidence and still introduce unsupported wording.

FORGE therefore separated:

`generation -> candidate`

from:

`verification -> trusted knowledge`

The generator's job was to produce a structured, reviewable candidate with evidence mappings — not to
declare that candidate correct.

## Provider pacing

During later generation work, FORGE added Groq rate-limit awareness:

- `x-ratelimit-*` header tracking;
- rolling TPM pacing;
- reset-duration parsing;
- serialized provider calls;
- `Retry-After` fallback handling;
- cumulative token/cost accounting.

The reserved maximum completion budget was reduced:

`1400 -> 900 tokens`

Local normalization also added:

- claim punctuation repair;
- retrieval-text expansion/trimming;
- **600-character hard floor**
- **700-character target**

## TPM deadlock defect

A concrete edge case exposed a pacing bug:

- conservative request estimate: **8,041 tokens**
- provider TPM bucket: **8,000 tokens**

If the pacing threshold itself exceeded the entire bucket, the loop could wait forever for a condition
that could never become true.

The correction:

- capped the pacing threshold at the provider's actual TPM limit;
- kept the provider tokenizer / HTTP 429 response authoritative;
- retained `Retry-After`;
- added an escape when remaining-token headers lacked a usable reset time;
- added a regression test for the exact **8,041 vs 8,000** condition.

## Research significance

This work is less glamorous than a benchmark, but it protects experimental validity.

A large generation run that silently stalls, miscounts failed-attempt tokens, or changes behavior under
provider pressure is difficult to reproduce and difficult to cost.

Rate-limit behavior therefore became part of the generation protocol rather than an operational afterthought.

## Boundary

No trust was assigned during generation.

No Chroma changes were made.

`brain_api.py` was not changed by these generator/pacing revisions.
