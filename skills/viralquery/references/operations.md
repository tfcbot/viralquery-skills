# ViralQuery app API

Base URL: `https://api.viralquery.com/v1`.

Send `Authorization: Bearer $VIRALQUERY_API_KEY` on every request. Read the key from a configured
secret or environment variable. Never put it in a URL, prompt, source file, or commit.

| Purpose | Request |
| --- | --- |
| List supported apps | `GET /apps?limit=200` |
| Get one app's videos | `GET /apps/videos?id=APP_ID` |
| Request a missing App Store app (Max) | `POST /app-requests` with `{ "appStoreUrl": "https://apps.apple.com/.../id123" }` |
| Check a request | `GET /app-requests?id=REQUEST_ID` |

The app request receipt returns `request.id`; use that receipt ID for status checks, not the App
Store ID. A ready response contains the numeric App Store app ID for `/apps/videos`.

`GET /apps/videos` returns `app`, `resultLimit`, `returnedCount`, and `videos`. Starter returns up
to 5; Max returns up to 50. Cite source URLs and identifiers. Filter or sort returned fields locally.

Do not infer that no viral videos exist elsewhere when ViralQuery returns an empty collection.
