---
title: Review code
use-case: Perform a structured code review covering logic, edge cases, conventions, and security.
author: {{repo-name}}
version: 1.0
---

# Review code

## Purpose

Produces a structured code review that goes beyond syntax — covering logic correctness, edge cases, adherence to team conventions, and potential issues. Useful as a first-pass review before a human reviewer looks at it.

## Prompt

```
Review the following code as an experienced engineer on this team.

Context: {{what_this_code_does}}
Language/framework: {{language_or_framework}}

Code:
{{paste_code_here}}

Review it across these dimensions and flag issues as: 🔴 must fix / 🟡 should fix / 🔵 suggestion

**Logic and correctness**
Are there bugs, incorrect assumptions, or cases where the code will not behave as intended?

**Edge cases**
What inputs or states could cause unexpected behaviour? Are null/empty/boundary cases handled?

**Team conventions**
Does the code follow the team's naming conventions, error handling patterns, and structure? Reference coding-conventions.md if relevant.

**Security and data handling**
Are there any obvious security issues — unvalidated input, exposed sensitive data, missing auth checks?

**Testability and test coverage**
Is the code structured in a way that makes it testable? Are the right things being tested?

**Suggestions**
Anything that could be simplified, made more readable, or done differently — not blockers, just improvements.

End with a one-line verdict: ✅ Ready to merge / ⚠️ Needs minor changes / 🚫 Needs significant rework.
```

## Example usage

**Input variables:**
- `{{what_this_code_does}}` → "Service method that calculates the number of available shifts for a given employee and week"
- `{{language_or_framework}}` → "Kotlin + Spring Boot"
- `{{paste_code_here}}` → [paste the relevant code]

## Notes

- For large PRs, review file by file rather than pasting everything at once.
- If your team has specific conventions defined in `general/knowledge/coding-conventions.md`, remind Claude to apply them by adding: "Also apply the conventions in coding-conventions.md."
