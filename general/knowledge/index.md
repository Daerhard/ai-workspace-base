# Knowledge index

This file is read at the start of every session to determine which knowledge is relevant for the current task. Do not load full knowledge files unless they match the task — read this index first, then load selectively.

## How to use this index

1. Read this file at session start.
2. Match the task description against the **tags** column.
3. Load the matching knowledge path(s).
4. If the match is ambiguous or spans multiple domains, ask: *"This touches [X] and possibly [Y] — should I load both?"*
5. If nothing matches, proceed without domain-specific knowledge.

---

## Domain knowledge

Domain knowledge describes the business domain — what the product does, how it works, and the rules that govern it. Load this when the task involves building or changing product behaviour.

| Domain | Tags | Path |
|---|---|---|
| {{Domain name}} | {{comma, separated, tags}} | `domain/{{folder-name}}/` |

---

## Tech knowledge

Tech knowledge describes how the system is built — architecture, conventions, and past decisions. Load this when the task involves implementation, code structure, or technical decisions.

`tech/architecture-overview.md` is always loaded — it applies to every session. Language-specific conventions are loaded selectively.

| Topic | Tags | Path |
|---|---|---|
| Architecture overview | **always load** | `tech/architecture-overview.md` |
| Kotlin conventions | kotlin, backend, spring, jvm, server | `tech/kotlin/conventions.md` |
| TypeScript conventions | typescript, frontend, react, ui, client | `tech/typescript/conventions.md` |

---

## Loading rules

**Auto-load (no question needed):**
- Single clear match between task description and tags → load silently, mention briefly: *"Loading [X] knowledge."*
- Task is purely technical with no domain component → load tech knowledge only

**Ask one question:**
- Task matches two or more domains → *"This touches [X] and [Y]. Load both?"*
- Task description is too vague to match confidently → *"Which area does this relate to: [list matching domains]?"*

**Load nothing extra:**
- No tag match → proceed with general project rules and knowledge only
- User says "just start" → proceed immediately, offer to load knowledge if needed later
