# Methodology

## Blueprint reconciliation

The acquisition candidate consumes the already validated canonical blueprint without changing it.

Preflight validation checks that 3,982 cards and 4,807 evidence roles reconcile to the expected 759 canonical topics.

## Role assignment

Evidence slots are explicitly labeled as primary, supporting, or cross-check roles.

This lets later policy distinguish basic source coverage from required independent corroboration.

## Deterministic smoke construction

A representative subset of 28 evidence slots across 24 topics is generated deterministically.

Its SHA-256 is reproduced during validation so later acquisition-mechanics changes can be tested on the same bounded workload.

## Source-policy catalog

A conservative catalog defines source-family behavior.

Unknown source families default to `REVIEW_REQUIRED`.

## Acquisition rails

The collector applies network and content-boundary controls including SSRF safety, redirects, robots policy, AI-exclusion policy, and bounded excerpts.

Discovery is kept separate from direct page-content acquisition.

## Offline validation boundary

Compilation, blueprint reconciliation, deterministic smoke reconstruction, invariant checks, and the evidence-auditor harness run without network access.

The historical record does not claim the Windows live network smoke had run at this checkpoint.
