---
name: generate-workspace
description: Generate a new AI workspace from this template. Trigger when the user wants to create, set up, or fork a new workspace.
---

# Generate workspace skill

Create a fully configured team workspace by cloning the template and substituting all placeholder values. Works in Claude Code (terminal) and Claude Cowork (desktop).

## When to trigger

Trigger this skill when:
- The user says "create a new workspace", "set up a workspace", "fork the template"
- The user wants to create a team-specific version of this repo

## Step 1 — Collect inputs

Ask the user for the following values. Collect all of them before proceeding.

| Input | Description | Example |
|---|---|---|
| `repo_name` | Name of the new GitHub repo | `{{repo-name}}-absences` |
| `target_dir` | Local folder to generate into (absolute path or `~/Desktop/{{repo_name}}`) | `~/Desktop/{{repo-name}}-absences` |
| `github_org` | GitHub org or user to push to later | `{{org}}` |
| `team_name` | Human-readable team or squad name | `{{team-name}}` |
| `marketplace_name` | Short identifier for the marketplace (no spaces) | `{{marketplace-name}}` |

## Step 2 — Clone the template

```bash
git clone https://github.com/{{org}}/{{repo-name}}.git {{target_dir}}
cd {{target_dir}}
rm -rf .git
```

## Step 3 — Substitute all placeholder values

Run the following replacements across all files:

```bash
# Repo name (appears in README, session-start.md, CONTRIBUTING.md)
find . -type f -name "*.md" -o -name "*.json" -o -name "*.sh" | \
  xargs sed -i '' 's/{{repo-name}}/{{repo_name}}/g'

# Marketplace name
find . -type f -name "*.md" -o -name "*.json" | \
  xargs sed -i '' 's/{{marketplace-name}}/{{marketplace_name}}/g'

# GitHub org
find . -type f -name "*.md" -o -name "*.json" | \
  xargs sed -i '' 's/{{org}}/{{github_org}}/g'

# Team name
find . -type f -name "*.json" | \
  xargs sed -i '' 's/{{Team or org name}}/{{team_name}}/g'

# Team description in marketplace.json
# Edit .claude-plugin/marketplace.json directly — set description to a short sentence describing {{team_name}}'s workspace.

```

> Note: on Linux, `sed -i ''` should be `sed -i`. Adjust based on the OS.

Also update `session-start.md` line 1 — replace the generic product description:
> *"You are an AI assistant operating within the {{team-name}} workspace."*

with:
> *"You are an AI assistant operating within the {{team_name}} workspace."*

## Step 4 — Remove the setup skills

The setup skills are only needed for generating workspaces — they should not be part of the forked repo.

```bash
rm -rf setup/
```

Also remove `./workspace-setup` from `.claude-plugin/marketplace.json`.

## Step 5 — Initialise git and commit

```bash
git init
git add -A
git commit -m "init: generate {{repo_name}} workspace"
```

## Step 6 — Print next steps

Tell the user:

```
✓ Workspace generated at {{target_dir}}

Next steps:
  1. Create the GitHub repo at github.com/{{github_org}}/{{repo_name}}
  2. Run: git remote add origin git@github.com:{{github_org}}/{{repo_name}}.git
  3. Run: git push -u origin main
  4. Fill in general/project-rules/role.md with your product and tech stack
  5. Fill in general/knowledge/tech/architecture-overview.md
  6. Set up branch protection — see docs/github-setup.md
```

## Notes

- Do not start the substitutions until all inputs are confirmed.
- If `target_dir` already exists and is non-empty, warn the user and ask before proceeding.
- The setup/ folder and `workspace-setup` marketplace plugin should always be removed from the fork — they are only relevant to the template repo itself.
