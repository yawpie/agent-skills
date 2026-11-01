---
name: atomic-commits
description: Organize working-tree changes into small, logical, independently reviewable Git commits. Use when implementing multiple changes, splitting an existing diff into separate commits, or preparing clean Conventional Commits. Do not trigger for tasks that do not modify or organize Git history.
---

# Atomic Commits

Create a series of focused Git commits so changes are easy to review, revert, and trace. Prefer one logical purpose per commit instead of one commit per file.

## Non-negotiable safeguards

- Inspect `git status --short`, current branch, and relevant diffs before modifying the index or committing.
- Never stage or commit secrets, credentials, environment files, generated artifacts, or unrelated user changes.
- Do not overwrite, discard, reset, amend, rebase, cherry-pick, force-push, or otherwise rewrite existing history without explicit authorization.
- Never assume all uncommitted changes belong to the current task. Ask for ownership clarification if a change cannot be safely attributed; otherwise leave it untouched.
- Do not create commits unless the user has requested committing changes or explicitly authorized this workflow. When the user requested only a plan or review, propose the commit boundaries without committing.
- Preserve functional behavior and avoid mixing refactoring with feature work unless intrinsically required.

## Workflow

1. **Inspect:** Read `git status --short`, `git diff`, `git diff --cached`, and recent `git log --oneline -5`. Identify existing staged changes and untracked files. Avoid leaking secret values into reports.
2. **Classify:** Group only task-related hunks by intent: feature, fix, refactor, test, docs, build, or chore. Each group must be understandable, independently testable when feasible, and reversible.
3. **Plan:** Present commit order with a brief purpose, relevant files/hunks, and a proposed Conventional Commit subject. Put foundational changes ahead of dependents. Keep user-owned staged changes separate.
4. **Implement:** Make changes in logical increments. If files contain mixed changes, stage selected hunks with `git add -p` or a precise patch. Do not use blanket `git add .` in a dirty working tree.
5. **Verify:** For each planned commit, inspect `git diff --cached --check`, `git diff --cached --stat`, and `git diff --cached`. Run the most relevant available tests, linting, or build checks. Record skipped checks and reasons.
6. **Commit:** Commit only the verified staged group using a Conventional Commit subject such as `feat(auth): add token refresh`, `fix(api): handle duplicate requests`, or `test(orders): cover retries`. Keep the subject concise and in imperative form.
7. **Repeat:** Check working tree and staging area after every commit. Never absorb unrelated changes into a later commit.
8. **Report:** List commits in order with abbreviated SHA, subject, tests run, and any remaining uncommitted changes or risks.

## Choosing commit boundaries

- Combine tightly coupled changes required for one coherent behavior.
- Split independent capabilities and documentation updates when each stands alone.
- Include tests with the feature or fix they validate, rather than deferring all tests to a separate commit.
- Avoid artificial splits that leave the codebase broken between commits, when feasible.
- If a single file contains unrelated modifications, stage individual hunks only after confirming each belongs to the task.

## Language

Follow the user's preferred language for explanations. Use English Conventional Commit types (`feat`, `fix`, `docs`, `refactor`, `test`, `build`, `chore`) in Git subjects. Indonesian explanations are welcome; keep subjects short and explicit.
