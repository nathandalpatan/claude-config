---
name: ticket-and-pr
description: Write, rewrite, or tidy GitHub tickets (issues) and write pull request descriptions. A ticket is the plan (background, requirements, acceptance criteria); a PR is the implementation (what changed, how, and the evidence it works). Reads the repo's existing issues, dependencies and PRs first to catch duplicates, contradictions and ordering problems. Use when the user wants to draft, batch-create, update or clean up issues, check a backlog's flow, or write or improve a PR title or description, including when opening a PR.
---

Ticket = the plan. PR = the implementation. A ticket should minimise questions before coding; a PR should minimise questions during review.

## Always

- Read what's real before writing: the relevant code, and for a PR the actual diff and the test output from this session. Use the repo's own names for things.
- Draft first and show the user. Create or edit anything on GitHub only once they approve, unless they already told you to post it. Never close, reopen or delete issues unless asked.
- No AI attribution anywhere: no `Co-Authored-By`, no "Generated with Claude Code", no emoji footers.
- Never silently settle a design decision. Ask, with a recommended default.

# Tickets

## Step 0: read GitHub first

- `gh issue list --state all --limit 200 --json number,title,state,labels,body`
- For issues being edited or closely related: `gh issue view <n> --comments`. Decisions made in the thread must survive a rewrite.
- Blocked-by / blocking links: `gh api repos/{owner}/{repo}/issues/<n>/dependencies/blocked_by` (and `/blocking`). Epics: `.../issues/<n>/sub_issues` and `/parent`.
- Open PRs that mention the issue (`gh pr list --search "#<n>"`), since work may already be underway.

Then check the whole set (existing + new/changed) and report what you find alongside the drafts:
- **Duplicates / overlap:** merge, narrow, or cross-reference.
- **Contradictions:** conflicting numbers, rules or names between issues.
- **Gaps:** something an issue assumes exists that no issue or code provides.
- **Order and dependencies:** nothing should use a feature before the issue that builds it. Links should match the text, with no cycles.
- **Stale items:** closed issues referenced as open, merged work with unchecked criteria.

## New mode

1. **Gather:** Step 0, then the user's notes. Never invent behaviour the code or existing issues contradict.
2. **Split:** one ticket = one independently shippable, testable outcome. If the title needs "and", split it. Order a batch foundations first (data, rules), then UI, then polish.
3. **Ask only what blocks you:** if a missing decision changes the acceptance criteria, ask in one batch with recommended defaults. Otherwise pick a sensible default and list it under Assumptions.
4. **Draft** every ticket in the format below and show them together with the consistency findings.
5. **Create** with `gh issue create` only on approval. Add native blocked-by and parent links after all issues exist, apply matching labels, and report the issue numbers.

## Update mode

1. **Scope:** the named issues, or the whole backlog if asked. Run Step 0 on everything related.
2. **Rewrite** into the format below. Keep every decision already made in the body or comments, plus the number, assignees, milestone, and checked criteria that are still true. Mark anything newly invented under Assumptions as new.
3. **Show before/after** per issue, with a short list of what changed and any knock-on edits other issues need.
4. **Apply** on approval: `gh issue edit <n> --title ... --body-file ...`, then fix labels and links. Add a one-line comment if the issue's meaning changed.

## Ticket format

**Title:** the outcome in plain words, imperative, specific, under ~70 chars. `Prevent users from registering for the same event more than once`, not `Fix the event registration system`. Put categories in GitHub labels (reuse the repo's existing ones), not in the title.

**Body:**

```
## Background
Why this matters: the current behaviour and the problem it causes.

## Requirements
- The desired behaviour, one point each, describing what must happen
  rather than every line of code.

## Acceptance Criteria
- [ ] Observable, pass/fail checks that define "done".

## Technical Notes
- Services, existing patterns or files to reuse, constraints, links.

## Out of Scope / Assumptions / Dependencies
- Things a reader might assume are included; defaults chosen without
  confirmation; Blocked by #N.
```

Leave out Technical Notes and the last section when there's nothing to say.

**Writing rules:**
- Requirements say *what*, acceptance criteria say *how we'll know*. Don't repeat one as the other.
- Acceptance criteria: 3–7 items (more means split the ticket). Each one is binary and observable, with exact values ("after 15 s", not "quickly"). Cover the happy path, then the edge and failure cases that matter (duplicates, errors, empty, max, invalid input).
- No vague catch-alls: "works correctly", "is user friendly", "handles errors".
- Keep terminology, label vocabulary and ticket size consistent across a batch.
- Mark open questions as questions; don't present guesses as requirements.

# Pull requests

Read the actual diff first: `git diff origin/main...HEAD` and `git log origin/main..HEAD`. If you didn't run the tests yourself, ask or check CI rather than assuming.

**Title:** a conventional commit subject: `<type>(<scope>): <imperative description>`, under 72 characters. Use the repo's convention if it differs. Example: `feat(events): add registration confirmation emails`.

**Body:**

```
## Summary
One or two sentences: what this PR does and why.

## Changes Made
- Each meaningful change, grouped by area: what changed and, where it
  isn't obvious, why it was done this way.

## Testing
- What was actually run or checked, and the result.
- Anything not tested, said plainly (e.g. "not run on Windows").

## Related Issue
Closes #123
```

**Rules:**
- A reviewer should understand the changes without opening every file. Write `Added duplicate-registration validation to the registration endpoint and covered it in the existing tests`, not `Made some changes to registration`.
- Explain important decisions and trade-offs. Add a `Known Limitations` section for gaps or follow-ups.
- Testing lists only things that really happened. Never write "all tests pass" unless they were run and passed.
- Use `Closes #N` only when the PR fully finishes the issue. Otherwise write `Part of #N` or `Related to #N`. Leave the section out if there's no issue.
- Keep it proportional: a one-line fix gets a short description.

# Final check

Ticket: can another developer tell what to do, what the expected outcome is, and when it's finished? Are dependencies and assumptions visible?

PR: can the reviewer tell what changed, why the key decisions were made, and what evidence shows it works?
