---
name: code-documentation
description: Read code files and generate or update inline documentation, docstrings, and README sections. Trigger when the user asks to document, add comments, or generate docs for code.
---

# Code documentation skill

Generate or update documentation for code files — inline comments, docstrings, and README sections.

## When to trigger

Trigger this skill when the user:
- Asks to "document", "add comments", or "write docs" for a file or function
- Asks to generate or update a README section
- Asks to explain what a piece of code does and wants it written into the file

## How to approach it

1. **Read the code first.** Read the full file before writing any documentation. Understand what it does before describing it.
2. **Document intent, not mechanics.** Good documentation explains *why* and *what*, not *how*. The code already shows how.
3. **Match the existing style.** If the file already has documentation, match its tone and format. Don't introduce a new style mid-file.
4. **Apply the team's conventions.** Refer to `general/knowledge/coding-conventions.md` for language-specific documentation standards.

## Output rules

- **Inline comments:** Only add comments where the logic is non-obvious. Do not comment every line.
- **Docstrings/KDoc/JSDoc:** Add to all public functions, classes, and interfaces. Include: purpose, parameters, return value, and any exceptions thrown.
- **README sections:** Use plain markdown. Keep sections short — link to code rather than duplicating it.

## Languages

Apply the standard documentation format for the language in use:
- Kotlin → KDoc (`/** */`)
- Java → Javadoc (`/** */`)
- Python → docstrings (`"""`)
- TypeScript/JavaScript → JSDoc (`/** */`)
- Other → follow the language's idiomatic convention

## Notes

- When updating existing docs, preserve any information that is still accurate. Only rewrite what has changed or is missing.
- If the code is unclear or confusing, flag it with a `// TODO: clarify` comment rather than documenting incorrect assumptions.
