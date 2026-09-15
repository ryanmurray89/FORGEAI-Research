# FORGE-NOTE-019 — Public Research Archive and Immutable Revision Sync

**Date:** 2026-09-15  
**Status:** Verified — public repository / website bridge operational  
**Project:** FORGE AI / NexLabs

## Purpose

FORGE's research results are kept separate from the private application repository.

The public archive lives in:

`ryanmurray89/FORGEAI-Research`

and publishes curated research records through a manifest-driven structure.

Supported public entry types include:

- experiments;
- benchmarks;
- technical notes;
- datasets;
- updates.

The public archive is not intended to expose private application code or raw internal research state.

## Public manifest

The root index uses:

`forge.public_research_index.v1`

Each entry identifies:

- research ID;
- type;
- title;
- date;
- publication status;
- summary;
- path;
- tags;
- public files.

Allowed status values are:

`draft / published / verified / archived`

The public artifact layer is intentionally limited to text-oriented formats such as Markdown, JSON, text, and CSV.

## Website bridge

The FORGE website periodically synchronizes the public repository into a local public-research cache.

Core pieces include:

- `scripts/research/sync_public_research.php`
- `src/PublicResearch.php`
- `public/research/index.php`
- `public/research/view.php`

Local state includes:

- cached manifest;
- sync state;
- per-entry artifact directories.

The sync runs every **5 minutes**.

## Artifact viewer

The public artifact viewer renders a restricted Markdown subset and safely escapes JSON/text content.

It can expose:

- SHA-256;
- byte size;
- artifact type;
- GitHub source link.

This makes the public research page useful for both humans and audit/reproducibility work without turning it into a generic arbitrary-file renderer.

## Mutable-branch synchronization problem

During publication of the early benchmark records, an important failure mode appeared.

The GitHub API showed the current `main` branch containing the new benchmark entry, while:

`raw.githubusercontent.com/.../main/manifest.json`

continued returning an older branch snapshot.

That meant a branch-name URL could temporarily serve stale content even though the repository itself had already advanced.

For a research archive, that can produce a worse problem than a missing page:

`new manifest + old artifact`

or:

`old manifest + new repository state`

## Immutable revision fix

Sync v0.2.3 changed the process.

Instead of fetching everything directly through the mutable `main` reference, FORGE now:

1. resolves `main` to its current commit SHA through the GitHub API;
2. fetches `manifest.json` from that exact SHA;
3. fetches every referenced artifact from the same SHA;
4. stores the resolved `commit_sha` in sync state.

Conceptually:

`main -> commit SHA -> manifest + all artifacts from that exact revision`

This removes branch-CDN freshness from the consistency contract.

## Why this matters

Research publication needs stronger consistency than an ordinary marketing website.

If the manifest says an experiment contains six artifacts, the website should not accidentally combine a manifest from one revision with files from another.

Using one immutable repository revision per sync gives FORGE a simple consistency guarantee:

> A synchronized public research snapshot is internally revision-consistent.

## Public/private boundary

The public archive intentionally excludes:

- private application repository contents;
- credentials and environment files;
- raw third-party evidence bodies;
- private internal telemetry payloads;
- implementation secrets.

It publishes safe research summaries, methodology, aggregate measurements, recorded provenance, and artifact hashes.

## Research significance

This archive turns individual experiments into a growing longitudinal research record.

It gives FORGE a public surface where benchmark failures, methodology changes, technical notes, and successful experiments can coexist without rewriting history.

That matters especially for the FORGE research thesis because negative results and architecture corrections remain visible alongside successful ones.

## Limitation

The archive is curated.

It is not a complete mirror of every private research artifact, and the public sync does not independently rerun experiments.

Its job is publication consistency and provenance, not experimental validation.
