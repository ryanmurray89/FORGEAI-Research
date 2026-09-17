# Methodology

## Build

A new isolated Chroma database was constructed from the frozen 423-claim clean verified corpus.

The build was validated by comparing expected claim count to indexed card count.

## Smoke retrieval

A known verified claim was queried against the isolated clean collection. The test checked:

- rank position;
- similarity score;
- verified metadata;
- supported verdict metadata;
- expected content terms;
- absence of write operations.

## Cutover

After the isolated build and retrieval smoke passed, the clean index replaced the legacy production
knowledge collection.

Memory collections were handled separately from the retired legacy `forge_cards` corpus so that user/chat
memory preservation did not reintroduce legacy knowledge cards.

## Source-of-truth rule

The production architecture treats `trusted_knowledge` in MySQL as authoritative and Chroma as a
rebuildable semantic retrieval index.

This separation allows index regeneration without redefining what knowledge is trusted.
