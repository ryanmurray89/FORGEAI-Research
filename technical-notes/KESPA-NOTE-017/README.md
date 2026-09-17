# KESPA-NOTE-017 — Signed Cross-Host Research Queue and Durable Handoff Architecture

**Date:** 2026-09-15  
**Status:** Verified — live distributed research transport operational  
**Project:** KESPA AI / NexLabs Studios

## Purpose

KESPA's autonomous research system runs across multiple machines.

Rather than exposing the HOME research server directly to the public Internet, the system uses a pull-based
control flow:

`HOME -> HTTPS -> app-nexlabs`

That keeps the public application server as the control-plane boundary while allowing the research server to
retrieve work and return completed releases securely.

## Logical host roles

Current roles are already separated:

- **app-nexlabs** — application / control plane
- **DESKTOP-S16TRCC** — HOME research plane
- **RYANDESKTOP** — inference / retrieval plane

The HOME server does not need a public inbound research endpoint.

## App-to-HOME work queue

The application exposes a research-request API supporting:

- `ping`
- `poll`
- `ack`

Requests are authenticated with **HMAC SHA-256**.

The authentication contract includes:

- timestamp;
- nonce;
- request-body hash;
- signature.

The accepted timestamp window is **five minutes**, and nonce state is retained to prevent replay.

## Durable HOME queue

The HOME poller runs every **5 minutes** and stores incoming work in a filesystem queue:

```text
pending/
processing/
done/
failed/
held/
receipts/
```

This is deliberately durable.

If the HOME machine reboots, pending research does not disappear merely because an in-memory worker stopped.

## Completed release handoff

Successful research produces a frozen release package under:

`D:\forge\research\trusted-release\<release_id>\`

A separate scanner runs every **5 minutes**.

It maintains delivery state under:

`D:\forge\research\handoff_state\`

and skips unchanged packages that were already delivered successfully.

The package is then sent over signed HTTPS to the application-side receiver.

A successful live handoff returned:

`Remote status: received`

`PASS`

## Application inbox

Accepted releases are stored under:

`/var/www/forge/storage/groq_research/inbox/<release_id>/`

Each accepted release contains:

- `handoff_receipt.json`
- `manifest.json`
- `verified_claims.jsonl`
- `verified_evidence.jsonl`

The app-side lifecycle can then process that frozen release independently of the HOME worker.

## Failure behavior

The transport follows a useful durability rule:

- polling failure -> request remains queued;
- HOME reboot -> filesystem queue survives;
- research failure -> request can move to `failed` or `held`;
- handoff failure -> trusted release remains local for retry;
- duplicate scan -> already delivered unchanged package is skipped.

Failure therefore does not require regenerating a successful research release.

## Why this architecture matters

The design separates three different concerns:

`control plane`

`research plane`

`inference / retrieval plane`

That separation reduces coupling and makes later hardware migration easier.

Moving the research worker from a home PC into rack hardware should mostly mean moving the worker/state and changing
endpoints or service scheduling — not redesigning the research protocol.

## Scaling boundary

The current file-backed queues are intentionally simple.

They are appropriate at present scale.

If research volume eventually reaches hundreds or thousands of jobs per hour, the same lifecycle can move to database
leasing, Redis, RabbitMQ, or another broker without changing the research trust model.

There is no reason to add that complexity before the workload requires it.
