# Linear MCP Setup Guide

## Claude Code

### Install the Linear MCP server

```bash
claude mcp add linear-server -- npx -y @anthropic-ai/linear-mcp-server
```

### Authenticate

After adding the server, run `/mcp` in Claude Code. You will be prompted to authenticate with Linear via OAuth. Follow the browser flow to grant access.

### Verify

```bash
claude mcp list
```

You should see `linear-server` listed and connected.

---

## OpenAI Codex

### Install via CLI (Recommended)

```bash
codex mcp add linear-server -- npx -y @anthropic-ai/linear-mcp-server
```

### Or configure manually in config.toml

Add the following to `~/.codex/config.toml` or project-level `.codex/config.toml`:

```toml
[mcp_servers.linear-server]
command = "npx"
args = ["-y", "@anthropic-ai/linear-mcp-server"]
```

### Authenticate

Launch Codex and the Linear MCP server will start automatically. On first run, it will open a browser window for Linear OAuth authentication. Complete the flow to grant access.

### Verify

In a Codex session, try listing your Linear issues to confirm the connection works.

---

## Cursor

### Configure MCP in Cursor settings

1. Open Cursor Settings > MCP
2. Click "Add MCP Server"
3. Configure:
   - **Name**: `linear-server`
   - **Type**: `command`
   - **Command**: `npx -y @anthropic-ai/linear-mcp-server`

Alternatively, add to your project's `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "linear-server": {
      "command": "npx",
      "args": ["-y", "@anthropic-ai/linear-mcp-server"]
    }
  }
}
```

### Authenticate

After adding the server, Cursor will start the MCP process. On first connection, a browser window will open for Linear OAuth. Complete the authentication flow.

### Verify

In Cursor's AI chat, ask it to list your Linear issues. If it returns results, the connection is working.

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| MCP server not found | Ensure Node.js >= 18 is installed and `npx` is available |
| OAuth flow doesn't open | Try restarting the MCP server; check firewall or browser popup blockers |
| Authentication expired | Remove and re-add the MCP server, then re-authenticate |
| Connection timeout | Check your network; Linear API requires internet access |
