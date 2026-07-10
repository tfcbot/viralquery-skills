<!-- mcp-name: io.github.tfcbot/viralquery -->

# ViralQuery for agents

ViralQuery gives agents a protected way to retrieve the top viral videos for mobile apps. Give an
agent an Apple App Store link: it finds the exact app, requests it on Max if needed, and retrieves
the video collection ViralQuery has for that app.

It is built for agents: a small MCP workflow, structured results, and clear source links. It is
not limited to one video style or content format.

This repository includes:

- an installable `viralquery` agent skill,
- remote MCP Registry metadata,
- copy-paste client configurations.

## Connect the remote MCP server

Endpoint:

```text
https://viralquery.com/mcp
```

A valid ViralQuery API key is required before an MCP session can start. The endpoint rejects
missing or invalid keys and revalidates each request.

Set your subscriber key locally:

```bash
export VIRALQUERY_API_KEY=sk_viralquery_...
```

Then add the server to Claude Code:

```bash
claude mcp add --transport http --scope user viralquery https://viralquery.com/mcp \
  --header "Authorization: Bearer ${VIRALQUERY_API_KEY}"
```

See [`examples/claude-code.json`](examples/claude-code.json) and
[`examples/cursor.json`](examples/cursor.json) for project configuration.

Never paste a live key into chat, commit it, or put it in an MCP URL.

## Install the skill

```bash
npx skills add tfcbot/viralquery-agent --skill viralquery -g
```

Then ask:

> Use $viralquery to get the top viral videos for this App Store link and include the source links.

## What the skill does

- calls `listApps` to discover valid app IDs and App Store URLs,
- calls `getAppVideos` for an available app,
- calls `requestApp` on Max when an App Store link is missing,
- calls `getAppRequest` until the app is ready,
- filters or sorts returned fields locally when needed,
- returns source links and the post information supplied by ViralQuery,
- reports a clear status when a new app is still being prepared.

The remote MCP exposes only those four bounded app tools. It exposes no catalog write, ingestion,
or maintenance controls.

## Access

Get a key and compare Starter / Max at [viralquery.com](https://viralquery.com/#pricing).
Read the [MCP setup guide](https://viralquery.com/docs/mcp/install) and
[API docs](https://viralquery.com/docs).

## Repository contents

This repository contains public client setup, MCP Registry metadata, and the ViralQuery skill.
