# Contributing to {{repo-name}}

Thanks for adding to the workspace. Follow these guidelines to keep the repo clean and useful.

---

## Where to put things

| What you're adding | Folder |
|---|---|
| Prompt | `general/prompts/` |
| Project rule or system instruction | `general/project-rules/` |
| Output template | `general/templates/` |
| MCP server config or API integration | `general/tools/` |
| Domain knowledge | `general/knowledge/domain/{{domain-name}}/` |
| Tech conventions | `general/knowledge/tech/{{language}}/` |

---

## File naming

Use lowercase kebab-case. Be specific.

```
# Good
prompts/summarize-meeting-notes.md
prompts/write-job-posting.md
project-rules/customer-support-agent.md

# Bad
prompts/prompt1.md
prompts/new.md
```

---

## File format (prompts and project rules)

Every file should have a header block followed by the content:

```markdown
---
title: {{Short descriptive title}}
use-case: {{One sentence — when do you reach for this?}}
author: {{Your name or GitHub handle}}
version: 1.0
---

# {{Title}}

## Purpose
{{What this prompt does and why it's useful}}

## Prompt

{{The actual prompt text. Use {{placeholder}} for dynamic values.}}

## Example usage

**Input:**
{{Example of what the user might provide}}

**Output:**
{{What Claude typically returns}}

## Notes
{{Edge cases, limitations, tips}}
```

---

## Placeholders

Always wrap dynamic values in double curly braces: `{{variable_name}}`. Use snake_case, be descriptive.

```
{{company_name}}     ✓
{{COMPANY}}          ✗
{{name}}             ✗  (too vague)
{{customer_name}}    ✓
```

---

## Submitting via Pull Request

1. Branch off `main`: `git checkout -b add/summarize-meeting-notes`
2. Add your file(s) to the relevant subfolder.
3. Open a PR with a short description.
4. A code owner must approve before merging.

## Review checklist

Before approving a PR, verify:

- [ ] File is in the right folder with the right naming convention
- [ ] Header block is complete
- [ ] All dynamic values use `{{placeholder}}` syntax
- [ ] Prompt has been tested at least once in Claude
- [ ] Output is reproducible (not overly sensitive to phrasing)

---

## Issues and ideas

Use GitHub Issues for:
- Suggesting new prompts or categories
- Reporting a prompt that no longer works well
- Proposing structural changes to the repo

Label issues with `idea`, `bug`, or `enhancement`.
