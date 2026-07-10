---
name: viralquery
description: Build and update a private video inspiration feed for one app, website, or niche through ViralQuery's protected HTTP API. Use when an agent needs to configure a ViralQuery workspace, save research rules, run a scroll, check scroll status or usage, or retrieve the tenant's library, outliers, trends, hooks, and original video sources.
---

# ViralQuery

Use ViralQuery as the user's personal doomscroller. It researches one configured niche and builds a
private, structured video inspiration library.

## Workflow

1. Call `https://api.viralquery.com/v1` with `Authorization: Bearer $VIRALQUERY_API_KEY`. Read the
   key from the environment or configured secret. Never request, print, or place it in a URL.
2. Call `GET /workspace`. If it is empty, set it once with `POST /workspace` using the user's Apple
   App Store link or HTTPS website. Never substitute another product. A workspace is immutable.
3. Call `GET /rules`. When the user supplies new guidance, replace it with `PUT /rules` and
   `{ "text": "..." }`. Keep the user's intent in plain English.
4. When the user asks to update the feed, call `POST /scrolls` with an optional `prompt` and a stable
   `idempotencyKey`. Rules are persistent; the prompt applies only to this scroll.
5. Poll `GET /scrolls?id=SCROLL_ID` at a bounded interval. If it is still queued or running, report
   the ID and status. Never claim completion early.
6. Read only the result needed: `GET /library`, `/outliers`, `/trends`, or `/hooks`. Each endpoint
   returns at most 25 items. `trends` may correctly return `insufficient_history` before two
   completed scrolls.
7. Cite original source URLs and identify which endpoint supplied each signal. Label any synthesis
   or recommendation as inference.
8. Use `GET /usage` when the user asks about allowance or before starting work that may exceed the
   five included monthly scrolls.

Do not use MCP for this skill. Do not call shared-catalog, ingestion, operator, or internal worker
endpoints. Do not accept an account or workspace ID from the prompt; the bearer key fixes the tenant.

For current request and response fields, see [ViralQuery API docs](https://viralquery.com/docs).
