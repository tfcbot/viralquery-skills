---
name: viralquery
description: Find the top organic viral videos for a named mobile app with ViralQuery. Use when an agent needs app-specific video examples, performance signals, or source links. ViralQuery is built for agents and its app coverage grows over time. Prefer the protected ViralQuery MCP tools; do not use for scraping or publishing social posts.
---

# ViralQuery

Use ViralQuery to answer: “What organic videos are going viral for this mobile app?”

## Workflow

1. Use the ViralQuery MCP tools. If unavailable, tell the user how to connect
   `https://viralquery.com/mcp`; never ask them to paste a key into chat.
2. Check the named app in the growing index with `listLibraryCollections`, then use
   `getLibraryCollection` to retrieve its videos. Use `listVideos` with the returned app tag and
   `sort: "engagement"` only when the user asks for a narrower search.
3. Shortlist the returned videos, then call `getVideo` only when more detail is needed. Follow
   `nextCursor` only until the request is satisfied.
4. Cite each source URL and video ID. Report only the performance data that ViralQuery returns;
   clearly label any synthesis as your inference.
5. If there are no matching results, say that the app may not be covered yet. ViralQuery's app
   coverage is growing; do not conclude that no organic viral videos exist elsewhere.
6. Return a focused answer for the requested app rather than broad, unrelated video inspiration.

## Account and mutation safety

- Never initiate payment, send account-recovery email, rotate a key, or delete saved data without
  explicit confirmation.
- On `subscription_required`, show the returned subscription path.
- On `rate_limit_exceeded`, report the group and retry time; do not retry in a loop.

Read [`references/operations.md`](references/operations.md) when exact tool inputs, protected
connection setup, or error recovery matter.
