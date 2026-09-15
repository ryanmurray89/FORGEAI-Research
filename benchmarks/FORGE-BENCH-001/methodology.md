# Methodology

## Corpus

The benchmark used a frozen clean corpus containing:

- 423 verified atomic claims;
- 56 linked evidence excerpts.

The isolated benchmark Chroma collection was validated independently before the benchmark. The source
record states that 423 IDs/documents/metadata were exact and that retrieval equivalence was confirmed
after allowing harmless float-round-trip differences in embeddings.

## Question split

The benchmark question builder created:

- 66 total questions;
- 12 calibration questions;
- 54 locked evaluation questions.

The calibration set was used to freeze retrieval policy without parsing the locked evaluation questions.

## Runtime comparison

The 54 locked questions were executed against each of three arms:

- A — raw local 7B;
- B — clean verified atomic retrieval;
- C — then-current FORGE orchestration / legacy retrieval path.

This produced 162 raw system outputs.

## Blinded quality scoring

A standalone quality scorer preserved the original raw benchmark outputs.

The historical record states that:

- frozen corpus/evaluation hashes were verified;
- 162/162 quality judgments completed;
- system identity was hidden during blinded judging;
- a missing-gold-ID metadata defect was repaired offline from locked reference IDs;
- `raw_results.jsonl` was not modified.

## Production isolation

The benchmark did not modify production Chroma, Brain API behavior, or database state. Private memory,
web/cloud retrieval, and trust callbacks were disabled for the benchmark path described in the source record.
