# Methodology

## Defect detection

The completed A/B/C raw result matrix was audited after execution.

All 162 rows were successful, but every row had an empty `gold_claim_ids` array.

The defect was traced to the evaluator metadata path rather than to missing model execution.

## Immutable raw-run rule

The original raw result file was retained unchanged.

Its recorded SHA-256 was used as the identity of the frozen run.

## Offline gold reconstruction

Gold associations were rebuilt from the locked `reference_claim_ids` already present in the frozen evaluation inputs.

No answer was regenerated and no raw benchmark output was rewritten.

## Blinded judge inputs

One-answer judge records were produced from the repaired evaluation metadata.

Arm identity, runtime metrics, and system identity were omitted from judge inputs.

## Quality evaluation

A single evidence-bound LLM judge produced 162 judgments.

Aggregate quality scoring was performed only after the blinded judgments were complete.
