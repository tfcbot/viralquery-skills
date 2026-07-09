# ViralQuery agent reference

ViralQuery is a protected remote MCP server for finding the top organic viral videos of mobile
apps. Its app coverage is growing.

## Connect safely

Use `https://viralquery.com/mcp` with the full header
`Authorization: Bearer sk_viralquery_...`. A valid key is required before MCP initialization and
on each request. Never put a key in a URL, prompt, source file, or commit.

## Find an app's top videos

Start with `listLibraryCollections` to find the app's exact name, slug, and ID in ViralQuery's
growing index. Then use `getLibraryCollection` with that ID to retrieve its videos.

Use `listVideos` with the app tag only when the user asks for a narrower search. For example,
rank the matching videos by engagement:

```json
{
  "tags": "duolingo",
  "sort": "engagement",
  "limit": 20
}
```

The result contains matching videos and a `nextCursor` when more results are available. Pull
`getVideo` for only the shortlisted IDs when additional detail is useful. Cite source URLs and
identifiers in the final answer.

If no videos match, say that the app may not be covered yet. Do not infer that no organic viral
videos exist; ViralQuery's catalog is expanding.

## Account and error handling

- Require explicit confirmation before any payment, account-recovery email, key rotation, or
  deletion action.
- For `401 unauthorized`, ask the user to configure their key outside chat; never request it.
- For `402 subscription_required`, show the returned subscription path and ask before checkout.
- For `429 rate_limit_exceeded`, report the retry time and stop instead of retrying in a loop.
