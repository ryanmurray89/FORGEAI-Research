# Methodology

## Existing-data reuse

The profile/leaderboard service aggregates existing `users`, `chats`, `messages`, and `forge_request_metrics` data rather than introducing a second analytics pipeline.

Benchmark-tagged telemetry is excluded from user/community product statistics.

## Activity estimation

Request timestamps are ordered chronologically.

Gaps of five minutes or less are treated as the same active session; longer gaps begin a new session and idle time is capped.

## Score construction

FORGE Score v2 uses fixed-target log scaling rather than community-relative normalization.

Weights are 35% tokens, 20% messages, 15% chats, 20% estimated active time, and 10% current streak.

Separate target sets apply to weekly, monthly, and all-time periods.

## Privacy model

Leaderboard visibility and public-profile visibility are independent settings stored in the existing `users.settings` JSON.

Public profiles render only safe aggregates and never expose prompts, responses, private memories, raw telemetry, request IDs, or conversation contents.

## Validation

The implementation was tested across authenticated profile rendering, leaderboard sorting/periods, privacy toggles, public-profile routing, conditional leaderboard links, activity heatmap rendering, and PHP syntax validation.
