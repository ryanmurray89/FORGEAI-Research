# Methodology

## Pipeline sequence

Blueprint v004 used a deterministic planning pipeline:

1. verify the exact recovered 729-row manifest and knowledge-plan inputs;
2. reapply only the previously audited unsafe-classification corrections;
3. add exactly 37 approved foundational topics;
4. confirm that existing corrected rows were not altered by the amendment;
5. preserve all taxonomy rows while suppressing 7 high-confidence aliases from card generation;
6. generate canonical card-level research/evidence scopes;
7. generate pending evidence-source slots;
8. validate IDs, counts, amendment membership, policy inheritance, alias suppression, and production-readiness state.

## Design rule

The blueprint separated **planning** from **truth**.

A planned card described what should eventually be researched and verified. It was never treated as a
factual knowledge record merely because a deterministic planner created it.

## Deterministic validation

The archived package included macOS and Windows validation paths and byte-for-byte comparison of major
generated machine-readable artifacts.

A later validator revision changed generated text/JSONL writing to explicit LF line endings across
supported operating systems so that newline translation would not create false SHA-256 mismatches.

The blueprint content and counts did not change as part of that newline fix.
