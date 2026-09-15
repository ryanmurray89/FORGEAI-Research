# Methodology — FORGE-EXP-003

## Comparison design

This was a same-batch before/after rerun rather than a new benchmark sample.

**Unchanged between runs:**

- 120 complete cards
- 142 evidence slots
- 107 topics
- 15-domain batch composition
- canonical 759-topic / 3,982-card / 4,807-slot blueprint baseline
- evidence collector architecture
- offline auditor (`forge-kb-evidence-audit-001`)
- authoritative source registry
- trust families
- search fallback disabled
- no LLM-based evidence generation or judging

**Changed in v001.2:**

A deterministic scope-override configuration supplied more precise seed URLs for selected topic+scope rows. Overrides could only use source IDs and URL hosts already allowed by the existing source registry.

## Pre-correction diagnosis

The baseline audit produced 24 hard failures. Every hard issue had the same reason: `no_scope_term_match`.

The correction was therefore targeted at seed-to-scope precision rather than changing the collector or loosening the evidence gate.

## Correction constraints

The historical correction report records:

- 64 override rules
- 72 affected batch slots
- 51 affected topics
- 38 existing approved source IDs
- 77 exact seed URLs
- zero new source/trust families

Five previous terminal failure slots were intentionally unresolved rather than adding new trusted source families merely to improve the metric.

## Evaluation

Both runs were evaluated with the same offline evidence-quality audit. The card-level gate required the selected card's evidence obligations to pass the evidence-quality rules; evidence audit success alone did not authorize production card generation.

## Limitations

- The two live network runs were not conducted under frozen network conditions.
- Exact source URLs changed for affected rows by design.
- Fetch yield did not improve in the corrected run.
- PASS_WITH_WARNINGS remained common after correction.
- The result should be interpreted as a batch-specific evidence-quality improvement under a bounded scope-seed correction.
