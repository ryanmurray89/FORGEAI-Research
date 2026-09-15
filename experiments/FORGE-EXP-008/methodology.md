# Methodology

## Candidate/evidence identity

Before model evaluation, the verifier rechecked frozen evidence hashes and candidate content/claim identity.

This prevents the verifier from silently judging different evidence or mutated candidate content from the material that was originally bound together.

## Cross-model verifier

Candidate claims were evaluated with `qwen/qwen3.6-27b`.

The run records explicitly state that the generator and verifier were not from the same model family.

## Claim-level verdicts

Each material claim could receive a support verdict such as:

- SUPPORTED
- PARTIALLY_SUPPORTED
- UNSUPPORTED
- CONTRADICTED
- UNCLEAR

Card-level verification could fail if claim support was insufficient.

## Structural validation

Malformed or incomplete verifier structure was treated as an execution failure.

The `missing_claim_number:7` case demonstrates that a structurally incomplete response did not become an implicit pass.

## High-stakes review

High-stakes/safety-sensitive candidates could pass model verification while still requiring human review.

A model pass did not assign trust, mark the candidate verified, or make it production-ready.

## Aggregate calculation

Public aggregate metrics are simple sums across the four recorded verifier summaries.

They are labeled as card-evaluation executions because this reconstruction does not independently prove corpus-level deduplication across every historical batch.
