# Methodology

## Gap detection

Persisted assistant responses are scanned after normal use.

A conservative policy identifies public-general-knowledge requests where retrieval was attempted but the resulting trust/retrieval
signals indicate KESPA may not know enough.

## Queue and handoff

Eligible requests are written into an isolated signed queue. A separate home-side poller retrieves jobs and acknowledges delivery.

The research result is emitted as a release package and handed back through a signed HMAC-authenticated receiver with timestamp,
nonce, replay protection, and release/hash validation.

## Research

The isolated worker gathers public evidence from multiple source organizations.

Search-result snippets are discovery aids only and are never considered evidence.

Claims require at least two independent source organizations and are refused entirely for high-stakes, sensitive, or time-sensitive
research classes.

## Import and promotion

The app-side isolated lifecycle validates the release package, imports a research candidate, performs local verification,
creates system-policy approval on PASS, promotes trusted knowledge, and indexes the promoted record.

A separate existing attestation path records the final trusted-knowledge asset in NexLedger.

## Validation

The full path was validated using the Cuckoo-filter question. Four candidate claims were generated and all four passed claim verification.
The resulting trusted-knowledge record was indexed and a NexLedger asset was confirmed.
