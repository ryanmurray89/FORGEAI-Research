# Methodology

## Failure mode

The scale verifier attempted to resolve candidate evidence references using canonical URL alone.

The scale corpus contained authoritative URLs associated with multiple distinct frozen excerpts, making URL-only
resolution ambiguous.

## Identity correction

The verifier was changed to resolve evidence using the pair:

`canonical_url + evidence_sha256`

This retains source-location provenance while selecting the exact frozen evidence content.

## Integrity boundary

The correction was implemented in new scale-verifier files only.

The historical record states that the canonical pilot verifier was not changed and that no candidate/evidence,
Chroma, Brain, or database mutation occurred.

## Contamination handling

The existing deadlock-1213 contamination guard remained strict except for blueprint scopes that explicitly
authorized that topic.
