# FORGE-NOTE-004 — Evidence-Bound Knowledge Factory Pilot Design

**Date:** 2026-09-02  
**Status:** Published methodology note  
**Project:** FORGE AI / NexLabs

## Purpose

Before FORGE attempted large-scale knowledge generation, it built a deliberately small clean pilot:

- **15 topics**
- **2 cards per topic**
- **30 planned cards**
- cross-domain technical, general, and high-stakes coverage

The goal was not to generate a large corpus quickly.

The goal was to establish the rules that would prevent generated prose from silently becoming trusted knowledge.

## Evidence first

The pilot used curated authoritative source seeds and collected bounded evidence excerpts with provenance.

The evidence layer included:

- evidence hashing;
- source-organization metadata;
- SSRF-safe URL handling;
- redirect validation;
- optional Google/DDG discovery fallback;
- high-stakes independent-source requirements;
- bounded excerpt collection rather than wholesale page mirroring.

For high-stakes topics, independence was measured at the **organization** level rather than by hostname alone.

That prevented multiple domains belonging to the same organization from being mistaken for independent corroboration.

## Evidence quality gate

Before generation, collected evidence could be screened for:

- duplicate evidence;
- duplicate URLs;
- anti-bot/error-page contamination;
- prompt-injection-like text;
- topic mismatch;
- navigation/HTML artifacts;
- insufficient independent organizations for high-stakes use.

Weak or unrelated second sources were not allowed to satisfy high-stakes cross-check requirements.

## Card blueprint

Each pilot topic received an exact two-card contract.

The blueprint bound cards to:

- specific collected evidence;
- explicit allowed claim scopes;
- topic-specific exclusions;
- global synthetic-contamination exclusions;
- evidence hashes and provenance;
- focused retrieval-text seeds.

High-stakes cards received stronger source-relevance and review requirements.

Every planned card remained:

`production_ready = false`

until later factual verification.

## Generation contract

The evidence-bound candidate generator added:

- strict evidence-only prompting;
- atomic claim-to-source mappings;
- separate focused `retrieval_text`;
- schema and length validation;
- long verbatim-copy detection;
- regression guards for known synthetic contamination;
- personalized high-stakes advice guards;
- audit/failure logging.

Generated candidates remained:

- `verified = false`
- `production_ready = false`

and received **no trust assignment merely because a model generated them**.

## Why this mattered

This pilot established the core FORGE principle used by later experiments:

> Generation proposes knowledge. Evidence and verification decide whether anything becomes trusted.

That distinction later enabled claim-level verification, clean corpus construction, frozen retrieval benchmarks,
and the autonomous trusted-knowledge lifecycle.

## Limitation

This record describes the pilot's design and safeguards.

The supplied historical changelog does not contain a complete final per-card outcome table for all 30 cards,
so this public note does not invent one.
