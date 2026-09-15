# FORGE-NOTE-022 — Source-Organization Independence and High-Stakes Evidence Policy

**Date:** 2026-09-01  
**Status:** Published historical technical record  
**Project:** FORGE AI / NexLabs

## Purpose

One of the first Knowledge Factory safety corrections was deceptively simple:

> **Two different domains do not necessarily mean two independent sources.**

FORGE initially had evidence mechanics that could reason about source/domain counts.

That was not strong enough for high-stakes corroboration.

The policy was hardened so evidence independence is measured by **source organization**, not merely hostname.

## Independence correction

The pilot evidence system changed from:

`hostname/domain count`

to:

`source-organization count`

Evidence records gained explicit:

`source_organization`

provenance.

Evidence reports also gained organization counts.

This prevents one organization operating several domains from accidentally satisfying an independence requirement multiple times.

A specific correction also prevented SEC-related domains from being falsely counted as separate independent organizations.

## High-stakes policy

Cognitive Behavioral Therapy (CBT) was promoted into the high-stakes verification policy.

The evidence path added independent cross-checking rather than allowing a single authoritative-looking source to satisfy the full requirement.

The same architecture supports stricter handling across health, legal, finance, security, and other higher-risk knowledge domains.

## Pilot source hardening

Several pilot source sets were corrected.

### CBT

Failed seeds were replaced with sources from:

- NIMH
- APA
- VA

### Cooking / food safety

Failed source URLs were replaced with:

- FoodSafety.gov
- current USDA FSIS material

### Investing

The U.S. Department of Labor was added as an independent evidence source.

### Copyright

Official **U.S. Code Title 17** was added as independent evidence.

## Additional evidence rails

The same implementation period also added or preserved:

- evidence-excerpt-only collection;
- explicit source-usage review;
- evidence hashing;
- provenance metadata;
- SSRF-safe public URL handling;
- redirect validation;
- high-stakes multi-domain evidence gates;
- curated authoritative source seeds;
- optional Google/DDG fallback discovery.

OpenStax was removed from the automated AI-ingestion source policy during this hardening pass.

Unknown/new source families were intended to default toward review rather than implicit trust.

## Why organization identity matters

Consider three pages:

```text
docs.example.org
research.example.org
support.example.com
```

Counting hostnames would produce:

`3 sources`

But if all three are controlled by the same organization, they are not three independent corroborators.

FORGE's corrected model asks:

`How many independent source organizations support this?`

not merely:

`How many URLs/domains did we collect?`

That is a stronger basis for evidence policy.

## Separation from generation

This work changed source qualification and evidence provenance.

It did **not**:

- call an LLM;
- generate knowledge cards;
- write to Chroma;
- change `brain_api.py`.

That separation allowed evidence-policy mechanics to be tested without confusing source quality with model behavior.

## Validation

The historical implementation record reports:

- syntax validation: **PASS**
- offline cross-check policy tests: **PASS**
- LLM calls: **0**
- Chroma changes: **0**
- Brain API changes: **0**

## Research significance

This correction is part of a broader FORGE principle:

> **Corroboration should represent genuinely independent evidence, not superficial URL diversity.**

That matters particularly for automated knowledge systems because a naïve source counter can manufacture confidence from multiple pages that all trace back to the same institution.

## Limitation

This note records policy mechanics and offline validation.

It does not claim a measured reduction in false factual acceptance across a statistically representative high-stakes dataset.

That question requires separate empirical evaluation.
