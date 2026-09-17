# KESPA-NOTE-016 — Telemetry-Backed User Profiles, Community Scoring, and Privacy Controls

**Date:** 2026-09-15  
**Status:** Verified — implementation and functional validation complete  
**Project:** KESPA AI / NexLabs Studios

## Purpose

KESPA added a complete user-profile and community analytics layer without creating a second telemetry system.

The feature derives its statistics from existing application data:

`users + chats + messages + forge_request_metrics -> UserStats -> profile / leaderboard / public profile`

That keeps product analytics tied to the same persisted runtime measurements already used elsewhere in KESPA.

## Observed tracked history

At implementation time, the recorded telemetry included:

- telemetry requests: **120**
- tracked chats: **21**
- tracked user messages: **120**
- tracked KESPA responses: **119**
- input tokens processed: **278,526**
- output tokens generated: **24,657**
- total model tokens: **303,183**

Telemetry history begins approximately **September 2, 2026**.

Because telemetry retention and retained chat/message history do not cover exactly the same period, the UI deliberately uses terms such as:

- `Tracked chats`
- `Tracked requests`
- `Tracked since`

rather than claiming absolute lifetime totals.

Benchmark-tagged telemetry is excluded from product-facing profile and leaderboard statistics.

## User profile

The authenticated `/profile` page exposes safe user-facing aggregates such as:

- account identity and plan;
- usage and token totals;
- response latency / TTFT / tokens-per-second;
- RAG, web, memory, review, cache, model, and reasoning-mode usage;
- estimated active time;
- streaks;
- milestones;
- 182-day activity heatmap.

Token terminology was deliberately written to avoid misleading users. For example:

`Input tokens processed`

is used instead of implying all prompt tokens represent words manually typed by the user.

## Estimated active time

Requests are sorted chronologically.

A gap of **5 minutes or less** is treated as the same active session.

Long idle periods are capped rather than being counted as active use.

The metric is therefore labeled:

`Estimated active time with KESPA`

rather than exact usage time.

## Community leaderboard

The authenticated `/leaderboard` supports:

- overall / KESPA Score;
- total tokens;
- chats;
- messages;
- estimated active time;
- current streak;
- longest streak;
- approximate generated words.

Periods:

- all time;
- this month;
- this week.

No prompts or conversation content are exposed.

## KESPA Score v2

The original score used community-relative normalization, which produced a bad edge case when only one active user existed.

V2 replaced that with fixed-target logarithmic scaling.

Weights:

- **35%** tokens
- **20%** messages
- **15%** chats
- **20%** estimated active time
- **10%** current streak

Different targets are used for all-time, monthly, and weekly scoring.

That makes the score usable even when the community is still small.

## Privacy controls

Leaderboard participation and public-profile sharing are separate settings in the existing `users.settings` JSON.

Defaults:

- leaderboard visibility: **enabled**
- public profile sharing: **disabled**

Public profile URL format:

`/u/<username>`

When public sharing is disabled, leaderboard avatars/usernames remain non-clickable.

## Public-data boundary

Public profiles may expose safe aggregate information.

They do **not** expose:

- prompts;
- KESPA answers;
- chat titles;
- emails;
- IP addresses;
- private memories;
- retrieved documents;
- web URLs;
- request IDs;
- raw telemetry JSON;
- private diagnostics;
- conversation contents.

## Architecture boundary

This feature required:

- **no `brain_api.py` changes**
- **no NexLedger changes**
- **no new statistics database table**
- **no second telemetry pipeline**

User/community statistics intentionally remain an application feature rather than externally attestable ledger evidence.

## Validation

Functional validation confirmed:

- `/profile` loads and scrolls;
- `/leaderboard` loads;
- ranking categories and periods work;
- privacy toggles remove/re-add leaderboard users;
- public profile sharing can be enabled/disabled;
- `/u/<username>` resolves;
- leaderboard identities link only when public sharing is enabled;
- the activity heatmap follows real weekday alignment.

The primary PHP implementation files were also linted successfully.

## Scalability note

Live aggregation is appropriate at current scale.

If KESPA grows substantially, the same public interface can later be backed by cached/materialized user statistics without changing the product contract.
