# Guide: prompts/

## What are prompts?


The distinction from the other folders:

| Folder | Purpose | When it's active |
|---|---|---|
| `project-rules/` | How Claude behaves | Always, every session |
| `knowledge/` | Context about your world | Always, every session |
| `prompts/` | How to do a specific task | On demand |
| `skills/` | Reusable capabilities with code | When triggered by task |

---

## What belongs here

A good candidate for `prompts/` is a task that:
- Happens repeatedly across the team
- Has a consistent structure or expected output
- Benefits from a standardized approach

One file = one task. If a prompt covers two different jobs, split it.

---

## File format

Every prompt file follows the same structure (see `_template.md`):

```markdown
---
title: Short descriptive title
use-case: One sentence — when do you reach for this?
author: Your name or GitHub handle
version: 1.0
---

## Purpose
What this prompt does and why it's useful.

## Prompt
The actual prompt text. Use {{placeholder}} for dynamic values.

## Example usage
Input variables and an example of what Claude returns.

## Notes
Edge cases, tips, suggested follow-ups.
```

---

## Writing good prompts

**Be specific about the output.** Don't just say "write a PR description" — define the sections, length, and tone you want. Claude follows explicit structure much more reliably than vague instructions.

**Use placeholders for everything dynamic.** Any value the user needs to supply should be `{{variable_name}}`. Use snake_case and be descriptive: `{{branch_diff}}` not `{{input}}`.

**Include an example.** A single good input/output example is worth more than two paragraphs of explanation. Claude uses it to calibrate tone and format.

**State what to ignore.** If there are things Claude should not include in the output, say so explicitly — e.g. "Do not include implementation details, only the user-facing impact."

**Keep it focused.** If you find yourself writing "and also...", that's a second prompt.

---

## Prompts vs. skills

Use a prompt when the task is text-in, text-out and doesn't require tool use or multi-step execution. Use a skill when the task involves running code, reading files, or a sequence of operations that Claude needs to orchestrate. See `docs/guides/skills.md` for more.
