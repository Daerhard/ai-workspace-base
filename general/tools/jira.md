# Tool: Jira MCP

Connects Claude to Jira so it can read, create, and update issues directly from the conversation.

## When it's useful

- Pushing a `create-ticket.md` output directly into Jira without copy-pasting
- Fetching ticket details during a session without switching tabs
- Updating ticket status or adding comments after a task is done
- Listing open tickets for a sprint or project

## Setup

### 1. Install the MCP server

```bash
npm install -g @modelcontextprotocol/server-atlassian
```

### 2. Create a Jira API token

1. Go to [https://id.atlassian.com/manage-profile/security/api-tokens](https://id.atlassian.com/manage-profile/security/api-tokens)
2. Click **Create API token**, give it a label, and copy the value.

### 3. Add to claude_desktop_config.json

```json
{
  "mcpServers": {
    "jira": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-atlassian"],
      "env": {
        "ATLASSIAN_URL": "https://{{your-org}}.atlassian.net",
        "ATLASSIAN_EMAIL": "{{your-email}}",
        "ATLASSIAN_API_TOKEN": "{{your-api-token}}"
      }
    }
  }
}
```

Replace the three placeholder values. Do not commit this file to the repo.

### 4. Restart Claude Desktop

The Jira integration will be available in the next session.

## Environment variables

| Variable | Description |
|---|---|
| `ATLASSIAN_URL` | Your Jira instance URL, e.g. `https://yourorg.atlassian.net` |
| `ATLASSIAN_EMAIL` | The email address associated with your Atlassian account |
| `ATLASSIAN_API_TOKEN` | Your Jira API token |

## Notes

- API tokens are per-user — each team member generates their own.
- Keep tokens out of version control. If you use a `.env` file, add it to `.gitignore`.
- See the [official MCP server docs](https://github.com/modelcontextprotocol/servers/tree/main/src/atlassian) for the full list of available tools.
