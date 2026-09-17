# KESPA-EXP-007 — Groq Evidence-Bound Generation Canary and Fail-Closed Verification

**Date:** 2026-09-02  
**Status:** Verified historical experiment  
**Project:** KESPA AI / NexLabs Studios

## Research question

Can a background external model generate useful structured knowledge candidates from frozen evidence without being allowed to decide what becomes trusted knowledge?

And, separately:

Will the downstream verifier actually stop candidates whose claims are only partially supported or structurally invalid?

This four-blueprint canary provides a small but concrete test of both boundaries.

## Generation run

KESPA ran the evidence-bound pilot generator using:

- generator: `forge-kb-v2-generator-006-groq`
- provider: Groq
- model: `openai/gpt-oss-120b`
- blueprints selected: **4**
- candidates generated: **4**
- generation failures: **0**
- prompt tokens: **15,445**
- completion tokens: **1,942**
- total tokens: **17,387** (derived from the two reported token counters)
- reported run cost: **$0.003482**

The generator verified frozen evidence hashes before generation.

The historical synthetic corpus was **not** used as factual evidence.

## Trust boundary

Successful generation did not mean successful verification.

Immediately after generation, all four outputs remained candidates:

- `verified=false`
- `trust=null`
- `production_ready=false`
- Chroma writes: **0**

The next explicit gate was human-readable review followed by claim/evidence verification.

That separation is fundamental to KESPA:

`evidence-bound generation != verified knowledge`

## Downstream verifier behavior

The supplied verification retry record demonstrates multiple outcomes.

### PostgreSQL

`PostgreSQL EXPLAIN and query-plan basics`

Result:

- card verdict: **VERIFIER_PASS**
- scope: **IN_SCOPE**
- seven claims recorded as supported
- status: `MODEL_VERIFIER_PASS_PENDING_FINAL_POLICY`
- trust remained null
- verified remained false
- production-ready remained false

Even a verifier pass did not bypass the final policy boundary.

### Calculus

`One-variable calculus reference concepts`

Result:

- card verdict: **VERIFIER_FAIL**
- scope: **IN_SCOPE**
- claims 1–5 were supported
- claim 6 was only **PARTIALLY_SUPPORTED**
- final status: `MODEL_VERIFIER_FAIL`

The candidate asserted specific Taylor-theorem and convex-function details that were not actually present in the supplied frozen evidence excerpt.

The verifier therefore failed the card instead of treating plausible model output as fact.

### Diabetes

`What diabetes is: blood glucose and insulin`

The verification run recorded a structural execution failure:

`missing_claim_number:7`

The failure was surfaced explicitly rather than silently interpreted as successful verification.

## Result

The canary established two separate properties:

**Generation path:** 4/4 candidates were produced with 0 generation failures.

**Trust path:** generated text still had to survive independent claim/evidence verification and later policy gates.

The observed verifier behavior included both a supported pass and fail-closed outcomes for partial evidence and malformed verification structure.

## Why this matters

A knowledge-acquisition system becomes dangerous if the same model that writes a candidate can implicitly make that candidate true.

This experiment kept those roles separate.

The external model could help transform evidence into structured candidate claims, but KESPA retained downstream authority over:

- evidence binding
- claim support
- scope
- verification state
- trust
- production eligibility

That design is more important than the 4/4 generation success rate.

## Safety boundary

This experiment did **not**:

- assign trust during generation;
- mark generated cards production-ready;
- write generated candidates to Chroma;
- use the old synthetic corpus as factual evidence; or
- interpret a verifier execution error as a successful result.

## Limitations

This was a four-blueprint canary, not a scale-quality benchmark.

The reconstruction inputs preserve individual downstream verification outcomes but do not contain a complete final-policy summary for all four generated cards. This record therefore does not invent an overall post-verification pass rate.

The experiment supports a claim about **pipeline behavior and trust separation**, not broad factual-accuracy performance.
