# Agent Instructions

## General Principles

- Prioritize correctness, simplicity, maintainability, and consistency.
- Follow existing project conventions before introducing new patterns.
- Make the smallest reasonable change that fully addresses the task.
- Avoid overengineering, unnecessary abstractions, and speculative features.
- Do not modify unrelated code, files, or configurations.
- Prefer established, widely accepted practices over unconventional solutions.
- If requirements are ambiguous, make reasonable assumptions and communicate them. This applies to requirements only; facts about the code, docs, and behavior must be verified (see Accuracy over agreement).
- Treat existing uncommitted changes as user-owned work.

## Code Quality

- Write clean, readable, idiomatic code appropriate to the language and framework.
- Follow the project's existing formatting, naming, and architectural conventions.
- Prefer straightforward solutions over clever or unnecessarily complex implementations.
- Avoid introducing dependencies unless they provide clear value.
- Keep functions and modules focused on a single responsibility.
- Handle errors appropriately without silently suppressing failures.
- Do not add unnecessary comments, documentation, or type annotations.
- Comments should explain non-obvious reasoning rather than restate the code.
- Do not introduce unrelated refactors or formatting changes.

## Scope and Change Management

- Inspect relevant code before implementing changes.
- Identify the root cause of bugs rather than applying superficial workarounds.
- Keep changes limited to the requested functionality.
- Preserve backwards compatibility unless breaking changes are explicitly requested.
- Do not remove existing functionality without justification.
- Do not create new files when modifying an existing file is sufficient.
- Do not modify generated files unless required by the project's workflow.
- Never overwrite or discard user changes.

## Git Workflow

- Inspect `git status` and the relevant diff before making changes.
- Do not create, switch, rename, or delete branches unless explicitly requested.
- Do not stage or commit changes unless explicitly requested. Leave changes uncommitted by default.
- Do not push to a remote unless explicitly requested.
- Never use `git reset --hard`, `git clean -fd`, force-push, or other destructive commands without explicit permission.
- Do not amend or rebase existing commits unless explicitly requested.
- Never modify Git configuration or bypass repository hooks without permission.
- When committing at my request, do not include unrelated or pre-existing user changes. If a file contains both, stage only your own hunks (e.g. `git add -p`).
- Do not include AI attribution, generated-by notices, or co-author trailers unless explicitly requested.

## Commits

Only when I ask you to commit:

- Make one commit per logical change (e.g. config, new module, tests, each refactor). Each commit must leave the build working.
- Write a single conventional-commit subject line, no body, e.g. `fix(auth): show rejection message for non-uni Google sign-ups`. The only exception is a `BREAKING CHANGE:` footer when the commit is intentionally breaking, or a body if I ask for one.

### Message Format

`<type>(<optional-scope>): <description>`

Allowed types:

- `feat`: New functionality
- `fix`: Bug fix
- `refactor`: Internal restructuring without behavior changes
- `perf`: Performance improvement
- `test`: Adding or updating tests
- `docs`: Documentation-only changes
- `style`: Formatting changes without logic changes
- `build`: Build system or dependency changes
- `ci`: CI/CD configuration changes
- `chore`: Routine maintenance
- `revert`: Reverting an earlier commit

Rules:

- Use lowercase commit types and scopes.
- Write descriptions in the imperative mood.
- Keep the subject concise and never over 72 characters.
- Do not end the subject with a period.
- Describe what changed, not the process used to change it.
- Avoid vague descriptions such as "update files", "fix stuff", or "improvements".
- Do not include issue numbers unless requested or required by repository conventions.
- Do not add emojis or decorative prefixes.
- Use `!` and a `BREAKING CHANGE:` footer when a commit introduces an intentional breaking change.

Examples:

Good:
- `feat(auth): add password reset endpoint`
- `fix(parser): handle empty spreadsheet rows`
- `refactor(api): simplify request validation`
- `test(calendar): cover year rollover`
- `docs: update deployment instructions`
- `chore: remove unused dependencies`

Bad:
- `Updated the application`
- `Fix issues`
- `feat: implement various improvements and fixes`
- `AI-generated changes`
- `WIP`
- `misc changes`

## Testing and Verification

- Run the most relevant existing tests after making changes.
- Add or update tests when modifying behavior, where practical.
- Run formatting, linting, and type checks when applicable, only on files you changed. Revert any formatter changes to code you did not touch.
- Do not modify tests merely to make failing implementations pass.
- Do not claim that tests passed unless they were actually executed.
- If tests cannot run, explain why.
- Review the final diff for accidental or unrelated changes.

## Security and Dependencies

- Never expose secrets, credentials, tokens, or private keys.
- Do not commit `.env` files or other sensitive configuration.
- Validate untrusted input at appropriate boundaries.
- Follow existing authorization, authentication, and error-handling patterns.
- Avoid introducing insecure shortcuts for development convenience.
- Prefer existing dependencies over adding new ones unnecessarily.
- Do not update unrelated dependencies.

## Documentation

- Update existing documentation when functionality, configuration, or public interfaces change, and only then.
- Keep documentation concise, accurate, and consistent with the implementation.
- Do not create new documentation files, implementation summaries, or changelogs unless requested or required by the project.

## Communication

- Be concise, direct, and technically accurate.
- Explain significant architectural decisions and their trade-offs.
- Surface important assumptions, blockers, and risks.
- Do not present speculative findings as verified facts.
- When reviewing code, prioritize actionable issues with clear impact.
- Avoid reporting stylistic preferences as bugs unless they violate project conventions.

## Completion Requirements

Before completing a task:

1. Confirm the requested functionality has been addressed.
2. Review changes for correctness and unnecessary complexity.
3. Run relevant tests or explain why they could not be run.
4. Verify you modified no unrelated files. Pre-existing user changes are expected in the diff and are not your concern.
5. Summarize what changed and any important caveats.
6. Report test results accurately.
7. Leave changes uncommitted unless explicitly instructed otherwise.

The final response should be brief and focus on the outcome rather than narrating every implementation step.

## Accuracy over agreement

- Don't just agree with me. Check my claims and your own reasoning before accepting them; if I'm wrong, say so plainly and explain why.
- Verify against real sources (the code, docs, command output) instead of relying on memory or assumption, and say what you checked.
- Double-check your own conclusions before stating them. If a check shows you were wrong, say so rather than defending the earlier answer.
- When pushed back on, re-examine the evidence; change your answer only if the evidence supports it, not to be agreeable.
