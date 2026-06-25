# Tool: GitHub MCP

Connects Claude to GitHub so it can read repos, issues, PRs, and commits — and create or update them — directly from the conversation.

## When it's useful

- Reviewing open PRs without leaving Claude
- Creating issues from a `create-ticket.md` output
- Reading file contents from a repo during a session
- Checking CI status or recent commits

## Setup

### 1. Install the MCP server

```bash
npm install -g @modelcontextprotocol/server-github
```

### 2. Create a GitHub personal access token

1. Go to **GitHub → Settings → Developer settings → Personal access tokens → Fine-grained tokens**
2. Create a new token with the following permissions for the relevant repos:
   - **Contents:** Read
   - **Issues:** Read and write
   - **Pull requests:** Read and write
   - **Metadata:** Read
3. Copy the token value — you'll need it in the next step.

### 3. Add to claude_desktop_config.json

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "{{your_github_pat}}"
      }
    }
  }
}
```

Replace `{{your_github_pat}}` with your token. Do not commit this file to the repo.

### 4. Restart Claude Desktop

The GitHub integration will be available in the next session.

## Environment variables

| Variable | Description |
|---|---|
| `GITHUB_PERSONAL_ACCESS_TOKEN` | Your GitHub personal access token |

## Notes

- Keep your PAT out of version control. Use a secrets manager or environment variable if sharing config across machines.
- Fine-grained tokens scoped to specific repos are more secure than classic tokens with broad access.
- See the [official MCP server docs](https://github.com/modelcontextprotocol/servers/tree/main/src/github) for the full list of available tools.
