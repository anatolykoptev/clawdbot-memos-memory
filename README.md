# Clawdbot MemOS Memory Plugin

A [Clawdbot](https://github.com/clawdbot/clawdbot) plugin that replaces the default memory system with [MemOS](https://github.com/MemTensor/MemOS) — a semantic memory operating system with persistent storage and vector search.

## Features

- 🧠 **Semantic Search** — Find memories by meaning, not just keywords
- 💾 **Persistent Storage** — PostgreSQL + pgvector backend
- 🔄 **Auto-indexing** — Memories are embedded and indexed by the MemOS server on save
- 🎯 **Preference Tracking** — Searches also return the user's stored preferences

## Installation

```bash
clawdbot plugins install github:anatolykoptev/clawdbot-memos-memory
```

## Configuration

Add to your `clawdbot.json`:

```json
{
  "plugins": {
    "slots": {
      "memory": "memos-memory"
    },
    "entries": {
      "memos-memory": {
        "enabled": true,
        "config": {
          "apiUrl": "http://memos-api:8000",
          "userId": "default",
          "topK": 10
        }
      }
    }
  }
}
```

## Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `MEMOS_API_URL` | MemOS API endpoint; used when `apiUrl` is not set in the plugin config | `http://memos-api:8000` |
| `MEMOS_USER_ID` | Default user ID; used when `userId` is not set in the plugin config | `default` |

The plugin config also accepts `topK`, but searches currently take their result
count from the tool's `maxResults` argument (default 10), not from `topK`.

## Tools

The plugin provides three tools:

### `memory_search`
Semantic search across stored text, preference and action memories. Arguments: `query` (required), `maxResults` (default 10), `minScore`.

```
Query: "What are my preferences for coffee?"
```

### `memory_save`
Save important information to persistent memory.

```
Content: "User prefers dark roast coffee in the morning"
```

### `memory_get`
Retrieve the user's text memories, optionally narrowed by a `filter` substring.

## Development

There is no build step, test suite or CI. The plugin is plain ES modules
(`index.js`, `api.js`, Node 18 or newer) that talk to the MemOS REST API
(`/product/search`, `/product/add`, `/product/get_all`, `/product/delete_memory`).
See [CONTRIBUTING.md](CONTRIBUTING.md) and [docs/INDEX.md](docs/INDEX.md).

## Status

Version 1.0.1, not published to npm; install from GitHub.

## Requirements

- MemOS API server running and accessible
- PostgreSQL with pgvector extension
- Embedding service (for vector generation)

## License

MIT, see [LICENSE](LICENSE).
