# Guide: tools/

## What are tools?


Not the integration code itself, but the config snippets and setup steps the team needs to get connected.

---

## What is MCP?

MCP (Model Context Protocol) is an open standard that lets Claude connect to external tools and data sources. Once an MCP server is configured, Claude can interact with that system directly — reading issues, creating tickets, querying databases — without the user having to copy-paste information back and forth.

MCP servers are configured in `claude_desktop_config.json` on your local machine. Each tool file in this folder contains the config snippet to add.

---

## How to use a tool config

2. Copy the config snippet.
3. Add it to your `claude_desktop_config.json` under the `mcpServers` key.
4. Set the required environment variables.
5. Restart Claude Desktop.

### Location of claude_desktop_config.json

| OS | Path |
|---|---|
| macOS | `~/Library/Application Support/Claude/claude_desktop_config.json` |
| Windows | `%APPDATA%\Claude\claude_desktop_config.json` |

---

## What belongs here

Add a file to `tools/` for each integration your team uses. Each file should include:
- What the integration does and when it's useful
- The MCP config snippet (ready to paste)
- Required environment variables and how to get them
- A short setup walkthrough
- Any known limitations

---

## Personal overrides

