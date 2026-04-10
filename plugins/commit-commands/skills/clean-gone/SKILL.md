---
name: "clean-gone"
description: "Prune remote tracking refs, detect local branches whose upstream is gone, remove related worktrees, and delete the stale branches."
---

# Clean Gone Branches

Use this skill when the user wants the equivalent of Claude Code's `/clean_gone`.

## Goal

Clean up local branches that track remote branches which have already been deleted.

## Workflow

1. Refresh remote state.
   - Run `git fetch --prune`.
2. Identify candidate branches.
   - Use `git branch -vv` to find local branches marked as gone.
3. Inspect worktrees.
   - If a gone branch is checked out in a linked worktree, remove the worktree before deleting the branch.
4. Delete stale branches.
   - Prefer `git branch -d <branch>`.
   - Use force deletion only if the user explicitly asks or if deletion is otherwise blocked and they approve the tradeoff.
5. Report the result.
   - List what was removed and what, if anything, was skipped.

## Safety

- Never delete the current branch.
- Never remove a worktree or branch that is not in gone state.
- If no gone branches exist, report that nothing needed cleanup.
