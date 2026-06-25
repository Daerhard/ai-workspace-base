# Guide: templates/

## What are templates?

Templates define the shape of a deliverable — blank document structures that either a human fills in directly, or that Claude uses as the target format when generating output.

The distinction from the other folders:

| Folder | Purpose |
|---|---|
| `prompts/` | Tells Claude *how* to produce something |
| `templates/` | Defines *what the output should look like* |
| `skills/` | Orchestrates both — executes steps and formats output |

A prompt and a template often work together: the prompt instructs Claude to produce a technical spec, and the template defines the exact sections and structure it should follow.

---

## How to use templates with Claude

Reference the template explicitly in your prompt:

> "Write a technical spec for this feature. Use the structure defined in `general/templates/technical-spec.md`."

Or paste the template directly into the conversation and ask Claude to fill it in:

> "Fill in this template based on the following requirements: [paste template] [paste requirements]"

---

## What belongs here

A good candidate for `templates/` is a document that:
- Your team produces repeatedly
- Has a consistent structure that everyone should follow
- Benefits from being standardized (easier to read, review, and compare)

---

## File format

Templates are plain markdown with `{{placeholder}}` sections. No YAML frontmatter needed — they are the output, not the instruction.

Each template should start with a short comment explaining what it is and when to use it:

```markdown
<!-- 
  Template: Technical spec
  Use for: Proposing new features or architectural changes before implementation.
  Fill in all {{placeholder}} sections. Remove this comment before sharing.
-->
```

---

## Tips

- **Keep placeholders descriptive.** `{{describe_the_problem_being_solved}}` is clearer than `{{problem}}`.
- **Include guidance in comments.** Use HTML comments (`<!-- -->`) to explain what belongs in each section. Remove them in the final document.
- 
