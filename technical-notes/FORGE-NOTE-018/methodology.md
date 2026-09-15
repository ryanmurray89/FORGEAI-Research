# Methodology

## Discovery

Multiple public/free discovery channels are queried to produce candidate URLs.

Search result text and snippets are never accepted as evidence.

Seed/citation expansion may discover additional candidate sources from a useful directly fetched page.

## Direct retrieval

Each candidate URL is fetched directly and screened for network safety, redirects, robots restrictions, content type,
response size, useful text, topical relevance, prompt-injection markers, and source-organization identity.

## Independence

Released claims require support from at least two independent source organizations.

Duplicate organizations cannot satisfy the independence requirement merely through multiple hostnames or pages.

## Claim verification

The first structured model call proposes evidence-bound claims.

A second structured model call checks support for those claims against the supplied evidence.

Provider failures trigger bounded retry, wait, reject, or hold behavior; they do not relax release rules.

## Refusal / hold boundary

High-stakes, private, sensitive, and volatile/current categories are not eligible for permanent autonomous learning through this path.

## Release philosophy

If required evidence, structure, support, or safety conditions are unavailable, the worker produces no trusted release.
