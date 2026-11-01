---
name: atomic-commits
description: Implement code changes in separate, purpose-focused Git commits so they are easy to trace, review, and revert. Use when the user requests incremental implementation, separate commits, atomic commits, commit terpisah, or splitting existing changes into multiple commits.
---

# Atomic Commits

Complete the requested work with one logical purpose per commit. When this skill is requested for implementation, create local commits as work progresses unless the user requests planning only or prohibits commits. Automatic invocation does not expand task authorization. Follow the user's instructions and repository rules.

The [Indonesian version](references/indonesian.md) provides the same instructions. Read it only when Indonesian instructions are needed. Use one language version at a time. When maintaining this skill, keep both versions equivalent.

## Inspect the initial state

- Read repository instructions, Git status, staged and unstaged diffs, and a few recent commit messages. Record the branch, initial HEAD if one exists, and changes present before starting.
- Distinguish this task's changes from the user's existing work. Include pre-existing changes only when the user asks for them to be committed.
- If the directory is not a Git repository, continue safe work and explain that commits cannot yet be created. Do not initialize Git or change identity configuration without authorization.
- If merge conflicts or an unfinished Git operation exist, do not resolve or abort them without clear relevance and authorization.

## Define commit boundaries

Briefly describe the purpose of each planned commit and its dependency order. One simple change needs only one commit. Do not request approval for routine grouping already within the task's scope.

- Separate purposes that can be reviewed independently, such as validation fixes, feature additions, and independent refactoring.
- Include the tests, configuration, migrations, documentation, or lockfiles required by an implementation in the same commit. Do not intentionally create intermediate commits that break the build or contracts.
- Do not split commits solely by file, directory, architecture layer, line count, or a target number of commits. One feature may require several files in one commit.
- Separate refactoring from behavior changes when both steps remain valid. Combine them if splitting creates a broken intermediate step.
- For changes across repositories, create commits in each repository and explain their dependencies.

Example: changes to settings persistence, gesture action mapping, and an independent navigation bug fix can form three commits. If the settings screen cannot build without its persistence model, include both in one commit or introduce a compatible model first.

## Complete and commit one purpose at a time

1. Implement one group of changes, including the adjustments needed for that step to work.
2. Run checks relevant to that group, following the project's commands and practices. For behavior changes, include meaningful tests when needed. Do not add tests that merely mirror the implementation or force tests for trivial changes.
3. Inspect the diff, then stage only the paths or hunks belonging to that purpose. Use explicit paths. Avoid blanket staging that can absorb unrelated work.
4. Inspect the entire index with `git diff --cached`, its summary, and `git diff --cached --check`. Ensure it contains no unrelated user changes, secrets, or generated files.
5. Create a local commit after required checks pass. Follow the repository's commit message style; if none exists, use `type(scope): concrete purpose`, such as `feat(settings): add gesture action mapping` or `fix(auth): reject inactive accounts`. Add the reason or limitations in the body when useful. Do not invent issue numbers or test results.
6. Verify that the commit succeeded, record its hash and contents, and check status before moving to the next purpose.

If changes are already mixed together, use hunk staging or a reviewed index patch. Do not discard or rewrite the working tree to separate them.

## Preserve the index and report verification accurately

- Preserve the user's initial changes and staging state. Do not include them through a plain `git commit`, unstage everything, or use stash as an automatic step.
- If the initial index contains work outside the scope, use an isolated temporary index or an authorized worktree only when the original changes and staging can be preserved correctly after committing. If that cannot be guaranteed, continue safe work and report the commit blocker.
- For commits assembled through partial staging, working tree tests may include code absent from the commit. Verify the commit snapshot in isolation when needed to establish that test results apply to that commit. State when the snapshot has not been tested.
- Fix failures caused by the task before committing. If required checks are blocked by the environment or pre-existing failures, report the cause and continue independent work; do not bypass required checks or claim they passed.
- Do not run destructive resets, discard changes, amend, rebase, squash, push, or modify Git hooks and configuration unless requested or already authorized. If a commit is incorrect, prefer a focused corrective commit.
- If a hook changes files, review those changes and rerun affected checks. If a hook rejects the commit, fix the cause without disabling the hook.

## Finish with traceable results

Complete all authorized purposes. Report each commit hash with a short description of its purpose, check results, and remaining changes. Explicitly state when a commit failed or testing covered only the working tree. Do not claim the working tree is clean while the user's work remains.
