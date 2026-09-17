# Methodology

## Recovery

The legacy corpus was used to recover the set of original subject areas without accepting its generated card bodies as trustworthy production knowledge.

Each recovered base topic received:

- corpus/contamination statistics;
- a rebuild classification;
- classification-source metadata;
- optional heuristic research-lead terms that were explicitly not promoted as facts.

## Ambiguity resolution

The initial recovered manifest contained 121 topics requiring manual classification.

Those topics were explicitly assigned to either:

- `TECH_REVIEW`, or
- `REBUILD_FROM_SOURCE`.

After resolution, no `MANUAL_CLASSIFY` backlog remained.

## Preservation rule

The existing synthetic corpus was kept immutable as archive/research material.

The recovery process did not rewrite `all_cards.jsonl`, production Chroma, or `brain_api.py`.

## Rebuild rule

Production knowledge was to be rebuilt from authoritative evidence with explicit source, freshness, verification, and trust contracts.

That decision separated coverage recovery from factual trust.
