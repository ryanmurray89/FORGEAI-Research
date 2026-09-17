# Methodology

## Runtime evidence source

The automation consumes closed telemetry from the live KESPA runtime on RYANDESKTOP rather than scraping an active/incomplete request.

Selected telemetry is aggregated on the research/home server.

## Safe evidence construction

The automation converts the selected aggregate into a safe `MET` research-evidence record.

The public architecture does not require private prompt/answer plaintext or source code to be written to NexLedger.

## Signed intake

Evidence crosses into the application side through a signed intake rather than an unauthenticated write path.

Accepted evidence is recorded in MySQL.

## Ledger attestation

A generic worker processes eligible accepted evidence and submits the corresponding provenance attestation to NexLedger.

MySQL remains authoritative; NexLedger supplies the tamper-evident evidence/provenance layer.

## Benchmark watch

The same automation watches for completed benchmark runs and can produce `BM` evidence from eligible completed-run outputs.

## Cadence

The operational automation runs hourly.

This converts evidence preservation from a manual post-run task into a recurring system process.
