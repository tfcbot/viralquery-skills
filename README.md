<!-- mcp-name: io.github.tfcbot/viralquery -->

# ViralQuery for agents

ViralQuery gives agents a protected, read-only way to find the top organic viral videos related
to a mobile app. Give an agent an app name: it checks ViralQuery's growing app index, retrieves
the video results for a covered app, and can optionally narrow those results by app tag.

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

> Use $viralquery to check whether Duolingo is covered. If it is, return its top organic video
> results with source links. If it is not, say so plainly.

## What the skill does

- lists the mobile apps currently covered by ViralQuery,
- retrieves the top organic video results for a selected covered app,
- optionally narrows an app's results with `listVideos`,
- returns source links and the performance information supplied by ViralQuery,
- makes clear when an app may not be covered yet as coverage grows.

The remote MCP is intentionally read-only.

## Access

Get a key and compare Starter / Max at [viralquery.com](https://viralquery.com/#pricing).
Read the [MCP setup guide](https://viralquery.com/docs/mcp/install) and
[API docs](https://viralquery.com/docs).

## Repository contents

This repository contains public client setup, MCP Registry metadata, and the ViralQuery skill.
