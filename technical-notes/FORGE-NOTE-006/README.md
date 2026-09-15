# FORGE-NOTE-006 — Compute-Aware Model Routing and Telemetry Foundation

**Date:** 2026-09-04  
**Status:** Verified — actual FORGE machine  
**Project:** FORGE AI / NexLabs

## Purpose

Before FORGE could make defensible claims about adaptive inference or compute efficiency, it needed to
measure its own runtime and make routing behavior controllable.

This milestone validated the infrastructure for that work.

## Validated runtime components

On the actual FORGE machine, the historical record reports:

- Brain API: **PASS**
- Models Admin: **PASS**
- Telemetry Admin: **PASS**
- persistent telemetry: **PASS**
- metrics endpoint: **PASS**
- RTX 3070 telemetry: **PASS**

Production Chroma was not modified.

Database impact was limited to configuration additions.

Private routing remained local by default, and no new request-time external-provider dependency was added.

## Why routing configuration mattered

An early routing rule treated broad technical terms such as `docker` as coding intent.

That produced a useful failure case:

- a Docker explanation request could be misrouted as coding;
- an actual Python implementation request should still route as coding.

The coding-keyword policy was narrowed and then validated:

- Docker explanation -> **learn / instant — PASS**
- Python implementation request -> **build / coding — PASS**
- telemetry requests -> **3/3 successful**

## Research significance

This was infrastructure work, but it removed two major experimental problems.

First, FORGE could now persist runtime telemetry instead of relying on ad hoc observations.

Second, routing behavior could be changed through configuration/Admin policy rather than being inseparable
from model/runtime mechanics.

That separation became important for later work on:

- adaptive inference;
- escalation policy;
- latency and energy measurement;
- role-specific model selection;
- future GPU/model swaps.

## Hardware boundary

The machine used an **NVIDIA RTX 3070**.

At this point, the single-GPU setup supported one resident primary model, so multiple logical model roles
did not yet mean multiple simultaneously resident specialized models.

That limitation is part of the research record rather than something to hide.

## Boundary

This milestone did not modify production Chroma and did not add a new cloud dependency to normal request handling.

It established the instrumentation and routing-control layer used by later FORGE experiments.
