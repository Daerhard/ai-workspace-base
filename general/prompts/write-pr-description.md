---
title: Write PR description
use-case: Generate a structured pull request description from a branch diff or change summary.
author: {{repo-name}}
version: 1.0
---

# Write PR description

## Purpose

Produces a consistent, well-structured PR description that gives reviewers the context they need without having to dig through the diff.

## Prompt

```
Write a pull request description based on the following changes.

Ticket: {{ticket_id}}
Branch: {{branch_name}}
Changes summary: {{describe_what_changed}}

Produce the description with exactly these sections:

**What changed**
A concise summary of what this PR does. 2-3 sentences max. Focus on the what, not the how.

**Why**
The motivation behind the change. Reference the ticket if relevant.

**How to test**
Step-by-step instructions for a reviewer to verify the change works as expected.

**Notes for reviewers**
Anything the reviewer should pay special attention to — edge cases, areas of uncertainty, deliberate trade-offs.

Keep the tone direct and technical. Do not include implementation details that are already visible in the diff.
```

## Example usage

**Input variables:**
- `{{ticket_id}}` → `ALP-1234`
- `{{branch_name}}` → `feat/ALP-1234-add-absence-export`
- `{{describe_what_changed}}` → "Added a CSV export endpoint for absence records, accessible from the absence overview page"

## Notes

- If your team has a specific PR template in `.github/pull_request_template.md`, append it to the prompt so Claude matches the format exactly.
