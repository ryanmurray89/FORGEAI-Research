# Methodology

## Frozen workload

The raw A/B/C execution used the 54-question locked evaluation set.

All three arms executed the same cases under the same benchmark program.

## Compute observation

The runtime harness recorded per-arm latency and GPU-energy measurements.

Arm C additionally exposed orchestration counters for LLM passes, RAG search/use, planner use, reviewer use, and inference avoidance.

## Isolation

Private memory, external web/cloud retrieval, and trust callbacks were disabled for the locked benchmark.

No production Chroma, Brain, or database writes were performed.

## Interpretation sequence

The raw runtime result was interpreted conservatively before quality judging: latency and energy alone were not treated as proof of superiority.

After blinded quality judging completed, the raw compute profile could be interpreted alongside the separately measured quality scores.

## Derived values

Latency/energy multiples and percentage reductions in this public note are arithmetic derived from the recorded mean values. They are not additional benchmark measurements.
