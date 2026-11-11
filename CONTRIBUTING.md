# Contributing

Thanks for helping. Open an issue first for anything larger than a small fix.

## Build and test

The plugin is plain ES modules (Node 18 or newer) with no build step, no
dependencies and no automated tests. To check a change, point a Clawdbot
instance at your checkout and a running MemOS server, then call `memory_save`,
`memory_search` and `memory_get` and confirm the results.

## Rules

- Keep `README.md`, `clawdbot.plugin.json` and `package.json` consistent when you
  change a config key, a tool argument or the plugin id.
- Do not add dependencies without a reason; the plugin uses the built-in `fetch`.

## Commits and pull requests

Use Conventional Commits (`feat:`, `fix:`, `docs:`, `chore:`). Describe what you
changed and how you tried it; the pull request template lists the checks.
