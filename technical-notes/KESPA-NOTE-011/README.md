# KESPA-NOTE-011 — Automated Research Evidence Capture and NexLedger Attestation

**Date:** 2026-09-14  
**Status:** Verified — operational automation completed  
**Project:** KESPA AI / NexLabs Studios

## Purpose

KESPA already produced useful telemetry and benchmark artifacts, but research evidence is much less useful if it
depends on somebody remembering to manually collect and preserve it after every run.

The evidence automation closes that gap.

It turns selected completed runtime/benchmark evidence into a repeatable provenance pipeline.

## Operational topology

The evidence path spans KESPA's existing hosts:

- **RYANDESKTOP** — live Brain/runtime machine
- **NVIDIA RTX 3070 8GB** — local inference GPU
- **DESKTOP-S16TRCC** — research/home server used for aggregation and background work
- **app-nexlabs** — application side, including signed evidence intake and database persistence

The home server remains the research/storage/background-work machine; it is not the live Brain.

## Hourly MET evidence flow

The completed automation runs **hourly**.

Its operational flow is:

`closed RTX 3070 telemetry -> home-server aggregation -> safe MET evidence -> signed intake -> MySQL -> generic NexLedger worker`

In words:

1. Read **closed telemetry** from `RYANDESKTOP`.
2. Aggregate the selected telemetry on the home/research server.
3. Construct a safe research-evidence payload classified as **MET**.
4. Send that payload through the signed intake.
5. Record the accepted event in MySQL.
6. Let the existing generic worker create the NexLedger attestation.

## Benchmark evidence

The same automation also watches for future **completed benchmark runs**.

Eligible completed-run evidence is handled as **BM** evidence rather than requiring a one-off manual attestation process for every benchmark.

That gives KESPA a durable evidence path for both:

- runtime/telemetry research snapshots — `MET`
- completed benchmark evidence — `BM`

## Why the pipeline is separated into stages

The system deliberately does not treat NexLedger as the application database.

The roles remain:

`runtime telemetry -> evidence construction -> signed intake -> MySQL authoritative record -> NexLedger attestation`

This separation allows KESPA to preserve normal application/database semantics while still creating a tamper-evident external provenance record for selected research evidence.

## Ledger scope remains narrow

The automation does **not** expand NexLedger into a general activity log.

The ledger is not for:

- routine Git commits or pushes;
- source-code history;
- ordinary deployment events;
- private prompt/answer plaintext;
- user profile or leaderboard statistics.

The evidence path is reserved for externally useful research/provenance material such as meaningful telemetry snapshots and completed benchmark evidence.

## Research significance

This automation matters because measurement provenance is now part of the system rather than a manual afterthought.

Future research can accumulate evidence continuously while retaining a defined chain:

`measurement -> aggregation -> signed submission -> authoritative DB event -> attestation`

That is useful for later benchmark comparison, grant/research documentation, investor diligence, and reproducibility work.

## Limitation

An attestation proves that a particular evidence record was committed through the pipeline.

It does **not** prove that the underlying experiment was well designed or that an interpretation is correct.

Scientific validity still depends on the experiment, measurement protocol, and analysis.
