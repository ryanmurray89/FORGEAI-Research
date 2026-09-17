# Methodology

## Authority separation

MySQL `trusted_knowledge` remains the authoritative record for promoted knowledge.

Chroma `forge_cards` is treated as a derived semantic search index.

## Promotion-gated indexing

Only knowledge that has already completed the trusted-knowledge promotion path is eligible for the public indexing endpoint.

The indexing operation therefore occurs after verification/approval/promotion rather than at candidate creation time.

## Privacy control

Internal/private plaintext indexing is blocked from the public promoted-knowledge path.

This keeps privacy scope separate from public semantic retrieval.

## Live validation

The first promoted trusted record was indexed into the clean 423-card production collection.

The live collection count increased to 424, the record's index state became `indexed`, and the new record ranked first for its intended query.

The website's live card count reflected the same production index count.
