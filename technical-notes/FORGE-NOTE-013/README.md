# FORGE-NOTE-013 — Frozen Benchmark Construction and Evaluation Leakage Prevention

**Date:** 2026-09-04  
**Status:** Verified — user environment  
**Project:** FORGE AI / NexLabs

## Purpose

Before comparing retrieval policies or running the A/B/C benchmark, FORGE created a fixed benchmark from the
clean **423-claim verified corpus**.

The important design decision was to separate:

`calibration`

from:

`evaluation`

so retrieval-policy tuning could not simply inspect and optimize against the final benchmark questions.

## Benchmark split

The benchmark builder produced:

- **66 total questions**
- **12 calibration questions**
- **54 locked evaluation questions**
- coverage of **423 gold claims**
- **0 high-stakes calibration questions**
- **2 high-stakes evaluation questions**

## Freeze procedure

Before calibration:

- the evaluation artifact was frozen;
- its SHA-256 was recorded;
- calibration tooling verified the evaluation hash;
- the evaluation questions themselves were **not parsed**;
- only the 12 calibration questions were loaded.

Recorded calibration output explicitly showed:

`Evaluation questions parsed: 0`

and:

`Evaluation hash verified: YES`

## Why this matters

A retrieval policy can look artificially strong if its thresholds, filters, or ranking rules are repeatedly tuned while
the final evaluation questions are visible.

FORGE instead used:

`12 calibration questions -> policy selection`

followed by:

`54 locked evaluation questions -> final experiment`

That does not make the benchmark perfect, but it creates a much cleaner experimental boundary.

## Frozen artifact hashes

```text
benchmark_calibration_v001.jsonl
366CA6A74CE2EDE4ABAF2DC9EE4641241AC5E57BFF99BCB1319415626A3BC60C

benchmark_evaluation_v001.jsonl
0EE67DE597B793A7A7665558AA97382494989A681376C59454ED4257455ACC62

benchmark_question_manifest_v001.json
D319B7F8E3ED9379ECAEFE47E4F0C3DEDE78F57450390C054B87AD3D757A74F7

benchmark_questions_v001.jsonl
D10807FCE5C049C991B5AAA4611D1D6D30D2EE61A526B4874DFE05D1F5BB7DBC
```

## Experimental isolation

During calibration:

- production Chroma opened: **NO**
- production Chroma modified: **NO**
- Brain modified: **NO**
- database modified: **NO**

The work stayed inside the isolated benchmark environment.

## Research significance

This benchmark freeze is the methodological bridge between the clean-corpus work and the later A/B/C and D experiments.

It provides a reproducible answer to:

> Which questions were used for tuning, and which questions were reserved for final evaluation?

## Limitations

The freeze prevents direct calibration-set/evaluation-set mixing, but it does not prove the benchmark is universally representative.

The questions still came from one fixed verified corpus and one research program's domain coverage.
