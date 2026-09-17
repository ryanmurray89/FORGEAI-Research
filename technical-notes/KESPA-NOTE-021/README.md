# KESPA-NOTE-021 — Public-Only External Intelligence Refinery and Budgeted Cloud Analysis

**Date:** 2026-09-05  
**Status:** Verified worker boundary; Windows-service deployment separately noted as pending user-environment validation at the recorded checkpoint  
**Project:** KESPA AI / NexLabs Studios

## Purpose

KESPA's External Intelligence Refinery was built to answer a narrow architectural question:

> Can KESPA use strong hosted inference for background analysis without turning the hosted model into a trust authority or sending private/internal data to it?

The refinery's answer is **yes, but only behind explicit classification, budget, provenance, and promotion boundaries**.

## External-data boundary

The refinery permits only tasks explicitly classified as:

- `public_external`
- `public_benchmark`

Private/internal classes are blocked before provider execution, including categories such as:

- private
- personal_private
- business_private
- confidential
- restricted
- secret
- PHI / health-private

Manual tasks must also be explicitly classified into one of the two allowed public classes.

## Provider output is not trusted knowledge

Every successful refinery result preserves a trust block equivalent to:

```text
provider output is evidence:             NO
provider output is verified knowledge:   NO
automatic promotion allowed:             NO
next gate:                               local review / future knowledge lifecycle
```

The structured diagnostic schema also requires:

`do_not_auto_promote = true`

That means Groq can analyze a retrieval failure, propose query rewrites, identify possible embedding/reranker issues, or suggest metadata improvements — but it cannot decide that its own output is true.

## Durable queue and provenance

The refinery uses file-backed states:

```text
pending/
processing/
done/
failed/
```

Tasks receive deterministic content-derived IDs.

Successful results preserve:

- input SHA-256;
- result SHA-256;
- provider/model identity;
- latency;
- token usage;
- request identity where available;
- provider rate-limit headers;
- trust/promotion state.

Failures are also persisted.

Rate-limited tasks are returned to the pending queue rather than discarded.

## First workload: retrieval diagnosis

The initial high-value workload was public benchmark retrieval diagnosis.

D v001 misses can be transformed into tasks containing:

- the question;
- retrieved verified claims;
- locked expected gold claims;
- frozen artifact hashes.

The external analyst is instructed to diagnose the miss without inventing external facts or marking anything verified.

Its recommendations are normalized into a controlled action vocabulary such as:

- query rewrite;
- embedding change;
- reranker change;
- metadata enrichment;
- claim rewrite/split;
- increase candidate recall;
- manual review.

## Spare-quota claim enrichment

A separate enrichment worker can spend otherwise-unused external quota improving retrieval aids for **already verified** claims.

It can propose:

- alternate user queries;
- aliases/synonyms;
- key concepts;
- retrieval keywords;
- ambiguity notes;
- freshness risk;
- semantically equivalent retrieval text.

But it is explicitly told:

> Do not verify, correct, expand, or replace the claim. Generate retrieval aids only. Do not introduce new factual assertions.

The trusted corpus remains **read only**.

It also skips claims that are:

- high stakes;
- safety sensitive;
- marked for human review.

And if the real refinery queue has work, enrichment yields priority and does not run.

## Rate-aware operation

The initial desktop run completed **4 Groq 120B analyses** and exposed an **8K TPM** provider limit.

The worker was subsequently made rate-aware.

The recorded deployment configuration preserved:

- observed provider limit: **8K TPM**
- operating target: **6.5K TPM**
- daily token ceiling: **180,000**
- daily request ceiling: **900**
- proactive pacing
- `Retry-After` handling
- rate-limit cooldown
- persistent usage ledger

The design response to quota pressure is therefore:

`wait / queue / resume`

not:

`weaken safety / skip provenance / auto-promote`

## Windows service deployment

Because the refinery does not require the local GPU, the deployment target was moved toward the always-on Windows home server.

The service wrapper added:

- delayed automatic startup;
- restart-on-failure behavior;
- immediate first cycle;
- **15-minute** default queue cycles;
- portable service-root inference;
- status/log tooling;
- Windows-to-Windows state migration.

Migration deliberately excludes `.env` and API keys.

At the recorded September 5 checkpoint:

- worker compile: **PASS**
- Windows-service wrapper compile: **PASS**
- service command construction review: **PASS**
- actual Windows SCM user-environment validation: **not yet claimed**

This note preserves that distinction rather than retroactively calling the service deployment verified.

## Research significance

This component demonstrates an important KESPA design principle:

`external model capacity != external trust authority`

KESPA can borrow high-capability cloud compute for bounded public analysis while retaining:

- privacy classification locally;
- deterministic trust rails locally;
- persistent provenance locally;
- promotion authority locally.

That keeps provider choice replaceable.

Groq can later be swapped or joined by another hosted/local model without changing the rule that provider output starts as **candidate intelligence**, not truth.

## Limitations

The original refinery workload was narrow and focused mainly on retrieval diagnosis.

Additional provider roles and full knowledge-lifecycle integration were future work at this historical checkpoint.

The recorded budget numbers are deployment settings, not permanent architectural constants.
