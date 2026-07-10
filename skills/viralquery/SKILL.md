---
name: viralquery
description: Find the top viral videos for a mobile app through ViralQuery's protected HTTP API. Use when an agent receives an Apple App Store link or app name and needs to list supported apps, retrieve the app's videos, request a missing app on Max, check request status, or answer prompts such as "get the viral videos for this app."
---

# ViralQuery

Use ViralQuery to answer: “Get the top viral videos for this mobile app.”

## Workflow

1. Call the protected API at `https://api.viralquery.com/v1` with `Authorization: Bearer $VIRALQUERY_API_KEY`.
   Read the key from the environment or the caller's configured secret; never request or print it in chat.
2. Prefer an Apple App Store link. Extract its numeric ID, call `GET /apps`, and use an exact matching
   `id` or `appStoreUrl`. For a name-only request, use an unambiguous listed match; never invent an ID.
3. If listed, call `GET /apps/videos?id=APP_ID` once with that exact ID.
4. If missing and the user supplied an App Store link, call `POST /app-requests` with the full link in JSON.
   This is Max-only and uses the account's bounded new-app allowance.
5. For `queued` or `joined`, call `GET /app-requests?id=REQUEST_ID` with the returned request ID. Poll at a bounded
   interval while practical. When `ready`, call `getAppVideos` with the returned app ID. If work is
   still running, report the status and request ID instead of claiming completion.
6. Cite each returned source URL and video ID. Report only the data that ViralQuery
   returns; clearly label any synthesis as your inference.
7. Filter or sort returned fields locally when needed. Return a focused answer for the requested
   app rather than broad, unrelated inspiration.

Do not use a remote tool transport for this skill. Do not call catalog writes, ingestion controls, or maintenance endpoints.

Read [`references/operations.md`](references/operations.md) when exact HTTP requests or response fields matter.
