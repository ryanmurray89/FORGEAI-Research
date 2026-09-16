# FORGE-NOTE-024 — Trusted Knowledge Freshness and Continuous Reverification Foundation

**Type:** Technical Note  
**Date:** 2026-09-15  
**Status:** published

## Summary

FORGE has begun extending Trusted Knowledge from a promotion-only lifecycle into a freshness-aware lifecycle that can distinguish durable knowledge from time-sensitive knowledge and eventually reverify it without repeatedly researching every known fact.

At this checkpoint, the **database foundation is complete**: `trusted_knowledge` has freshness-related state, `knowledge_refresh_jobs` exists, and FORGE's existing supersession/versioning mechanism can be reused when a trusted claim materially changes. The policy layer, scheduler/queueing worker, evidence reacquisition, comparison logic, stale-on-retrieval behavior, Admin controls, and refresh telemetry remain planned next-stage work.

This note intentionally documents the boundary between what is complete and what is still design/implementation work. It does **not** claim that continuous reverification is operational yet.

## Research / Technical Motivation

A verified knowledge system has two competing goals:

1. Reuse previously verified knowledge quickly rather than researching the same fact on every request.
2. Avoid treating time-sensitive knowledge as permanently true after its original verification.

The proposed lifecycle is:

```text
Don't know
→ acquire evidence
→ verify
→ Trusted Knowledge
→ RAG reuse
→ scheduled freshness checks
→ refresh / supersede / hold
→ continue serving current verified knowledge
```

The design therefore separates **knowledge reuse** from **knowledge freshness**. RAG can remain the fast path for known claims, while freshness policy determines when a claim must be checked again.

## Freshness Classes

The supplied design defines six freshness classes:

| Class | Intended role |
|---|---|
| `static` | Knowledge expected to change rarely or effectively never under normal operation. |
| `slow` | Knowledge that may change, but normally on long timescales. |
| `volatile` | Knowledge expected to require recurring reverification. |
| `highly_volatile` | Knowledge where short freshness windows may be appropriate. |
| `event_driven` | Knowledge refreshed in response to a relevant event rather than only a fixed interval. |
| `manual` | Knowledge refreshed only through an explicit human/system action. |

The exact refresh intervals are intentionally **not hard-coded in this note**. The plan is for them to live in `brain_config` / Admin so policy can be tuned without altering core runtime mechanics.

## Completed Foundation at This Checkpoint

Directly recorded as complete in the supplied project update:

- Freshness-related state has been added to `trusted_knowledge`.
- A `knowledge_refresh_jobs` queue table exists.
- Existing trusted-knowledge supersession/versioning can be reused for refreshed claims.

These changes establish the persistence layer needed for later scheduling and reverification.

## Planned Refresh Lifecycle

The remaining planned lifecycle is:

1. **Freshness policy**
   - Define class-specific policy in `brain_config` / Admin.
   - Track verification time, next refresh time, interval/state, attempts, and failures.

2. **Scheduler / queueing**
   - Find trusted rows that are due under current policy.
   - Queue bounded refresh jobs in `knowledge_refresh_jobs`.

3. **Evidence reacquisition**
   - Prefer authoritative sources and APIs where appropriate.
   - Allow web discovery and external/Groq assistance when appropriate to the existing evidence policy.

4. **Claim comparison**
   - Compare newly verified evidence with the currently trusted claim.

5. **Outcome handling**
   - **Unchanged:** refresh verification/freshness timestamps without creating unnecessary new knowledge.
   - **Changed:** create a newly verified claim and connect history through the existing supersession mechanism.
   - **Conflict / insufficient evidence:** hold for review instead of silently replacing trusted knowledge.

6. **Indexing behavior**
   - Re-index Chroma only when the trusted knowledge materially changes.
   - Avoid churn when reverification confirms the existing claim.

7. **Stale-on-retrieval behavior**
   - Requests containing freshness-sensitive intent such as “latest” or “current” may trigger revalidation when the trusted claim is stale or otherwise due.

8. **Operational visibility**
   - Admin views for freshness state, overdue knowledge, queued refreshes, failures, conflicts, and manual reverification.
   - Telemetry for refresh frequency, latency, provider usage, cost, unchanged-vs-changed outcomes, and knowledge reuse.

## Supersession Model

A material change should not overwrite history in place. The design reuses the existing trusted-knowledge versioning boundary:

```text
old trusted claim
→ status = superseded
→ new verified claim
→ supersedes_knowledge_id = prior knowledge row
```

This preserves lineage and allows FORGE to distinguish “previously verified but no longer current” from “never trusted.”

## Re-indexing Boundary

The proposed indexing rule is deliberately narrow:

```text
reverification confirms same trusted claim
→ update freshness metadata
→ no material Chroma rewrite

reverification produces materially changed trusted claim
→ promote/supersede
→ re-index affected trusted knowledge
```

This keeps the rebuildable retrieval index aligned with authoritative Trusted Knowledge while avoiding unnecessary index churn.

## Validation Boundary

No database dump, migration SQL, scheduler execution, refresh-job run, provider trace, changed-claim example, conflict example, or end-to-end reverification result was supplied for this artifact.

Accordingly:

- The **database foundation** is recorded as completed project state.
- The **continuous reverification architecture** is documented design.
- The scheduler and full refresh lifecycle are **not claimed operational**.
- Status is therefore **published**, not `verified`.

## Next Recorded Implementation Step

The supplied project update identifies the next implementation step as:

```text
freshness policy in brain_config / Admin
+ scheduler / queueing worker
```
