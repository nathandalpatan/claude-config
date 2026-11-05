---
description: Commit current changes as separate logical commits
allowed-tools: Bash(git status:*), Bash(git diff:*), Bash(git add:*), Bash(git commit:*), Bash(git log:*)
---

Review the working tree with `git status` and `git diff`, then commit the changes following my global CLAUDE.md rules:

- One commit per logical change (config, new module, tests, each refactor). Stage only the files for that change.
- Each commit must leave the build working.
- Message: a single conventional-commit subject line, no body.

Don't push. $ARGUMENTS
