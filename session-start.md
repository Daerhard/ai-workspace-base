# Session Start

<!-- REPO_NAME: {{repo-name}} -->

You are an AI assistant operating within the {{team-name}} workspace.
Follow these instructions at the start of every session.

## 1. Load workspace specs

The `general/` folder contains the workspace configuration. Always load and apply:

- `general/project-rules/` — active project rules and system instructions
- `general/knowledge/index.md` — knowledge manifest (read this, do not load full knowledge yet)
- `general/knowledge/tech/architecture-overview.md` — always load (lightweight, always relevant)
- `general/prompts/` — reusable prompt templates
- `general/templates/` — output templates
- `general/tools/` — tool and integration configs

Domain knowledge is loaded selectively — see step 2.

## 2. Load relevant knowledge

Once the user describes the task, match it against `general/knowledge/index.md`:

This applies to both domain knowledge (business areas) and language-specific tech knowledge (Kotlin, TypeScript). Architecture overview is already loaded — skip it here.

**Single clear match** → load that domain's folder silently, mention it briefly:
> *"Loading [Domain] knowledge."*

**Ambiguous or multiple matches** → ask one question:
> *"This touches [X] and possibly [Y] — should I load both?"*

**No match or user says "just start"** → proceed without domain knowledge. Offer to load it later if needed.

## 3. Confirm and proceed

Briefly confirm what's loaded, then ask how you can help:

> "I've loaded the workspace specs [+ domain: X if applicable]. What are we working on?"

## 4. Responding to prompt requests

When the user asks to see available prompts (e.g. "show me the prompts", "what prompts do you have", "list prompts"):

1. Read all `.md` files in `general/prompts/` (excluding `_template.md`).
2. List them by `title` and `use-case` from the frontmatter.
3. Ask which one to apply.

When the user selects a prompt:

1. Read the full prompt file.
2. Identify all `{{placeholder}}` variables.
3. Ask the user to supply any values that aren't already available from context.
4. Apply the prompt with the filled-in values.

