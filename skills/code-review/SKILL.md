---
name: code-review
description: Review code changes (diffs, PRs, files) for correctness, security, performance, and maintainability. Use when asked to review, critique, or audit code.
---

# Code Review

## Process

1. **Get context.** Read the PR description or ask what the change is meant to do. Note the language, framework, and existing repo conventions.
2. **Read the full change before commenting.** Understand intent first, then look for problems.
3. **Review in priority order** (see below). Spend effort on the top items.
4. **Verify, don't guess.** Trace the code path before claiming a bug. Run tests, linters, and type checks if tools are available.
5. **Report** using the output format below.

## Review priorities (highest first)

1. **Correctness:** logic errors, off-by-one, null/undefined handling, race conditions, unhandled errors, edge cases, resource leaks.
2. **Security:** input validation, injection (SQL/XSS/command), authn/authz gaps, hardcoded secrets, unsafe deserialization, risky dependencies.
3. **Contracts and data integrity:** breaking API changes, schema/migration safety, backward compatibility.
4. **Performance:** N+1 queries, needless allocations, poor algorithmic complexity, blocking calls in hot paths.
5. **Tests:** new behavior covered, failure paths covered, no brittle or flaky tests.
6. **Maintainability:** unclear naming, duplication, excess complexity, dead code, missing "why" comments.
7. **Style:** only what the linter/formatter doesn't catch. Lowest priority.

## Rules

- Review only the changed code and what it directly affects. Don't audit the whole codebase unless asked.
- Every finding includes: location (`file:line`), issue, why it matters, suggested fix.
- Label severity: **blocker** (must fix), **major** (should fix), **minor** (worth fixing), **nit** (optional).
- State confidence when uncertain. Never present a guess as fact.
- Follow the codebase's existing conventions, not personal preference.
- No filler praise. Mention a good pattern only if it's notable.
- If there are no real issues, say so plainly. Don't invent findings.

## Output format

**Verdict:** approve / approve with changes / request changes, plus a 1-2 sentence summary.

**Findings** (grouped by severity, blockers first):

- `file:line` [severity] Issue. Why it matters. Fix.

**Questions:** anything unclear about intent that affects the review.

**Missing tests:** specific cases worth adding (if any).
