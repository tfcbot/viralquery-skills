<!-- mcp-name: io.github.tfcbot/viralquery -->

# ViralQuery for agents

ViralQuery is a private video inspiration feed for one app, website, or niche. An agent saves simple
research rules, runs bounded scrolls, and reads structured library, outlier, trend, and hook data.

## Install the skill

```bash
npx skills add https://viralquery.com/skills
```

Then ask:

> Use $viralquery to set my app as the workspace, look for organic demos with strong visual hooks,
> and run my first scroll.

The skill uses the protected ViralQuery HTTP API directly. It does not require MCP.

## Optional remote MCP

Agents that support remote MCP can connect to `https://viralquery.com/mcp` with a ViralQuery API
key in the bearer header. The MCP server exposes the same tenant workspace, rules, scroll, and
bounded result workflow.

```bash
claude mcp add --transport http --scope user viralquery https://viralquery.com/mcp \
  --header "Authorization: Bearer ${VIRALQUERY_API_KEY}"
```

Never paste a live key into chat, commit it, or put it in an MCP URL.

## Public tools

- `getWorkspace` / `setWorkspace`
- `getRules` / `putRules`
- `createScroll` / `getScroll`
- `getLibrary` / `getOutliers` / `getTrends` / `getHooks`

Get a key at [viralquery.com](https://viralquery.com/#pricing). Read the
[quickstart](https://viralquery.com/docs/quickstart), [MCP guide](https://viralquery.com/docs/mcp/install),
and [API docs](https://viralquery.com/docs).
