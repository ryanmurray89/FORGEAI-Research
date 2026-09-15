# Methodology

## Corpus under test

The test used the clean 423-claim verified corpus and a Brain-compatible Chroma representation using
`all-MiniLM-L6-v2` embeddings with cosine distance.

## Structural validation

IDs, documents, and metadata were compared across all 423 records.

The validator required exact agreement for those fields.

## Retrieval validation

A fixed retrieval-equivalence sample compared top-1 and top-10 results across the compatible index representations.

All 32 recorded checks matched.

## Embedding comparison

Stored embeddings were compared numerically.

Tiny float-roundtrip differences were permitted only when they remained small and did not alter the tested
retrieval results.

The maximum recorded absolute delta was `1.49011611938e-08`.

## Isolation

The work was performed outside the production Chroma path and did not modify Brain API behavior or production
database state.
