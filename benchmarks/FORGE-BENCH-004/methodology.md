# Methodology

## Corpus

An isolated Chroma candidate index contained 30 verified evidence-bound pilot cards.

Embeddings were created from each card's focused `retrieval_text` using `all-MiniLM-L6-v2`, normalized to 384 dimensions with cosine distance.

## Query set

Thirty reviewed queries were used, one targeting each expected pilot card.

The benchmark requested the top five results for each query.

## Retrieval measures

The benchmark recorded exact expected-card rank and expected-topic rank at @1, @3, and @5.

This distinction allowed retrieval of the correct topic but a sibling card to be measured separately from exact-card retrieval.

## Initial contamination gate

Benchmark v001 also scanned top-5 retrievals for contamination.

Its first implementation classified some legitimate cross-topic clean retrievals as contamination, causing a NO-GO despite strong retrieval accuracy.

## Correction

Benchmark v002 separated cross-topic retrieval from hard synthetic contamination and added a whole-candidate hard-contamination scan.

The retrieval corpus itself was not changed by this benchmark correction.

## Production isolation

Both candidate and historical production Chroma were query-only during the benchmark.

No Brain changes or production writes were performed.
