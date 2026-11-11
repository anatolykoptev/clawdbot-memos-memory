# clawdbot-memos-memory — notes for coding agents

Index of every document: [docs/INDEX.md](docs/INDEX.md).

## What this is

A Clawdbot memory plugin backed by a MemOS server. `index.js` registers three
tools (`memory_search`, `memory_save`, `memory_get`) and reads the plugin
config; `api.js` is the thin REST client for the MemOS endpoints
`/product/search`, `/product/add`, `/product/get_all` and `/product/delete_memory`.
`clawdbot.plugin.json` holds the plugin id (`memos-memory`), kind and config
schema.

## Gate

There is no CI, build step or test suite. Check a change against a running MemOS
server by installing the plugin in Clawdbot and exercising the three tools.

## Invariants easy to break

- The plugin id `memos-memory` must stay identical in `clawdbot.plugin.json`,
  the README configuration example and `package.json` (`name`).
- Config precedence is plugin config, then the `MEMOS_API_URL` and
  `MEMOS_USER_ID` environment variables, then the built-in defaults, in
  `register()` in `index.js`.
- `formatSearchResults` maps MemOS `text_mem`, `pref_mem` and `act_mem` cubes to
  the Clawdbot `memory_search` result shape; a change to the MemOS response shape
  breaks it silently, because errors are returned as `fallback: true` results,
  not thrown.
- The `topK` config value is parsed but not used by search; the tool's
  `maxResults` argument decides the count.
