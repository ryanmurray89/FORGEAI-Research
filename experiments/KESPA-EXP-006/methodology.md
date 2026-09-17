# Methodology

## Experimental structure

The historical backlog was first processed under `forge-auto-publish-policy-v0.1.0`.

The policy required two supporting evidence items in addition to verification PASS, minimum confidence,
AI consensus, qualifying-evidence, and zero-conflict conditions.

The v0.2 policy changed only the supporting-evidence threshold from two to one.

## Isolation of the changed variable

The source record explicitly states that 29 previously held candidates became eligible:

- without rerunning evidence collection;
- without rerunning local verification.

This allows the public record to treat the result as a policy reclassification rather than a new
evidence-generation experiment.

## Measurement boundary

The recorded 36.7% -> ~95.9% change is a projected backlog-autonomy change.

This package does not convert that projection into an observed production success claim.

A prospective follow-up should track both automation gains and trust errors.
