# ViralQuery read-only app retrieval

ViralQuery is a protected remote MCP server for retrieving organic viral videos collected for
mobile apps.

## Connect safely

Use `https://viralquery.com/mcp` with the full header
`Authorization: Bearer sk_viralquery_...`. A valid key is required before MCP initialization and
on each request. Never put a key in a URL, prompt, source file, or commit.

## Use the two app tools

1. Call `listApps` with optional `limit` and `cursor` to find the app's exact name and stable ID.
2. Call `getAppVideos` with `{ "id": "APP_ID" }` to retrieve that app's video collection.

Example:

```json
{
  "id": "APP_ID"
}
```

The result contains the selected `app` and its `videos`. Each video may include platform, caption,
hashtags, source timestamps, and metrics. Filter or sort those fields locally. Cite returned source
URLs and identifiers in the final answer.

If the app is not listed or its collection is empty, state what ViralQuery returned. Do not infer
that no organic viral videos exist elsewhere.

## Keep the connection protected

The MCP has only the two read-only tools above. Configure a key outside chat and never include a
key in a URL, prompt, source file, or commit. If connection fails, tell the user to verify their
local MCP configuration without requesting their key.
