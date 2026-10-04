---
name: findsafeskills-search
description: Search findsafeskills for skills, plugins, and MCP servers for coding agents (Claude Code, Codex, Gemini CLI, and others). Use when the user asks to find, discover, or look up a skill/plugin/MCP server, or describes a capability they want their coding agent to have and you're not sure if one already exists.
---

# findsafeskills search

Searches [findsafeskills](https://skillfinder-neon.vercel.app), a semantic search engine for
coding-agent skills, plugin marketplaces, and MCP servers, so you don't have to write one from
scratch if something similar already exists.

## When to use this

- The user asks to find a skill/plugin/MCP server for some capability.
- Before building a new skill from scratch, to check whether one already exists (also see
  `port-skill` if a match exists for the wrong platform — it's listed on findsafeskills's own
  `/diy` page).

## How to search

```bash
curl -s "https://skillfinder-neon.vercel.app/api/search?q=<URL-ENCODED-QUERY>&source=skill"
```

Optional filters (add as additional query params):
- `platform` — one of `claude-code-skill`, `claude-code-marketplace`, `codex-skill`,
  `gemini-cli-skill`, `agent-skill`, `marketplace`, `mcp-server`.
- `category` — free-text category filter.

The response is JSON: `{ "results": [{ "slug", "display_name", "description", "platform",
"repo_url", "github_stars", ... }] }`. Describe the query in plain language — search is semantic
(vector similarity), not keyword matching, so "something that converts PDFs to markdown" works
better than guessing exact repo names.

## Example

```bash
curl -s "https://skillfinder-neon.vercel.app/api/search?q=pdf+to+markdown+conversion&source=skill"
```

Present the top few results to the user with their `display_name`, `description`, and
`repo_url` so they can decide which (if any) to install.
