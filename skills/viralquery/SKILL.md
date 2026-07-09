---
name: viralquery
description: Research the top organic viral videos for a named mobile app with ViralQuery's protected, read-only MCP. Use when an agent needs to list covered apps, retrieve the video results for one app, or optionally narrow an app's results. ViralQuery is built for agents and its app coverage grows over time.
---

# ViralQuery

Use ViralQuery to answer: “What organic videos are going viral for this mobile app?”

## Read-only workflow

1. Use the ViralQuery MCP tools. If unavailable, tell the user how to connect
   `https://viralquery.com/mcp`; never ask them to paste a key into chat.
2. Check the named app in the growing index with `listLibraryCollections`, then use
   `getLibraryCollection` with the selected app ID to retrieve its top video results.
3. Call `listVideos` only when the user asks for a narrower view. Use the app tag returned by the
   index and only the filters needed for that request.
4. Cite each returned source URL and video ID. Report only the performance data that ViralQuery
   returns; clearly label any synthesis as your inference.
5. If the app is not in the index or has no matching results, say that it may not be covered yet.
   ViralQuery's app coverage is growing; do not conclude that no organic viral videos exist
   elsewhere.
6. Return a focused answer for the requested app rather than broad, unrelated video inspiration.

The MCP is read-only. Do not propose actions outside the three research tools.

Read [`references/operations.md`](references/operations.md) when exact tool inputs or protected
connection setup matter.
