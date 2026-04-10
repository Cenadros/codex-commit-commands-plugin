---
name: "commit"
description: "Review local git changes, stage only the intended scope, draft a repo-style commit message, and create a commit."
---

# Commit Workflow

Use this skill when the user wants the equivalent of Claude Code's `/commit`.

## Goal

Turn a set of local changes into one intentional git commit without silently sweeping in unrelated files.

## Workflow

1. Inspect the current worktree.
   - Run `git status -sb`.
   - Review staged and unstaged diffs before deciding what belongs in scope.
2. Determine scope.
   - If the worktree is mixed and the user has not made scope clear, stop and ask which files belong in the commit.
   - Do not default to `git add -A` when unrelated user edits are present.
3. Review recent commit style.
   - Inspect a handful of recent commits with `git log --oneline -n 10`.
   - Match the repository's existing style unless the user asks for a specific format.
4. Stage only the intended files.
   - Prefer explicit paths.
   - Never stage `.env`, credentials files, or obviously secret-bearing artifacts unless the user explicitly asks.
5. Draft the message.
   - Keep it terse and accurate.
   - Prefer imperative mood.
   - Use conventional commit prefixes only if the repository already does or the user asked for them.
6. Create the commit.
   - Use a normal non-empty commit.
7. Summarize the result.
   - Report the branch, commit SHA, and committed scope.

## Safety

- Never commit unrelated user changes silently.
- Never rewrite or amend existing commits unless the user explicitly asks.
- If there is nothing to commit, say so plainly instead of forcing an empty commit.
