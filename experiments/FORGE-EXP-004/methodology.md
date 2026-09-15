# Methodology

## Source experiment

This public record reconstructs the historical `seed_ready_full_run` from the internal
`FORGE_seeded_evidence_scale_v001_2_windows_candidate` package.

The public package does not republish raw third-party evidence excerpts, internal scripts, private
configuration, or the historical Git repository.

## Acquisition stage

The collector selected the full seed-ready queue available to the v001.2 package.

Recorded acquisition outputs included:

- queue results;
- evidence-source rows;
- terminal failure rows;
- acquisition summary;
- evidence-quality audit.

General search fallback remained disabled.

## Quality stage

Collected excerpts were evaluated by `forge-kb-evidence-audit-001`.

The audit classified evidence rows as:

- `PASS`
- `PASS_WITH_WARNINGS`
- `NEEDS_REVIEW`

It also calculated card-level gate passage and tracked duplicate evidence hashes, duplicate final URLs,
hard scope failures, and warning classes.

## Release decision

The audit explicitly instructed:

> Do NOT generate cards until the selected acquisition batch passes evidence quality gates.

Accordingly, this public study treats the run as a measured scale experiment, not a production knowledge release.
