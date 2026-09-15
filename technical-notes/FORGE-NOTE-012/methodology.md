# Methodology

## Research construction

Evidence was first acquired through the safe-fetch stage and then passed through evidence audit.

Candidate claims were constructed from the audited evidence and evaluated by a claim-support verifier.

## Release gate

A separate research-release policy decided whether the research package was eligible to become a trusted release.

The trusted-release stage froze the eligible claims/evidence into a release artifact before application import.

## Application promotion

The release entered the application as a `research_release` candidate.

After the application-side trust lifecycle completed, the candidate was promoted into trusted knowledge and indexed into live retrieval.

## Ledger attestation

The existing generic NexLedger worker processed the promoted trusted-knowledge record and created its attestation.

The proof did not require modifying the NexLedger worker.

## Validation

The complete path was validated with a systemd research release containing six verified claims and one evidence record.

The resulting trusted record was confirmed active/public/indexed and retrievable by the live Brain.
