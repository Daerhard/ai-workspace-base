# Guide: knowledge/

## What is knowledge?

Knowledge is domain context that Claude needs to understand your world — not how to behave (that's `project-rules/`), not how to do a task (that's `prompts/`), but **what your team knows** that Claude doesn't.

Think of it as the context a new developer would need to read before their first week is productive. Without it, Claude gives generic answers. With it, Claude reasons about your actual product, processes, and decisions.

---

## Two types of knowledge

**Static knowledge** — things that rarely change. Product architecture, data models, domain glossary, team structure. Write it once and update occasionally.


---

## Structure

```
knowledge/
├── index.md                        ← manifest — AI reads this first, every session
├── domain/                         ← business context, loaded selectively per task
│   └── {{domain-name}}/
│       └── overview.md
└── tech/                           ← engineering context
    ├── architecture-overview.md    ← always loaded
    ├── kotlin/
    │   └── conventions.md          ← loaded selectively (backend tasks)
    └── typescript/
        └── conventions.md          ← loaded selectively (frontend tasks)
```

### Why selective loading?

Knowledge can grow large. Loading everything every session wastes context and makes the AI slower to focus. Instead, the AI reads only the lightweight `index.md` at startup, then loads specific files on demand when the task matches.

`architecture-overview.md` is the exception — it's small, always relevant, and always loaded. Everything else (domain knowledge and language-specific tech conventions) is loaded selectively based on the task at hand.

---

## index.md — the knowledge manifest

`index.md` is the single file the AI reads at every session start. It contains a table of all available domains with tags and paths. The AI matches the task description against the tags and loads only what's relevant.

**Domain table format:**

| Domain | Tags | Path |
|---|---|---|
| {{Domain name}} | {{comma, separated, tags}} | `domain/{{folder-name}}/` |

**Loading rules defined in `index.md`:**
- Single clear tag match → load silently
- Multiple matches → ask one question
- No match → proceed without domain knowledge

Add a new row to this table whenever you create a new domain folder.

---

## Adding a new domain

1. Create a folder: `general/knowledge/domain/{{domain-name}}/`
2. Add an `overview.md` file using the template in `_example-domain/`
3. Add a row to `general/knowledge/index.md` with the domain name, tags, and path
4. The AI will automatically pick it up on the next session

---

## domain/

Each domain folder contains an `overview.md` based on the `_example-domain/` template. The template includes:

- **What this domain covers** — 2-3 sentence description of the product area
- **Glossary** — domain-specific terms and their definitions. Use this for terms that have a specific meaning in this domain — not generic definitions.
- **Business rules** — constraints and conditions Claude needs to know to avoid wrong suggestions
- **How it connects to other domains** — dependencies and interactions between domains

---

## tech/

### `architecture-overview.md` — system structure

A high-level map of your system so Claude understands where things live and how they connect. Helps Claude reason about where a change should go without needing to be told every time.

What to include:
- List of services/applications and what each one does
- How services communicate (REST, events, queues, etc.)
- Key external dependencies and integrations
- Monorepo vs. multi-repo structure and how it's organized

### `{{language}}/conventions.md` — code-level rules per language

Rules that go beyond a standard style guide — patterns specific to how your team writes code. Prevents Claude from suggesting approaches you've already moved away from.

Each language gets its own subfolder with a `conventions.md` file so you can load only what's relevant for the task. The repo ships with `kotlin/` and `typescript/` as starting points.

What to include:
- Error handling patterns
- Naming conventions for layers (e.g. service, repository, controller naming)
- How you handle DTOs, mappers, and domain objects
- Testing conventions (unit vs. integration, naming, structure)
- Framework-specific patterns your team follows

**To add a new language:**
1. Create `general/knowledge/tech/{{language}}/conventions.md`
2. Add the YAML frontmatter with appropriate tags (e.g. `tags: [python, django, backend]`)
3. Add a row to `general/knowledge/index.md` in the Tech knowledge table
4. The AI will pick it up automatically on the next session

---

## General tips

- **Shorter is better.** Claude reads this on every session. Dense walls of text reduce effectiveness — prefer clear, scannable structure.
- **Update when things change.** Stale knowledge is worse than no knowledge — Claude will confidently reason from outdated context.
- **Reference, don't duplicate.** If something is already well-documented in Confluence or a README, link to it rather than copying it here. Keep this file as the map, not the encyclopedia.
- **Start with the glossary.** It has the highest return on investment for the least effort.
