# Commit Commands

This Codex plugin mirrors the workflow intent of Claude Code's `commit-commands` plugin, but uses Codex skills instead of slash commands.

Available skills:

- `commit-commands:commit`
- `commit-commands:commit-push-pr`
- `commit-commands:clean-gone`

Suggested prompts:

- `Commit the relevant changes in this repo.`
- `Publish this work: create a branch if needed, commit, push, and open a draft PR.`
- `Clean up local branches whose upstreams are gone.`

Notes:

- Codex does not expose the same plugin-defined slash command surface as Claude Code, so these workflows are triggered by natural language or explicit skill invocation.
- The publish flow prefers structured GitHub tooling when available and falls back to `gh` where needed.
