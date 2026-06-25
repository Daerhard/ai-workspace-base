# Guide: skills/

## What are skills?

Skills are self-contained, reusable capabilities that Claude can trigger automatically when a task matches. Unlike prompts — which are text-in, text-out and user-triggered — a skill can span multiple steps, read and write files, and execute code.

Think of a prompt as a recipe card the user hands to Claude. A skill is a capability Claude already has loaded and reaches for on its own when the situation calls for it.


---

## Prompts vs. skills

| | Prompt | Skill |
|---|---|---|
| Triggered by | User, manually | Claude, automatically |
| Can run code | No | Yes |
| Can read/write files | No | Yes |
| Multi-step | No | Yes |
| Format | Single `.md` file | Folder with `SKILL.md` |

Use a prompt when the task is simple text-in, text-out. Use a skill when the task involves tool use, file operations, or a sequence of steps Claude should manage on its own.

---

## Anatomy of a skill

A skill is a directory containing at minimum a `SKILL.md` file:

```
my-skill/
├── SKILL.md          ← required
├── reference.md      ← optional: detailed docs Claude reads when needed
└── scripts/
    └── helper.py     ← optional: code Claude can execute
```

### SKILL.md structure

```markdown
---
name: Short skill name
description: One sentence — when should Claude trigger this skill?
---

# Instructions

The full instructions for how to execute this skill.
Reference additional files by name — Claude will read them only when needed.
```

The `name` and `description` are loaded into Claude's context at session start (progressive disclosure level 1). The full body is only read when Claude decides the skill is relevant (level 2). Additional files are read on demand (level 3+).

---

## Writing good skills

**The description is the trigger.** Claude decides whether to activate a skill based on the `description` field. Make it specific and action-oriented: "Generate KDoc comments for the selected Kotlin function" not "Document code."

**Use progressive disclosure.** Keep `SKILL.md` focused on core instructions. Move detailed reference material to separate files and link to them. Claude will read them only when needed, keeping the context window lean.

**Separate code from instructions.** If the skill involves running a script, keep the script in a `scripts/` subfolder. Claude can execute it without loading it into context.

a personal override. Same folder name = user version wins. This lets individuals customize skill behavior without touching the general version.

---

## Adding a skill to session-start.md


```markdown
## Skills

Load skills from `general/skills/` and a personal override if present.
```

Claude Cowork users can install skills directly by zipping the skill folder as a `.skill` file.
