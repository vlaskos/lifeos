# Connect Notion (MCP)

LifeOS skills talk to your Notion through Notion's official MCP server.
Your data stays in your Notion; you approve access in Notion's own window.

## Claude (web, desktop, mobile)

1. Open **Settings → Connectors** and add **Notion**.
2. Approve access in the Notion window. Give access to the workspace where you duplicated LifeOS.
3. In a new chat, check that Claude can see Notion: "Search my Notion for LifeOS".

## Claude Code

Install Notion's official plugin — it adds the Notion MCP server (`https://mcp.notion.com/mcp`) and Notion's skills:

```text
/plugin marketplace add makenotion/claude-code-notion-plugin
/plugin install notion-workspace-plugin@notion-plugin-marketplace
```

Restart Claude Code; on first use it opens a browser window to approve access in Notion.
LifeOS does not add a second Notion server, so there is nothing to configure twice.

## Troubleshooting

- **Claude can't find LifeOS** — the connector may not have access to that page. Re-open the connector settings in Notion and add the LifeOS page.
- **"Upgrade" instead of the Areas wheel** — Notion's free plan allows one chart per workspace. Not an MCP issue.
