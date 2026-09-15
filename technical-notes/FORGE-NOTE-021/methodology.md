# Methodology

## Classification gate

Before an external request is issued, the refinery checks the task's classification.

Only `public_external` and `public_benchmark` are allowed. Private/internal classifications fail closed.

## Structured external analysis

The external provider receives bounded public task data and is required to return a strict structured schema.

For retrieval diagnosis, the schema includes an explicit `do_not_auto_promote=true` hard rail.

## Trust separation

Provider output is stored as candidate analysis with provenance and explicit trust metadata.

It is never marked as evidence or verified knowledge by the refinery itself.

## Queue durability

Tasks transition through persistent pending, processing, done, and failed directories.

Rate-limited tasks are requeued.

Successful and failed executions are recorded in a usage/audit ledger.

## Budget control

The worker tracks daily successful requests and token usage and stops before configured ceilings or reserved token capacity would be exceeded.

Provider rate limits trigger pacing/cooldown rather than policy bypass.

## Spare-quota enrichment

Claim enrichment runs only when the primary refinery queue is idle.

It reads already verified non-high-stakes claims and creates retrieval aids without modifying the trusted corpus or introducing new factual assertions.

## Deployment validation boundary

The refinery worker had real external-provider validation.

The later Windows service wrapper had compile/review validation but, at the recorded changelog checkpoint, not an actual Windows SCM user-environment PASS.
