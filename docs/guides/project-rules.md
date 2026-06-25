# Guide: project-rules/

## What are project rules?

Project rules are system-level instructions that are always active — they shape how Claude behaves in every session, before any task-specific prompt is used. Think of them as the onboarding doc you'd give a new employee: not "how to do task X" but "how we work here."

The key distinction from prompts: project rules are **always loaded**, regardless of the task. A prompt for "write a PR description" is only used when someone needs a PR description. A project rule saying "always use conventional commits format" applies to everything Claude does.

---

## What belongs here

Project rules typically cover four areas. We keep them in separate files so they're easy to override at the user level.

### `role.md` — Who is Claude in this team's context?

Define the product, domain, and tech stack so Claude has the background it needs to make good judgment calls without being told every time.

What to include:
- What your product does in 2-3 sentences
- Primary tech stack (languages, frameworks, infrastructure)
- The team Claude is assisting (e.g. engineering, product, ops)
- Any domain-specific terminology Claude should understand

Example:
> You are an AI assistant working within the {{team-name}} engineering team. {{team-name}} builds {{product description}}. The primary stack is {{tech stack}}.

### `communication.md` — How should Claude communicate?

Define tone, language, and interaction style so responses feel consistent across the team.

What to include:
- Tone (formal, casual, direct)
- Language (English only? German too? When to switch?)
- Default response length (concise by default, or detailed?)
- When to ask clarifying questions vs. make a reasonable assumption and proceed
- Whether to explain reasoning or just deliver the result

### `output-format.md` — How should responses be structured?

Prevent inconsistency in how Claude formats its output.

What to include:
- When to use markdown vs. plain text
- Code block conventions (always specify language, etc.)
- Whether to use bullet points or prose
- How to handle long outputs (summarize first, then detail)
- Specific format requirements for recurring outputs (commit messages, PR titles, etc.)

### `workflow.md` — Team-specific behavioral rules

Guardrails and habits specific to how your team works.

What to include:
- Git conventions (commit message format, branch naming)
- What Claude should always do (e.g. summarize what it did at end of session)
- What Claude should never do (e.g. push to main, delete files without confirmation)
- How to handle uncertainty (flag it explicitly rather than guessing silently)
- Any compliance or security rules relevant to the team

---

## General tips

- **Keep each file focused.** One concern per file makes user-level overrides clean — a user can replace just `communication.md` without touching the rest.
- **Be specific.** "Be concise" is less useful than "Keep responses under 5 sentences unless the user asks for more detail."
- **Use positive framing.** "Always summarize changes at the end" is clearer than "Don't forget to summarize."
- **Iterate.** Start minimal and add rules when you notice Claude doing something consistently wrong across the team.
