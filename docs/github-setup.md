# GitHub Setup

## Branch protection

Changes to `general/` affect everyone, so they should go through a review. GitHub Rulesets (Settings → Rules → Rulesets) let you enforce this at the path level.

Recommended setup:

1. Create a new Ruleset targeting the `main` branch
2. Add a file path filter: `general/**`
3. Enable: *Require a pull request* + *Require review from Code Owners*
4. Save

---

## CODEOWNERS

Add the following to `.github/CODEOWNERS`, replacing the placeholders with your GitHub org and handles:

```
# Changes to general/ require approval
/general/       @{{org}}/{{admins-team}}

# Changes to .github/ require approval
/.github/       @{{org}}/{{admins-team}}
```
