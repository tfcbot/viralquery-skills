---
name: viralquery
description: Retrieve organic viral videos for a mobile app with ViralQuery's protected, read-only MCP. Use when an agent needs to discover which mobile apps are available, select a stable app ID, get that app's video collection, or answer a request such as "get the viral videos for Cal AI."
---

# ViralQuery

Use ViralQuery to answer: “Get the viral videos ViralQuery has for this mobile app.”

## Read-only workflow

1. Use the ViralQuery MCP tools. If unavailable, tell the user how to connect
   `https://viralquery.com/mcp`; never ask them to paste a key into chat.
2. Call `listApps` and match the requested name to one returned app. Use its exact `id`; never
   invent an ID or pass the user's text directly to `getAppVideos`.
3. Call `getAppVideos` once with that ID. Filter or sort the returned fields locally only when the
   user's task requires a subset.
4. Cite each returned source URL and video ID. Report only the data that ViralQuery
   returns; clearly label any synthesis as your inference.
5. If the app is not listed, say ViralQuery does not currently have it in the public app library.
   Do not conclude that no organic viral videos exist elsewhere.
6. Return a focused answer for the requested app rather than broad, unrelated video inspiration.

The MCP exposes only `listApps` and `getAppVideos`. Do not look for write or maintenance tools.

Read [`references/operations.md`](references/operations.md) when exact tool inputs or protected
connection setup matter.
