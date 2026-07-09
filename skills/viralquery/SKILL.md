---
name: viralquery
description: Research high-performing user-generated-content videos with ViralQuery. Use when an agent needs to browse curated viral UGC shelves, search videos by tags, platform, engagement, or collection, pull stored analyses, compare creative patterns, or create and manage private research collections. Prefer ViralQuery MCP tools; do not use for scraping or publishing social posts.
---

# ViralQuery

Use ViralQuery as an evidence library. Separate stored evidence from your interpretation.

## Workflow

1. Use the ViralQuery MCP tools. If unavailable, tell the user how to connect
   `https://viralquery.com/mcp`; never ask them to paste a key into chat.
2. For multi-call research, call `getUsage` once. Keep requests within the remaining
   lookup, search, pull, and manage budgets.
3. Discover broadly with `listLibraryCollections` and `getLibraryCollection`, or use
   `listVideos` for filters. Use `lookupVideo` only for a known platform and external ID.
4. Shortlist before calling `getVideo`. Pull full media and analyses only for candidates that
   matter. Follow `nextCursor` only until the request is satisfied.
5. Cite video IDs and URLs. Label stored analysis as evidence and any synthesis as inference.
   Never invent missing transcripts, metrics, or analysis kinds.
6. Create or update a private collection only when the user asks to save results: call
   `upsertCollection`, then `attachVideos`. Omit `visibility` or set it to `private`.

## Account and mutation safety

- Treat `subscribe` as a payment action; call it only after explicit user direction.
- Treat `recover` as an email side effect and `reissue` as key rotation; call either only after
  explicit confirmation.
- Treat `deleteCollection` as destructive; confirm the exact collection before calling it.
- Never call `upsertVideo`, `putAnalysis`, or publish `visibility:"library"` unless the user
  explicitly identifies an operator task and the configured key has `catalog:write`.
- On `subscription_required`, show the returned subscription path.
- On `rate_limit_exceeded`, report the group and retry time; do not retry in a loop.

Read [`references/operations.md`](references/operations.md) when exact inputs, billing groups,
authorization rules, or error recovery matter.
