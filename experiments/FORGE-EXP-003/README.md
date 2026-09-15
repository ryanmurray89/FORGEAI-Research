# FORGE-EXP-003 — Seeded Evidence Scale: Scope-Precision Correction

**Original experiment date:** 2026-09-02  
**Public archive publication:** 2026-09-15  
**Status:** Verified historical experiment  
**Project:** FORGE AI / NexLabs

## Research question

When a fixed evidence-acquisition batch fails primarily because broad topic-level seed URLs do not match the exact card scope, can a bounded scope-specific seed correction improve evidence quality **without changing the canonical blueprint, acquisition architecture, or source trust registry**?

## Fixed batch

The before/after comparison used the same production Scale Batch 001:

- **120 complete cards**
- **142 planned evidence slots**
- **107 topics**
- **15 domains**
- search fallback: **OFF**
- LLM calls: **0**
- production Chroma writes: **0**
- Brain changes: **0**
- FORGE database writes: **0**

The v001.2 correction did not create a new batch and did not change the target set.

## Baseline result

The first live seeded-evidence run collected 98 evidence excerpts from the 142 planned slots. The offline evidence audit reported:

- **41 PASS**
- **33 PASS_WITH_WARNINGS**
- **24 NEEDS_REVIEW**
- **24 hard issues**, all `no_scope_term_match`
- **62 / 120 cards** passed the complete evidence gate (**51.7%**)

The observed hard failures pointed to seed precision: some approved topic-level source pages were too broad for the exact requested card scope.

## Bounded correction

The correction added a configuration-driven scope-specific seed layer:

- **64 deterministic override rules**
- **72 batch slots affected**
- **51 topics affected**
- **38 already-approved source IDs used**
- **77 exact authoritative seed URLs**
- **0 new source/trust families**
- canonical blueprint: **unchanged**
- source registry: **unchanged**
- collector architecture: **unchanged**
- search fallback: **OFF**

The correction covered all 24 prior hard `no_scope_term_match` rows with a more precise scope seed. Five prior terminal fetch slots were intentionally left unresolved instead of expanding trust solely to improve the score.

## Corrected rerun result

The same 120-card / 142-slot batch was rerun. It collected 97 evidence excerpts and the same offline auditor reported:

- **52 PASS**
- **44 PASS_WITH_WARNINGS**
- **1 NEEDS_REVIEW**
- **1 hard `no_scope_term_match` issue**
- **82 / 120 cards** passed the complete evidence gate (**68.3%**)

### Measured change

- Card evidence-gate passage: **51.7% → 68.3%**
- Absolute improvement: **+16.7 percentage points**
- Passing cards: **62 → 82** (**+20 cards**)
- Hard scope-match issues: **24 → 1** (**-95.8%**)
- PASS evidence rows: **41 → 52**
- PASS_WITH_WARNINGS rows: **33 → 44**
- Evidence excerpts audited: **98 → 97**

The corrected run did **not** improve raw fetch yield: it audited one fewer evidence excerpt. The result therefore supports a narrower conclusion — the scope-specific seed correction substantially improved the quality/gating outcome of the acquired evidence, not network reliability or source availability.

## Interpretation

This experiment supports the idea that evidence acquisition can fail because of **locator precision**, even when the source family itself is approved and the collector is functioning. A bounded scope-aware correction improved evidence-to-card fit without broadening trust policy or redesigning the acquisition mechanism.

That matters to FORGE because permanent knowledge depends on source evidence being relevant to the atomic scope it is supposed to support. More fetched text is not necessarily better evidence.

## What this does not prove

This is not a randomized experiment, and network conditions were not frozen between the two runs. The correction changed exact source URLs for affected slots, so the comparison demonstrates the behavior of this specific batch and policy configuration rather than a universal improvement rate.

The experiment also does not prove that the remaining PASS_WITH_WARNINGS rows are production-ready. The original audit explicitly required human review and prohibited card generation merely because an evidence row passed this audit stage.

## Historical source

This public record was reconstructed from the original internal FORGE research archive. The public package intentionally excludes implementation scripts, raw fetched third-party evidence text, private configuration, and duplicated baseline packages. Hashes for the source summary artifacts used to reconstruct this record are included in `provenance.json`.
