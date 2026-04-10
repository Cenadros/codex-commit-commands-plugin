# Codex Commit Commands

This repository packages a reusable Codex plugin that mirrors the workflow intent of Claude Code's `commit-commands` plugin, but uses Codex skills instead of slash commands.

Included workflows:

- commit scoped changes with a repo-style message
- create a branch if needed, commit, push, and open a draft PR
- clean up local branches whose upstreams are gone

## Repository Layout

- `plugins/commit-commands`
- `.agents/plugins/marketplace.json`

## Install Options

### Repo-local install

Copy `plugins/commit-commands` into the target repository under `plugins/commit-commands`, then add the marketplace entry from `.agents/plugins/marketplace.json` into the target repository's `.agents/plugins/marketplace.json`.

### Home-local install

Copy `plugins/commit-commands` to `~/plugins/commit-commands` and add this entry to `~/.agents/plugins/marketplace.json`:

```json
{
  "name": "commit-commands",
  "source": {
    "source": "local",
    "path": "./plugins/commit-commands"
  },
  "policy": {
    "installation": "AVAILABLE",
    "authentication": "ON_INSTALL"
  },
  "category": "Productivity"
}
```

## Usage

Codex does not expose the same plugin-defined slash command surface as Claude Code, so use natural language or explicit skill invocation.

Examples:

- `Commit the relevant changes in this repo.`
- `Publish this work: create a branch if needed, commit, push, and open a draft PR.`
- `Clean up local branches whose upstreams are gone.`
