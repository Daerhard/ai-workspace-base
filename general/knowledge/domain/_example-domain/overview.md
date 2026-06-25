---
domain: {{Domain name}}
tags: [{{tag1}}, {{tag2}}, {{tag3}}]
---

# {{Domain name}}

<!--
  This is a domain knowledge file. It is loaded selectively — only when the current
  task matches this domain's tags in knowledge/index.md.

  Keep it focused and scannable. Claude reads this to understand the domain before
  implementing or advising. Avoid duplicating what's in code or external docs — link instead.

  See docs/guides/knowledge.md for guidance.
-->

## What this domain covers

{{Describe what this domain is about in 2-3 sentences. What product area does it belong to? What problem does it solve?}}

## Glossary

| Term | Definition |
|---|---|
| {{term}} | {{what it means in this domain — not the generic definition}} |
| {{term}} | {{what it means in this domain}} |

## Business rules

<!--
  Rules that govern how this domain behaves. These are the things Claude most commonly
  needs to know to avoid suggesting something that violates a business constraint.
-->

{{Describe the key rules — constraints, conditions, edge cases that matter.}}

## How it connects to other domains

{{List other domains this one interacts with and how. E.g. "Shift Cards depend on Automatic Planning output."}}

