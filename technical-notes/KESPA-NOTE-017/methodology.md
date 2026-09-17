# Methodology

## Request authentication

The app-side request API authenticates HOME polling requests with HMAC SHA-256 over timestamp, nonce, and request-body identity.

Requests outside the timestamp window or using replayed nonces are rejected.

## Queue durability

HOME persists each research request into a filesystem state machine rather than holding work only in memory.

Explicit queue directories represent pending, active, completed, failed, held, and receipt states.

## Release handoff

Completed trusted-release packages are immutable handoff units.

A periodic scanner detects eligible releases and sends them through the signed HTTPS receiver.

Delivery state prevents unchanged successful packages from being resent indefinitely.

## Application persistence

Accepted releases are written into an application inbox with a receipt and the exact release artifacts required by the isolated app-side lifecycle.

## Resilience principle

Transport failures do not lower trust requirements and do not require successful research to be regenerated.

The system retains durable state and retries delivery instead.
