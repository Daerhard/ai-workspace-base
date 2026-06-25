---
title: Create ticket
use-case: Turn a rough idea, bug report, or feature request into a well-structured issue.
author: {{repo-name}}
version: 1.0
---

# Create ticket

## Purpose

Transforms a rough description into a complete, actionable ticket with clear acceptance criteria. Reduces back-and-forth during refinement and ensures nothing important is missing before work starts.

## Prompt

```
Write a well-structured ticket based on the following input.

Type: {{bug | feature | chore | spike}}
Raw description: {{describe_the_issue_or_feature}}
Reporter context (optional): {{any_additional_context}}

Produce the ticket with exactly these sections:

**Summary**
One sentence — what is this ticket about?

**Background**
Why does this matter? What is the current behaviour or situation, and why is it a problem or opportunity?

**Acceptance criteria**
A checklist of specific, testable conditions that must be true for this ticket to be considered done.
Format: - [ ] {{condition}}

**Out of scope**
Anything explicitly not covered by this ticket to prevent scope creep.

**Open questions**
Any unknowns that need to be resolved before or during implementation.

Keep the language precise and technical. Avoid vague terms like "improve" or "fix" without specifying what the expected outcome is.
```

## Example usage

**Input variables:**
- `{{type}}` → `bug`
- `{{describe_the_issue_or_feature}}` → "Absence requests submitted on the last day of the month are sometimes saved with the wrong month"
- `{{reporter_context}}` → "Happens when the user's timezone is UTC+2 and they submit after 10pm"

## Notes

- For Jira-specific fields (story points, components, epic link), add them manually after generation or override this prompt in your personal folder with a Jira-flavored version.
- For spikes, replace "Acceptance criteria" with "Definition of done" and focus on what knowledge or decision the spike should produce.
