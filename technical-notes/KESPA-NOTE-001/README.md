# KESPA-NOTE-001 — Knowledge Blueprint v004: Deterministic Bootstrap Planning

**Date:** 2026-09-02  
**Status:** Verified — deterministic user-environment validation  
**Project:** KESPA AI / NexLabs Studios

## What this document records

Before KESPA could build a trusted corpus, it needed a deterministic plan for what knowledge should exist,
how many research/evidence scopes should be created, and which topics required stronger review.

Blueprint v004 was that planning artifact.

It did **not** generate factual knowledge.

## Starting point

The recovered taxonomy contained:

- **729 taxonomy rows**
- **3,810 corrected pre-amendment planned cards**
- **24 audited unsafe classifications**
- **20 domain changes**

A bounded foundational-gap amendment then added exactly:

- **37 approved topics**
- **207 planned card scopes**

This produced:

- **766 total taxonomy rows**
- **4,017 raw planned cards before alias suppression**

## Canonical result

After suppressing **7 existing aliases**, KESPA produced:

- **759 canonical generating topics**
- **3,982 unique planned card scopes**
- **4,807 planned evidence-source slots**

Every planned card remained:

- **production-ready: false**
- **selected evidence URLs: 0**

No filler was added merely to reach a round corpus-size target.

## Safety and review planning

The blueprint marked:

- **216 high-stakes cards**
- **467 safety-sensitive cards**
- **216 human-review cards**
- **2,975 technical-validation cards**
- **216 cross-check-required cards**

This metadata controlled later evidence and verification behavior; it did not itself make any claim trustworthy.

## Largest planned domains

- Web/backend: **912 cards**
- Infrastructure/DevOps: **876**
- Database/data: **378**
- Security: **364**
- AI/ML: **324**
- Business/finance: **308**

The approved amendment also introduced narrowly scoped `software_engineering` and `business_operations`
domains for newly added foundational topics.

## Determinism

The historical candidate included deterministic builders and validators.

The archived local validation recorded:

- all pipeline scripts compiled successfully;
- the exact 729-row baseline hashes were checked;
- the approved amendment count was exactly 37;
- final blueprint IDs were unique;
- major machine-readable artifacts reproduced byte-for-byte;
- explicit LF newlines were later enforced across operating systems so deterministic SHA-256 comparisons would survive Windows newline translation.

## Why this mattered

The purpose was not to maximize corpus size.

The purpose was to define an auditable research plan before spending provider tokens or generating
persistent knowledge. Known foundational gaps were corrected before evidence acquisition so later
retrieval/answer benchmarks would not be biased by intentionally missing basic concepts.

## Important boundary

This note documents a **planning-stage artifact**.

At this point:

- no factual production cards had been generated;
- no evidence had been fetched;
- no provider/model calls were made;
- production Chroma was unchanged;
- Brain was unchanged;
- the database was unchanged.

The original public record was conservatively marked **published** because the first source archive did
not yet contain the separate user-environment validation result.

A later KESPA changelog/Jira record supplied that missing result:

- Windows Python: **3.11.9**
- deterministic v004 rebuild: **byte-for-byte match**
- blueprint counts: **unchanged**
- production state changes: **none**
- final validator result: **`[PASS] Windows validation completed successfully`**

Because the missing user-environment validation was later supplied, this public record is now correctly
marked **verified**.

That verified status applies to the deterministic blueprint artifact and its reproduction, not to the
factual truth of future cards that the blueprint planned.
