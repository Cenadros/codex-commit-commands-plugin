---
name: "commit-push-pr"
description: "Create a branch if needed, commit scoped changes, push to origin, and open a draft pull request."
---

# Commit, Push, PR Workflow

Use this skill when the user wants the equivalent of Claude Code's `/commit-push-pr`.

## Goal

Take local work from working tree to remote draft PR with minimal context switching and without hiding scope decisions.

## Prerequisites

- `git` must be available.
- `gh` should be installed and authenticated when CLI fallback is needed.
- The repository must have a usable `origin` remote.

## Workflow

1. Confirm scope.
   - Run `git status -sb` and inspect the diff.
   - If the worktree contains unrelated changes, ask the user which files belong in the PR.
2. Choose branch strategy.
   - If the current branch is `main`, `master`, or the repo default branch, create a new branch named `codex/<description>`.
   - Otherwise stay on the current branch.
3. Stage the intended files only.
4. Review recent commit style with `git log --oneline -n 10`.
5. Create a terse, accurate commit.
6. Run the most relevant checks that are practical in the repo.
   - If no clear automated check exists, say so.
7. Push with tracking.
   - Use `git push -u origin <branch>`.
8. Open a draft PR.
   - Prefer structured GitHub tooling when the repository and head branch can be resolved cleanly.
   - Fall back to `gh pr create --draft` when needed.
9. Summarize the result.
   - Include branch name, commit SHA, validation run, and PR URL.

## Safety

- Do not push unrelated user changes.
- Default to a draft PR unless the user explicitly asks for ready-for-review.
- If `gh` is missing or unauthenticated and a fallback is required, stop and explain the blocker.
