# ViralQuery operation reference

The remote MCP endpoint is `https://viralquery.com/mcp`. Send the subscriber key as the full
`Authorization: Bearer sk_viralquery_...` header. Never put a key in a URL or prompt.

## Public account tools

The HTTP API exposes these without a key. The hosted MCP endpoint itself still requires a valid
key before initialization, so use the web/API flow for initial subscription and key recovery.

| Tool | Input | Purpose / side effect |
|---|---|---|
| `getHealth` | `{}` | Report API and storage health. |
| `getPricing` | `{}` | Return Starter and Max labels and monthly prices. |
| `subscribe` | `{ tier: "starter" \| "max" }` | Start Stripe checkout. Payment action; require explicit direction. |
| `claimSubscription` | `{ claimToken: string }` | Poll a checkout claim and return a key once. |
| `recover` | `{ email: string }` | Email a verification code. Side effect; require confirmation. |
| `reissue` | `{ email: string, code: string }` | Rotate the API key. Destructive to the old key; require confirmation. |

## Keyed account tools

These require a valid key but do not consume a daily research group.

| Tool | Input | Output |
|---|---|---|
| `getUsage` | `{}` | Tier, subscription state, reset time, and remaining group budgets. |
| `listEvents` | `{ limit?: number }` | Recent operation events for the calling key. |

## Subscriber research tools

An active subscription is required. Limits reset at midnight UTC and are counted per request.

| Group | Tool | Input |
|---|---|---|
| lookup | `lookupVideo` | `{ platform: string, externalId: string }` |
| search | `listVideos` | `{ collection?: string, tags?: string, platform?: string, minEngagement?: number, sort?: "engagement" \| "posted" \| "recent", limit?: 1..200, cursor?: string }` |
| search | `listCollections` | `{ kind?: string, limit?: 1..200 }` |
| search | `listLibraryCollections` | `{ limit?: 1..200 }` |
| pull | `getVideo` | `{ id: string, kind?: string }` |
| pull | `listCollectionVideos` | `{ id: string }` |
| pull | `getLibraryCollection` | `{ id: string }` |
| manage | `upsertCollection` | `{ slug: string, name?: string, visibility?: "library" \| "private", kind?: string, status?: string, tags?: string[], metadata?: object }` |
| manage | `attachVideos` | `{ collectionId: string, videoIds: string[1+], note?: string }` |
| manage | `deleteCollection` | `{ id: string }` |

Keep subscriber collections private. `visibility:"library"` requires operator scope.

## Operator-only tools

The fail-closed `catalog:write` scope is required.

- `upsertVideo` — `{ platform, externalId, url, mp4Url?, tags?, engagementRate?, postedAt?,
  metadata?, collectionSlug? }`. Idempotent by platform and external ID.
- `putAnalysis` — `{ videoId, kind, result, producedBy?, schemaVersion?, force? }`. Idempotent per
  video and analysis kind unless `force` creates a new version.

Do not attempt operator tools with a normal subscriber key.

## Error recovery

- `401 unauthorized`: the bearer header is missing or invalid. Ask the user to configure it
  outside chat; do not request the secret.
- `402 subscription_required`: show `subscribeUrl` and ask before calling `subscribe`.
- `403 forbidden`: report `requiredScope` and `grantedScopes`. Do not work around scope policy.
- `429 rate_limit_exceeded`: report `group`, `limit`, and `retryAfter`. Stop the loop.
- `502 upstream_error`: a retry is safe when `retryable` is true, but use bounded backoff.
