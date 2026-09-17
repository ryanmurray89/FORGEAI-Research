# KESPA-NOTE-015 — Trusted Knowledge Indexing Boundary and Private-Data Exclusion

**Date:** 2026-09-14  
**Status:** Verified — live production indexing confirmed  
**Project:** KESPA AI / NexLabs Studios

## Purpose

After the clean 423-claim production cutover, KESPA needed a controlled way for newly promoted trusted knowledge
to enter live semantic retrieval.

The indexing path could not simply accept arbitrary candidate text.

It also had to preserve the privacy boundary between:

- public promoted knowledge; and
- internal/private training material.

## Indexing contract

The production architecture established:

`MySQL trusted_knowledge = authoritative`

`Chroma forge_cards = rebuildable semantic index`

The live Brain added an authenticated:

`POST /knowledge/index`

for promoted knowledge ingestion.

The path allows **public promoted trusted knowledge** to enter `forge_cards`.

It explicitly blocks **internal/private plaintext** from the public promoted-knowledge Chroma indexing path.

## Why that separation matters

A vector database is optimized for retrieval, not for being the canonical trust ledger.

KESPA therefore keeps lifecycle state, provenance, verification, approval, and authoritative knowledge records
outside Chroma.

Chroma can then be rebuilt from trusted records if needed.

The index answers:

> What trusted information should be retrieved for this query?

It does not decide:

> What information deserves to be trusted?

## First live validation

The clean production index started at:

`423 cards`

The first promoted trusted record was indexed:

`trusted_knowledge #1`

Recorded indexed card:

`trusted-knowledge-b645128e-7020-4639-9e3e-7a21aaf36fc8`

Production index version:

`dev-013-trusted-knowledge-index`

Observed result:

- before: **423**
- after: **424**
- index status: **indexed**
- intended-query rank: **#1**
- website card counter reflected the live index

Result:

`PASS`

## Privacy boundary

The same architecture keeps internal/private Manual Train material outside the public external-evidence/index path.

That means the system does not solve knowledge growth by flattening every data class into one vector store.

Public knowledge and private/internal material retain different lifecycle rules.

## Research significance

This is a small but important control for continuous learning.

Without an explicit indexing boundary, a system can have excellent verification logic and still contaminate live retrieval
by allowing unpromoted or private material to bypass the trust lifecycle.

KESPA instead requires:

`candidate -> verification -> approval -> promotion -> indexing`

for public trusted knowledge.

## Limitation

This note proves the production indexing path and its data-class boundary.

It does not claim that one #1 retrieval result is a broad quality benchmark; retrieval effectiveness is evaluated in separate
benchmark records.
