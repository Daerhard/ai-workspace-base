---
title: Write commit message
use-case: Generate a conventional commit message from a description of what changed.
author: {{repo-name}}
version: 1.0
---

# Write commit message

## Purpose

Produces a well-formed commit message following the Conventional Commits standard. Keeps the git history clean and consistent across the team.

## Prompt

```
Write a git commit message for the following change.

Change description: {{describe_what_changed}}
Ticket (optional): {{ticket_id}}

Follow the Conventional Commits format:
<type>(<scope>): <short summary>

[optional body — only if the change needs explanation beyond the summary]

[optional footer — ticket reference, breaking change notice]

Types: feat, fix, chore, refactor, docs, test, ci
- Use feat for new functionality
- Use fix for bug fixes
- Use chore for maintenance, dependencies, tooling
- Use refactor for restructuring without behaviour change
- Use docs for documentation only changes
- Use test for adding or updating tests
- Use ci for CI/CD changes

Rules:
- Summary line: max 72 characters, imperative mood ("add" not "added"), no full stop
- Body: wrap at 72 characters, explain the why not the what
- Ticket reference format: refs {{ticket_id}}

Return only the commit message, nothing else.
```

## Example usage

**Input variables:**
- `{{describe_what_changed}}` → "Added validation to reject absence requests that overlap with existing ones"
- `{{ticket_id}}` → `ALP-1234`

**Example output:**
```
feat(absence): reject overlapping absence requests

Added server-side validation to prevent duplicate absence submissions
when an employee already has an approved absence in the same period.

refs ALP-1234
```

## Notes

- If your team uses a different commit format, update the rules section in `workflow.md` and override this prompt in your personal folder.
- For very small changes (e.g. typo fix), skip the body entirely — the summary line is enough.
