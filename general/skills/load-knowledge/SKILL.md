---
name: load-knowledge
description: Match the current task against the knowledge index and load the relevant domain or tech knowledge files. Trigger when the user describes a task and relevant domain knowledge may exist in the workspace.
---

# Load knowledge skill

Selectively load domain or tech knowledge based on the current task description.

## When to trigger

Trigger this skill when:
- The user describes a task and you haven't loaded domain knowledge yet
- The user mentions a feature area, product domain, or technical topic
- The user asks "what do you know about X" or "load the knowledge for X"
- A new topic comes up mid-session that may have domain knowledge

## How to execute

### Step 1 — Read the index

Read `general/knowledge/index.md`. This is the only file you need to read at this step.

### Step 2 — Match the task

Compare the task description against the **tags** column in the index. Look for overlap between what the user described and the tags listed.

### Step 3 — Decide and act

**Confident single match (tags clearly align):**
Load the matching domain folder. Announce briefly:
> *"Loading [Domain] knowledge."*

**Multiple matches:**
Ask one question before loading:
> *"This task touches [Domain A] and [Domain B]. Load both, or just one?"*

**Low confidence or vague description:**
Ask one question:
> *"Which area does this relate to: [list 2-3 candidate domains from the index]?"*

**No match:**
Do not load anything. Proceed with general knowledge. If the user seems to expect domain-specific knowledge, say:
> *"I don't have specific knowledge for this area yet. You can add it to `general/knowledge/domain/`."*

### Step 4 — Confirm and continue

After loading, briefly confirm:
> *"[Domain] knowledge loaded. Ready to continue."*

Then proceed with the task.

## Notes

- Read the index file, not the full knowledge files, when deciding what to load. The index is designed to be cheap to read.
- If knowledge changes mid-session (e.g. the user switches topics), re-run this skill for the new topic.
- Do not reload knowledge that's already been loaded in this session unless the user asks.
