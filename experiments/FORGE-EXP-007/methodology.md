# Methodology

## 1. Bounded canary selection

The pilot selected four cross-domain card blueprints rather than starting with a large generation batch.

Each blueprint was already bound to collected evidence.

## 2. Evidence-bound generation

Groq `openai/gpt-oss-120b` was used by `forge-kb-v2-generator-006-groq`.

Frozen evidence hashes were checked before generation.

The model's job was to create structured candidate material from the supplied evidence. Its output was not treated as a source and did not receive trust.

## 3. Candidate-only state

Generated objects remained:

- `verified=false`
- `trust=null`
- `production_ready=false`

No Chroma writes were performed.

## 4. Human-readable inspection

The generator emitted a candidate review artifact so generated claims, retrieval text, sources, and safety flags could be inspected before trust assignment.

## 5. Independent claim/evidence verification

A downstream verifier evaluated candidate claims against the frozen evidence and approved scope.

This stage was allowed to fail the candidate.

Observed examples include:

- PostgreSQL: verifier pass, still pending final policy.
- Calculus: verifier fail because one claim was only partially supported by the available frozen evidence.
- Diabetes: verification execution failure because claim numbering was structurally incomplete.

## 6. Fail-closed interpretation

A generation success was never counted as a verification success.

A partial-support finding or execution defect did not produce trusted or production-ready knowledge.

## Measurement boundary

The experiment records provider usage and observed pipeline states.

It does not estimate an all-card verification pass percentage because the supplied reconstruction set does not contain a complete final-policy result for every one of the four candidates.
