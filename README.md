<!-- mcp-name: io.github.tfcbot/viralquery -->

# ViralQuery for agents

Search a curated library of viral UGC, pull stored analyses, and organize the strongest evidence
into private research collections.

This public repository is the distribution layer for ViralQuery:

- an installable `viralquery` agent skill,
- remote MCP Registry metadata,
- copy-paste client configurations.

The hosted implementation derives MCP tools from the same typed contract as the ViralQuery API,
SDK, and CLI.

## Connect the remote MCP server

Endpoint:

```text
https://viralquery.com/mcp
```

The endpoint rejects missing or invalid keys before MCP initialization. Every stateless request is
revalidated against the ViralQuery account gateway.

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

> Use $viralquery to find strong founder-led UGC patterns for my mobile app. Cite the source
> videos, separate stored evidence from your inference, and save the final shortlist privately.

## What the skill does

- starts broad with curated shelves and filtered search,
- limits expensive pulls to a shortlist,
- cites video IDs and source URLs,
- keeps private collections private,
- requires confirmation before payment, email, key rotation, or deletion,
- blocks accidental operator-only library writes.

## Access

Get a key and compare Starter / Max at [viralquery.com](https://viralquery.com/#pricing).
Read the [MCP setup guide](https://viralquery.com/docs/mcp/install) and
[API docs](https://viralquery.com/docs).

## Repository boundary

This repository contains public metadata and workflows only. The production MCP server and API are
hosted by ViralQuery; no implementation secrets or customer data live here.
