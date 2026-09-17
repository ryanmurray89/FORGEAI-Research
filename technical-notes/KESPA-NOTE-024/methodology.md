# Methodology

## Purpose

This artifact converts a KESPA implementation/Jira update into a public technical record while preserving the distinction between completed foundation work and future lifecycle design.

## Source Handling

The supplied raw update was treated as the factual source of truth. Duplicate text in the dump was deduplicated before packaging.

The artifact was compared against the existing public manifest. The closest existing records describe:

- autonomous trusted-knowledge promotion,
- trusted research release promotion,
- trusted-knowledge indexing and private-data exclusion,
- autonomous natural research-gap acquisition,
- and the public research archive.

None of those entries documents post-promotion freshness policy, scheduled reverification, change detection, or supersession-on-refresh as its primary technical purpose. This lifecycle was therefore treated as a materially distinct technical note rather than an update to an existing package.

## Classification

The package is classified as `technical_note` because the supplied material primarily documents architecture, persistence foundations, policy boundaries, and an implementation plan rather than a completed controlled experiment or benchmark.

The status is `published`, not `verified`, because the source states that the database foundation is complete but does not include live schema output, scheduler execution, queued job output, refresh-worker traces, or end-to-end reverification results.

## Recorded vs Derived Content

### Directly recorded

- Trusted Knowledge freshness lifecycle is the module goal.
- Six named freshness classes are planned.
- Database foundation is complete.
- `trusted_knowledge` has freshness-related state.
- `knowledge_refresh_jobs` exists.
- Existing supersession/versioning can be reused.
- Freshness policy belongs in `brain_config` / Admin rather than hard-coded runtime intervals.
- The next implementation step is policy configuration plus scheduler/queueing.
- Planned outcomes include unchanged refresh, changed-claim supersession, review holds, material-change re-indexing, stale-on-retrieval checks, Admin visibility, and telemetry.

### Derived

- `freshness_classes_defined = 6`, obtained by counting the six explicitly named classes.

No other numerical performance, cost, latency, provider, or refresh metrics were derived because the source did not provide execution data.

## Publication Safety

No credentials, prompts, user data, raw telemetry, private source code, API secrets, IP addresses, or private evidence bodies were included.

## Validation Limitations

This artifact does not establish that:

- any refresh interval has been configured,
- any scheduler has run,
- any refresh job has been queued or processed,
- any evidence has been reacquired,
- any trusted claim has been refreshed or superseded through this module,
- any conflict has been held for review,
- or any Chroma record has been re-indexed through a freshness event.

Those results should become future artifacts only after concrete execution evidence exists.
