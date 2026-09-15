# FORGE-NOTE-010 — Autonomous Natural Research Gap Lifecycle

**Date:** 2026-09-15  
**Status:** Verified — end-to-end production path proven  
**Project:** FORGE AI / NexLabs

## Purpose

FORGE's manual trusted-knowledge lifecycle could already take supplied training material through evidence,
verification, approval, promotion, and indexing.

The next step was harder:

> Can FORGE detect when it does not know enough during normal use, research the missing public-general
> knowledge, verify it, and add it to trusted knowledge without silently weakening the existing trust boundary?

The natural-research lifecycle was built as an **isolated path** rather than by modifying the older manual
learning pipeline.

## Trigger policy

A normal response can become a research-gap candidate when the recorded request satisfies conservative conditions such as:

- Brain response path;
- non-cache request;
- RAG actually searched;
- learning-style goal;
- trust after response at or below **0.72**;
- best RAG score at or below **0.45**, or no useful result.

The detector excludes:

- private/internal requests;
- memory-related requests;
- high-stakes requests;
- ordinary routing-only misses.

Eligible jobs are classified as:

`public_general_knowledge`

## Isolated research flow

The implemented path is:

`normal question -> gap detector -> signed queue -> research worker -> evidence -> claims -> release -> signed handoff -> verification -> approval -> trusted knowledge -> index -> NexLedger`

The research worker does **not** modify, wrap, or piggyback on the legacy/manual lifecycle scripts.

## Evidence policy

The natural-research worker uses a stricter rule than ordinary search-assisted answering:

- search snippets are **never** factual evidence;
- each promoted claim requires support from at least **2 independent source organizations**;
- high-stakes, sensitive, and time-sensitive requests are refused by this worker;
- claims are verified before release;
- the imported release is verified again before promotion.

## End-to-end proof: Cuckoo filter

The first full natural-gap proof used the question:

`What is a Cuckoo filter?`

Recorded lifecycle:

- request: `research-gap-20a905c55f6ad819c57f6920`
- release: `forge-release-07990ffc7fc9d09f9be2dd3b`
- release SHA-256:  
  `07990ffc7fc9d09f9be2dd3b5594285e5ee0789f7430e24fb1a812cbbf996ed3`
- evidence sources: **3**
- independent source organizations: **3**
- candidate claims: **4**
- verified claims: **4**
- Groq requests: **2**
- Groq tokens: **11,034**
- imported candidate: **#82**
- promoted trusted knowledge: **#74**
- NexLedger asset: **FORGEAI#TK123V1**

Final result:

`PASS`

## Why this matters

This turns "learning from use" into a controlled research lifecycle rather than a model-memory shortcut.

The system does not persist a weak answer merely because a user asked a question.

Instead:

`low-confidence gap -> explicit research -> evidence -> verification -> trusted promotion`

That preserves the core FORGE rule:

> Candidate intelligence is not trusted knowledge.

## Boundary

This path was intentionally isolated from the older manual lifecycle.

The proof did not require changing the legacy/shared learning scripts, and search snippets were never accepted as evidence.

The authoritative record remains trusted knowledge; the semantic index remains rebuildable.

## Limitation

One successful Cuckoo-filter run proves the machinery works end to end.

It does **not** establish a mature autonomous-research accuracy rate. That requires many more runs with measured false acceptance,
false rejection, source quality, research yield, latency, token cost, and energy.
