# Methodology

## Evidence-bound generation

Before each generation request, the pilot verified the frozen evidence bindings used by the card blueprint.

The model was instructed to stay within the supplied evidence. Generated claims were mapped back to source
evidence rather than emitted as an unstructured trusted card.

## Validation

Candidate output was subjected to schema, content-length, verbatim-copy, contamination-regression, and
high-stakes language checks.

Trust remained deferred regardless of whether generation succeeded.

## Provider pacing

Provider headers and retry signals were used to regulate request timing. Calls were serialized where necessary
to protect the organization-level TPM budget.

Token/cost accounting included failed validation attempts rather than recording only accepted candidates.

## Deadlock regression

The pacing logic was explicitly tested against a request estimate larger than the entire nominal TPM bucket:
8,041 estimated tokens versus an 8,000 TPM limit.

The corrected logic bounded the wait threshold to a realizable value.
