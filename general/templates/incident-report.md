<!-- 
  Template: Incident report (post-mortem)
  Use for: Analyzing what went wrong after an incident, the impact, and what prevents recurrence.
  Fill in all {{placeholder}} sections. Remove this comment before sharing.
  Blameless by default — focus on systems and processes, not individuals.
-->

# Incident report: {{title}}

**Date:** {{YYYY-MM-DD}}
**Severity:** P1 | P2 | P3
**Author:** {{name}}
**Participants:** {{names of people involved in resolution}}

---

## Summary

{{One paragraph — what happened, when, and what the impact was.}}

## Timeline

| Time (UTC) | Event |
|---|---|
| {{HH:MM}} | {{What happened}} |
| {{HH:MM}} | {{What happened}} |
| {{HH:MM}} | Incident resolved |

## Impact

{{Who was affected and how? Include scope (number of users, services down, data affected) and duration.}}

## Root cause

{{What was the underlying cause? Go beyond the immediate trigger — use "5 whys" if helpful.}}

## What went well

{{What helped limit the impact or speed up resolution?}}

## What went wrong

{{What made the incident worse or the resolution harder?}}

## Action items

| Action | Owner | Due date |
|---|---|---|
| {{what needs to change}} | {{name}} | {{YYYY-MM-DD}} |

## References

{{Links to alerts, logs, PRs, related tickets.}}
