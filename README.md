<!-- mcp-name: io.github.tfcbot/viralquery -->

# ViralQuery for agents

ViralQuery helps agents find the top organic viral videos for a mobile app. Give an agent an app
name and it can search ViralQuery's growing app coverage, return the strongest matching videos,
and cite the original sources.

It is built for agents: MCP-first, structured results, and clear source links. It is not limited
to one video style or content format.

This public repository is the distribution layer for ViralQuery:

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

> Use $viralquery to find the top organic viral videos for Duolingo. Return source links and the
> available performance signals. If Duolingo is not covered yet, say so plainly.

## What the skill does

- searches for a named mobile app,
- surfaces its strongest organic viral videos,
- returns source links, identifiers, and available performance information,
- makes clear when an app may not be covered yet as the catalog grows,
- requires confirmation before payment, account recovery, key rotation, or deletion.

## Access

Get a key and compare Starter / Max at [viralquery.com](https://viralquery.com/#pricing).
Read the [MCP setup guide](https://viralquery.com/docs/mcp/install) and
[API docs](https://viralquery.com/docs).

## Repository boundary

This repository contains public metadata and client setup only. The protected production MCP
server and API are hosted by ViralQuery; no implementation secrets or customer data live here.
