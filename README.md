# FORGEAI Research

Public research artifacts for **FORGE AI** by NexLabs.

This repository is intentionally separate from the private FORGE application repository.
It is for public experiments, benchmarks, technical notes, selected datasets, progress updates,
and provenance records.

## Repository layout

- `manifest.json` — machine-readable public research index consumed by forge.nexlabs.studio
- `experiments/` — controlled experiment reports and artifacts
- `benchmarks/` — benchmark results and reproducibility material
- `technical-notes/` — architecture/research notes intended for public release
- `datasets/` — selected public datasets or derived benchmark data
- `updates/` — dated FORGE research/project updates
- `provenance/` — hashes, release metadata, and public attestation references

## Publication boundary

Do not publish:

- production source code
- environment files or secrets
- customer/user data
- private prompts or internal-only configuration
- private telemetry
- credentials, API keys, tokens, or webhooks
- proprietary implementation details that are not intentionally being released

Published results should be scoped to the hardware, models, datasets, policies, and experiment
configuration actually used. A result from one experiment is not a general performance claim.

## Website

Public research is presented at:

https://forge.nexlabs.studio/research/

The website will consume `manifest.json` and selected entry manifests from this repository.
