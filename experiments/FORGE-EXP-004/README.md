# FORGE-EXP-004 — Full Seed-Ready Evidence Scale Run

**Date:** 2026-09-03  
**Status:** Published historical scale study  
**Project:** FORGE AI / NexLabs

## Research question

How does FORGE's seeded evidence-acquisition and quality-gating pipeline behave when expanded from a
bounded 120-card test batch to the full seed-ready population available at that stage?

## Run scope

The historical run selected:

- **3,128 evidence slots**
- representing **2,831 cards**

The run used seeded authoritative-source acquisition rather than general search fallback.

## Acquisition result

FORGE recorded:

- **2,146 evidence excerpts collected**
- **982 terminal `SEED_FETCH_FAILED` slots**
- **0 seed-not-ready skips**
- **441 network requests used**

The original acquisition summary also recorded **1,469 fetch failures**. That counter is preserved as
reported, but it is not treated as equivalent to the **982 terminal failed slots** in the queue status counts.

Safety rails remained active:

- Search fallback: **OFF**
- Full-page mirroring: **NO**
- LLM calls: **0**
- Chroma writes: **0**
- Brain changes: **0**
- Database writes: **0**

## Evidence-quality audit

The audit evaluated all **2,146 collected evidence excerpts** across **2,831 cards**.

Source-quality outcomes:

- **835 PASS**
- **848 PASS_WITH_WARNINGS**
- **463 NEEDS_REVIEW**

Card-level gate:

- **1,555 / 2,831 cards passed**
- **54.9% card-level gate passage**

Hard issues:

- **463** `no_scope_term_match`

Warnings:

- **840** `weak_scope_term_match`
- **11** navigation-boilerplate-heavy
- **6** suspected encoding artifacts

Duplicate signals:

- **161** duplicate evidence hashes
- **145** duplicate final URLs

## Result

This was **not** a clean-corpus success result.

It was a scale test that showed two things at once:

1. the seeded collector could operate across thousands of planned evidence slots; and
2. scaling exposed enough evidence-quality and scope-matching problems that the pipeline could not
   responsibly proceed directly to knowledge-card generation.

The next gate explicitly required review of failed and warned evidence rows.

## Why this matters

FORGE's evidence lifecycle was designed to fail closed.

A weaker system could have interpreted "2,146 excerpts collected" as permission to generate thousands
of knowledge cards. FORGE did not. The evidence-quality gate held the corpus because only **1,555 of
2,831 cards** met the complete evidence gate in this run.

That negative/partial result is part of the research record.

## What this does not prove

This experiment does not measure end-user answer quality, production reliability, or general model
capability. It also does not mean that every passing card later became trusted knowledge.

It measures the behavior of the evidence-acquisition and quality-gating subsystem under a materially
larger workload.
