# KESPA-EXP-008 — Cross-Model Claim Verification and Human-Review Gating Pilot

**Date:** 2026-09-02  
**Status:** Verified — user environment  
**Project:** KESPA AI / NexLabs Studios

## Research question

Can KESPA independently check generated candidate claims against their frozen evidence using a different model family — while still failing closed on weak evidence and preserving separate human-review requirements for higher-risk material?

The recorded pilot verifier used:

- verifier: `forge-kb-v2-claim-verifier-002-free-tier`
- verifier model: `qwen/qwen3.6-27b`
- generator/verifier same model family: **NO**

## Four recorded verification runs

Across four recorded runs, KESPA performed **21 card-evaluation executions**.

Aggregate recorded outcomes:

- verifier passes: **19**
- verifier failures: **1**
- execution failures: **1**
- human-review-required flags: **7**
- supported claim verdicts: **130**
- partially supported: **1**
- unsupported: **1**
- contradicted: **0**
- unclear: **0**
- reported tokens: **105,688**

These totals are the sum of recorded verifier runs. They are not presented as a separately deduplicated corpus count.

## Run 1 — six-card clean verification

`batch-13a/verification-6b`

Result:

- candidate cards: **6**
- verifier pass: **6**
- verifier fail: **0**
- execution failures: **0**
- supported claims: **40**
- total reported tokens: **29,634**

All six passed the model-verification stage.

But the state remained:

`trust=null`

`verified=false`

`production_ready=false`

The next gate was still the final policy/trust stage.

## Run 2 — verifier catches unsupported material

`batch-13a/verification-7a`

Result:

- candidate cards: **7**
- verifier pass: **6**
- verifier fail: **1**
- supported claims: **45**
- partially supported: **1**
- unsupported: **1**
- total reported tokens: **30,762**

This is important because the verifier did not simply agree with everything the generator produced.

A candidate with incomplete evidence support failed the card-level verification gate.

## Run 3 — high-stakes model pass does not remove human review

`batch-13b/verification-highstakes-4`

Topics included:

- Cognitive Behavioral Therapy CBT
- Investing

Result:

- candidate cards: **4**
- verifier pass: **4**
- verifier fail: **0**
- supported claims: **26**
- human review required: **4**
- total reported tokens: **21,601**

Every card passed model verification.

Every card still required human review.

The resulting state remained equivalent to:

`MODEL_VERIFIER_PASS_PENDING_HUMAN_REVIEW`

with no trust assignment and no production-ready status.

That demonstrates a deliberate policy boundary:

> **model agreement does not erase a higher-risk review requirement.**

## Run 4 — structural verifier failure is blocking

`batch-13b/verification-safety-4`

Result:

- candidate cards: **4**
- verifier pass: **3**
- verifier fail: **0**
- execution failures: **1**
- supported claims: **19**
- human review required: **3**
- total reported tokens: **23,691**

The execution failure was surfaced as:

`missing_claim_number:7`

The next gate explicitly required resolving the verifier execution failure first.

KESPA did not infer that an incomplete verifier response meant the missing claim was safe.

## Trust and production boundary

Across the recorded verifier runs:

- frozen evidence hashes rechecked: **YES**
- candidate content/claim identity checked: **YES**
- trust assigned: **NO**
- candidate files mutated: **NO**
- cards marked verified by this stage: **NO**
- production-ready cards: **0**
- Chroma writes: **0**

The model verifier was an analytical gate, not the authority that promoted knowledge.

## Why cross-model verification mattered

The verifier used a different model family from the generator.

That does not guarantee independence in the statistical or epistemic sense, but it reduces one obvious failure mode:

`generator creates claim -> same model simply endorses its own phrasing`

Instead, candidate claims were checked against the frozen evidence under a separate verifier contract.

## Research significance

This pilot demonstrated three useful behaviors at once:

1. supported candidates could pass an independent model-verification stage;
2. partially/unsupported material could fail that stage;
3. high-stakes material could remain blocked for human review even after a model pass.

That is a much stronger trust boundary than treating model confidence or model agreement as permission to publish.

## Limitations

This was a small pilot and should not be interpreted as a general verifier-accuracy benchmark.

The aggregate count is a sum of four recorded evaluation runs, not a claim about a deduplicated production corpus.

Model-based evidence verification still inherits model limitations and therefore remains only one layer in the KESPA trust lifecycle.
