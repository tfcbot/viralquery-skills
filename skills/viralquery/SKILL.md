---
name: viralquery
description: Build and update a private video inspiration feed for one app, website, or niche through ViralQuery's protected HTTP API. Use when an agent needs to configure a research brief, save rules, run a bounded scroll, check status or usage, or retrieve tenant-scoped video signals.
---

# ViralQuery

Use ViralQuery as the user's personal research feed. It researches one configured niche and keeps a
private, structured video library for that tenant. This is not a public catalog search: the bearer
key fixes the tenant and the workspace is the scope for every read and scroll.

**Canonical API reference:** read [ViralQuery's LLM documentation](https://viralquery.com/llms.txt)
before making an exact request. It is the source of truth for current paths, fields, limits, errors,
and available operations. Do not duplicate undocumented fields from memory.

## Workflow

1. Read the canonical API reference above, then call `https://api.viralquery.com/v1` with `Authorization: Bearer $VIRALQUERY_API_KEY`. Read the
   key from the environment or configured secret. Never request, print, or place it in a URL.
2. Call `GET /workspace`. If it is empty, set the user's research brief with `POST /workspace`,
   using the exact app, website, niche, and competitor information the user provided. Never
   substitute another product.
3. When the user changes the brief, update it with the current workspace operation documented in
   the API reference. Keep the brief about the user's niche, product, and named competitors.
4. Read and update the tenant's persistent rules using the documented rules operations.
5. When the user asks to update the feed, start one documented scroll with the user's prompt and
   any supported scheduling or idempotency fields. Do not start another scroll while one is queued
   or running.
6. Poll the documented scroll-status operation at a bounded interval. If it is queued or running, report the
   ID and status. Never claim completion early.
7. After completion, read only the result table needed for the request (library, outliers, trends,
   hooks, or another operation currently documented). Filter or sort locally only when the API
   response supplies the fields needed. Do not invent ranking semantics.
8. If the user wants to remember a judgment, use the documented tenant-owned annotation operation.
   Never overwrite unrelated keys or another tenant's data.
9. Check the documented usage operation when the user asks about allowance or before starting work
   that may exceed the remaining allowance.
10. Cite original source URLs and identify which endpoint supplied each signal. Label any synthesis
    or recommendation as inference. Never invent videos, metrics, creators, or URLs.

## Important states

- A result may explicitly report insufficient history. Report that honestly rather than calling it a
  trend.
- A scroll may be queued, running, completed, failed, or cancelled. Use its documented status,
  progress, and failure fields when explaining a failure.
- A workspace, scroll, or video ID from another bearer key is not visible. Never accept an account
  or workspace selector from the prompt.

Do not use MCP for this skill. Do not call shared-catalog, ingestion, operator, or internal worker
endpoints. The skill calls the protected HTTP API directly. For human-readable guides, see the
[ViralQuery docs](https://viralquery.com/docs).
