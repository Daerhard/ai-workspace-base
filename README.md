# {{repo-name}}

A ready-to-use AI workspace with reusable prompts, project rules, and tool configurations for Claude. Fork it to create your own team workspace.

## Repo structure

```
.
├── general/                          # Workspace configuration
│   ├── project-rules/                # How Claude behaves — always active
│   │   ├── role.md
│   │   ├── communication.md
│   │   ├── output-format.md
│   │   └── workflow.md
│   ├── knowledge/                    # Context loaded selectively per task
│   │   ├── index.md                  # Manifest — AI reads this first, loads selectively
│   │   ├── domain/                   # Business context — loaded when task matches
│   │   │   └── _example-domain/      # Template for new domain folders (includes glossary)
│   │   └── tech/                     # Engineering context
│   │       ├── architecture-overview.md   # Always loaded
│   │       ├── kotlin/
│   │       │   └── conventions.md    # Loaded for backend tasks
│   │       └── typescript/
│   │           └── conventions.md    # Loaded for frontend tasks
│   ├── prompts/                      # Reusable task prompts — invoked on demand
│   │   ├── write-pr-description.md
│   │   ├── write-commit-message.md
│   │   ├── review-code.md
│   │   └── create-ticket.md
│   ├── skills/                       # Auto-triggered capabilities
│   │   ├── code-documentation/
│   │   └── load-knowledge/
│   ├── templates/                    # Document structures — filled in by Claude or humans
│   │   ├── poc.md
│   │   ├── technical-spec.md
│   │   ├── incident-report.md
│   │   └── onboarding.md
│   └── tools/                        # MCP server configs and integrations
│       ├── github.md
│       └── jira.md
├── setup/
│   └── skills/
│       └── generate-workspace/       # Generate a new workspace with Claude Code / Cowork
├── docs/
│   ├── github-setup.md               # Branch protection and CODEOWNERS setup
│   └── guides/                       # Explanation of each section
│       ├── project-rules.md
│       ├── knowledge.md
│       ├── prompts.md
│       ├── skills.md
│       ├── templates.md
│       └── tools.md
├── session-start.md                  # Entry point for all AI tools
├── CLAUDE.md                         # Auto-loaded by Claude Code — points to session-start.md
├── CONTRIBUTING.md
└── .github/
    └── CODEOWNERS
```

## How it works

`session-start.md` is the single entry point. It loads `general/` at the start of every session and matches knowledge to the task automatically.

### What's automatic vs. on demand

| Folder | How it's used |
|---|---|
| `project-rules/` | Always active — loaded every session |
| `knowledge/` | Selective — `architecture-overview.md` always loads; domain and language conventions matched automatically to the task |
| `skills/` | Auto-triggered — Claude activates when the task matches the skill description |
| `prompts/` | Available on demand — ask "show me the prompts" to list and apply them |
| `templates/` | Available on demand — reference in a prompt or ask Claude to fill one in |
| `tools/` | One-time setup, then always available |

## Using with Claude Code

`CLAUDE.md` at the repo root is automatically read by Claude Code at session start — no setup needed beyond cloning. It points Claude to `session-start.md` which handles the rest.

This repo is also a Claude Code plugin marketplace. Add it to make the workspace skills available:

```bash
/plugin marketplace add {{org}}/{{repo-name}}
/plugin install workspace-skills@{{marketplace-name}}
```

To make the marketplace available automatically in a project repo, add this to `.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "{{marketplace-name}}": {
      "source": {
        "source": "github",
        "repo": "{{org}}/{{repo-name}}"
      }
    }
  }
}
```

## Using with Claude (Cowork / Desktop)

Add `session-start.md` as a project instruction in your Claude Project. Claude will load the workspace specs at the start of every session.

## Creating a new workspace from this template

**With Claude Code or Cowork:**

```bash
/plugin marketplace add {{org}}/{{repo-name}}
/plugin install workspace-setup@{{marketplace-name}}
```

Then: *"Generate a new workspace"* — Claude asks for your inputs and generates the full workspace locally. You push to GitHub manually.

## Principles

- **Keep it simple** — clean, focused prompts beat clever ones.
- **Use placeholders** — always mark dynamic parts as `{{variable_name}}`.
- **Stay modular** — one file, one purpose. Easy to diff, easy to reuse.
- **Work in the open** — use GitHub Issues for ideas, PRs for changes.
