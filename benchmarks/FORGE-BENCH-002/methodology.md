# Methodology

## Experimental design

D v001 was evaluated against the frozen FORGE benchmark workload using the same locked evaluation
cases and quality-evaluation machinery established for the earlier A/B/C benchmark.

The final comparison used:

`Frozen A + frozen B + C-envelope with D answer; C slot = D`

This preserved the existing evaluation contract while substituting D's adaptive response into the
third scoring slot.

## Runtime lock

The historical finalization references a frozen D runtime-result lock and two D execution runs.
The final quality run was `d_v001_20260905T225726Z`.

## Quality evaluation

The blinded judge evaluated 162 one-answer inputs.

The historical record states that judge inputs contained no A/B/C labels, runtime metrics, or system
identity.

## Preregistration

Success was not defined as "quality looks good."

The experiment had explicit thresholds for:

- answer quality;
- retrieval Hit@1;
- gold recall;
- latency;
- energy;
- inference-call count;
- escalation rate;
- quality per second;
- quality per Wh.

The public record preserves the overall primary result as **FAIL** because not all required behavioral
targets were satisfied.

## Production isolation

The benchmark finalization recorded:

- Production Chroma opened: NO
- Production Chroma modified: NO
- Brain modified: NO
- Database modified: NO
- Raw results modified: NO
