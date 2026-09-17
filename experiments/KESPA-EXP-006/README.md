# KESPA-EXP-006 — Autonomous Trust Policy v0.1 → v0.2 Backlog Reclassification

**Date:** 2026-09-14  
**Status:** Published policy experiment  
**Project:** KESPA AI / NexLabs Studios

## Research question

Can KESPA reduce unnecessary human-review load by changing only the supporting-evidence threshold
while preserving its other verification, consensus, confidence, and conflict gates?

## Policy v0.1

The original autonomous publication policy required:

- verification: **PASS**
- confidence: **>= 0.90**
- AI consensus: **yes**
- qualifying evidence: **>= 2**
- supporting evidence: **>= 2**
- conflicting evidence: **0**
- verifier conflict: **false**

Successful autonomous approvals were recorded as:

- `approver_type = system_policy`
- `policy_version = forge-auto-publish-policy-v0.1.0`

## Observed product problem

The backlog was producing more human-review cases than desired for routine public knowledge.

The research concern was not simply "make everything green."

The goal was to determine whether otherwise strong candidates were being held because the publication
policy required two independently classified supporting evidence items even when verification,
consensus, confidence, and conflict checks were already favorable.

## Policy v0.2

The policy change was deliberately narrow:

`minimum supporting evidence: 2 -> 1`

The source record states that all other trust, conflict, and consensus requirements were retained.

System-generated publish jobs also used real `system_policy` approval metadata aligned to:

`forge-auto-publish-policy-v0.2.0`

## Backlog reclassification result

Applying the revised policy to the already processed backlog made:

- **29 previously held candidates newly eligible**
- with **no evidence recollection**
- and **no local reverification**

Recorded autonomy estimate:

- v0.1 backlog autonomy: **36.7%**
- v0.2 projected backlog autonomy: **~95.9%**
- absolute change: **+59.2 percentage points**

## Why this is useful experimentally

This is cleaner than regenerating the candidates under a new pipeline.

The upstream candidate evidence and local verification remained the same. The changed variable was the
publication-policy threshold for supporting evidence.

That makes the backlog useful as a policy-reclassification study.

## Important limitation

**~95.9% is a projected/expected backlog autonomy figure, not a completed prospective production success rate.**

A higher automation rate is not enough to validate the policy.

The next scientifically useful comparison should measure whether v0.2 changes:

- false acceptance;
- false rejection;
- human-review rate;
- conflict detection;
- evidence quality;
- verification accuracy;
- latency/compute/energy.

The objective remains maximizing safe autonomous knowledge acquisition, not maximizing auto-publication by itself.
