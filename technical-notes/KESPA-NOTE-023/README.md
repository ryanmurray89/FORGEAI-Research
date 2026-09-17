# KESPA-NOTE-023 — Deterministic Evidence Acquisition Preflight and Bounded Smoke Harness

**Date:** 2026-09-02  
**Status:** Published historical technical record  
**Project:** KESPA AI / NexLabs Studios

## Purpose

Once KESPA had a deterministic knowledge blueprint, the next problem was much larger:

> How do you safely acquire evidence for thousands of planned knowledge scopes without immediately launching thousands of network fetches?

The Evidence Acquisition v001 preflight created a bounded test harness first.

## Canonical acquisition scope

The validated blueprint produced:

- canonical topics: **759**
- canonical card scopes: **3,982**
- evidence-source slots: **4,807**

The evidence workload was split into explicit roles:

- primary: **3,982**
- supporting: **609**
- cross-check: **216**

Those roles sum to the full **4,807-slot** acquisition plan.

## Acquisition components

The preflight introduced:

- a full blueprint evidence collector;
- an offline evidence-quality auditor;
- a deterministic representative smoke selector;
- an acquisition invariant validator;
- a conservative **60-family** source-policy catalog;
- a Windows offline validation wrapper;
- a bounded Windows network-smoke wrapper.

The validated v004 blueprint itself remained unchanged.

## Deterministic smoke

Instead of testing the entire 4,807-slot queue first, KESPA generated a bounded representative smoke:

- **28 evidence slots**
- **24 topics**

The smoke's deterministic SHA-256 reproduced byte-for-byte.

That matters because the same bounded workload can be reused after changes to discovery or source-policy mechanics.

## Discovery is separate from acquisition

The preflight explicitly separated:

`candidate source discovery`

from:

`page-content acquisition`

Finding a URL is not evidence.

A source still has to survive the acquisition and evidence-quality rails.

## Conservative source handling

The acquisition candidate included controls for:

- unknown sources -> `REVIEW_REQUIRED`;
- SSRF-safe URL handling;
- redirect validation;
- robots policy;
- AI-exclusion handling;
- bounded evidence excerpts.

PDF ingestion was deliberately deferred.

## Recorded validation

The historical checkpoint recorded:

- Python compilation: **PASS locally**
- full queue recognized: **4,807**
- cards reconciled: **3,982**
- canonical topics: **759**
- smoke build: **28 slots / 24 topics**
- smoke deterministic SHA-256: **reproduced byte-for-byte**
- full collector offline preflight: **PASS locally**
- input/catalog invariant validation: **PASS locally**
- evidence auditor mechanical harness: **PASS locally**
- network calls during validation: **0**

## Important validation boundary

The same record explicitly says:

`RESULT: NOT YET EXECUTED on your Windows KESPA environment`

for the live bounded network smoke at that checkpoint.

So this note is intentionally marked **published**, not verified from a live Windows acquisition run.

Later experiments separately document the actual v001/v001.1/v001.2 live discovery behavior and the seeded scale runs.

## Safety / data impact

During this preflight:

- production Chroma changed: **NO**
- Brain API changed: **NO**
- database changed: **NO**
- private-data routing changed: **NO**
- DeepInfra usage: **NONE**
- Groq usage: **NONE**
- external web usage during candidate validation: **NONE**
- production-ready evidence created: **0**

## Why this matters

The preflight made a large evidence campaign testable before spending network/provider resources.

It also separated three questions that are easy to accidentally collapse:

1. **What knowledge scopes exist?**
2. **Where might evidence be found?**
3. **Does directly retrieved evidence actually satisfy the scope and quality gates?**

That separation made the later source-discovery and scale experiments much easier to diagnose.

## Limitations

This is an acquisition-mechanics record, not a live coverage result.

The later evidence-discovery and scale experiments provide the empirical network outcomes.
