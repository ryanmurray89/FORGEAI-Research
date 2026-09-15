# Methodology

## Question isolation

The benchmark builder created:

- 66 total questions;
- 12 calibration questions;
- 54 locked evaluation questions.

Only the 12 calibration questions were loaded during retrieval-policy tuning. The locked evaluation
file hash was verified without parsing the evaluation questions.

## Corpus

The isolated retrieval collection contained 423 verified atomic claims.

A compatibility validator confirmed exact IDs/documents/metadata and retrieval equivalence while
allowing harmless float-scale embedding round-trip differences.

## Calibration sequence

The initial comparison tested:

1. plain vector top-6 retrieval;
2. the then-current FORGE minimum-150-character retrieval policy;
3. a reduced minimum-40-character atomic-compatible variant.

A later final policy-freeze comparison tested plain vector top-6 against the refined atomic-compatible
FORGE ranking path.

The public record keeps the initial and final measurements separate because the reported timing values
came from different calibration steps.

## Selection rule

The final policy was frozen based on retrieval effectiveness and latency before opening the 54-question
evaluation workload.

The selected policy was `plain_vector_top6`.
