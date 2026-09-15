# Methodology

## Input population

The historical experiment used the existing scale claim/evidence verifier against a 100-card diagnostic
subset of generated knowledge.

Evidence resolution used canonical URL plus SHA-256 rather than URL alone so that multiple legitimate
frozen excerpts from the same authoritative URL could remain distinct.

## Verification unit

Verification was performed at the atomic-claim level rather than the whole-card level.

Each surviving claim retained evidence/provenance linkage. Claims that did not meet the strict support
criteria were excluded from the clean corpus.

## Consolidation

The verified survivors were consolidated deterministically into:

`clean_verified_claim_corpus_v001`

The historical user-environment validation recorded the exact expected count of 423 claims.

## Production isolation

The consolidation did not write to production Chroma, Brain, or the database, and did not assign
production trust or production-ready status.
