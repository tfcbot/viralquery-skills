# ViralQuery read-only app research

ViralQuery is a protected remote MCP server for finding the top organic viral videos related to
mobile apps. Its app coverage is growing.

## Connect safely

Use `https://viralquery.com/mcp` with the full header
`Authorization: Bearer sk_viralquery_...`. A valid key is required before MCP initialization and
on each request. Never put a key in a URL, prompt, source file, or commit.

## Use the three research tools

1. Start with `listLibraryCollections` to find the app's exact name, slug, and ID in
   ViralQuery's growing index.
2. Use `getLibraryCollection` with that ID to retrieve the top video results for the covered app.
3. Use `listVideos` only when the user asks to narrow those results. Supply the app tag from the
   index and only the requested filters.

For example, narrow Duolingo's results to the most-engaged videos:

```json
{
  "tags": "duolingo",
  "sort": "engagement",
  "limit": 20
}
```

The result contains matching videos and a `nextCursor` when more results are available. Follow a
cursor only when it is needed to satisfy the request. Cite returned source URLs and identifiers in
the final answer.

If the app is not listed or no videos match, say that it may not be covered yet. Do not infer that
no organic viral videos exist; ViralQuery's coverage is expanding.

## Keep the connection protected

The MCP has only the three research tools above. Configure a key outside chat and never include a
key in a URL, prompt, source file, or commit. If connection fails, tell the user to verify their
local MCP configuration without requesting their key.
