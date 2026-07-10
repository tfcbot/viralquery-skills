# ViralQuery app retrieval

ViralQuery is a protected remote MCP server for retrieving the top viral videos for mobile apps.

## Connect safely

Use `https://viralquery.com/mcp` with the full header
`Authorization: Bearer sk_viralquery_...`. A valid key is required before MCP initialization and
on each request. Never put a key in a URL, prompt, source file, or commit.

## Use the four app tools

1. Call `listApps` with optional `limit` and `cursor` to find exact IDs and App Store URLs.
2. Call `getAppVideos` with `{ "id": "APP_ID" }` for an available app.
3. If an App Store URL is missing, call `requestApp` with `{ "appStoreUrl": "..." }`. This tool is
   Max-only, quota-limited, and idempotent for the same account and app.
4. Call `getAppRequest` with `{ "id": "REQUEST_ID" }`. When `status` is `ready`, call
   `getAppVideos` with the returned app ID.

Example:

```json
{
  "id": "APP_ID"
}
```

`getAppVideos` returns the selected `app`, `resultLimit`, `returnedCount`, and `videos`. Starter
returns up to 5; Max returns up to 50. Each video may include platform, caption, hashtags, source
timestamps, and metrics. Filter or sort those fields locally. Cite source URLs and identifiers.

If a request remains in progress, state its status and request ID. If a collection is empty, state
what ViralQuery returned. Do not infer that no viral videos exist elsewhere.

## Keep the connection protected

The MCP has only the four bounded app tools above. It has no catalog or ingestion controls.
Configure a key outside chat and never include it in a URL, prompt, source file, or commit. If the
connection fails, ask the user to verify local MCP configuration without requesting the key.
