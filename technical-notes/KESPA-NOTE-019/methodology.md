# Methodology

## Publication contract

Research records are added to the public repository through the root manifest and an entry-specific artifact directory.

Each entry declares its type, status, summary, path, tags, and public files.

## Website synchronization

The website sync resolves the repository's current `main` branch to an immutable commit SHA.

The manifest and all referenced artifacts are then fetched from that same revision.

Successful sync state records the resolved commit SHA.

## Local cache

Public research artifacts are cached under the website's `storage/public_research` area so the public page does not need to fetch GitHub on every page request.

## Artifact safety

The viewer supports only the public text-oriented artifact formats used by the repository and safely escapes structured/text content.

## Publication boundary

Private application code, environment values, raw evidence bodies, and private internal artifacts remain outside the public repository.
