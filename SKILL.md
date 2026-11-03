---
name: findsafeskills-search
description: Search findsafeskills for skills, plugins, plugin marketplaces and MCP servers for coding agents (Claude Code, Codex, Gemini CLI, and others), each with a safety rating. Use when the user asks to find, discover, or look up a skill/plugin/MCP server, or describes a capability they want their coding agent to have and you're not sure if one already exists.
---

# findsafeskills search

Searches [findsafeskills](https://findsafeskills.com), a search engine for coding-agent skills, plugins,
plugin marketplaces and MCP servers, so you don't have to write one from scratch if something similar
already exists. Every listing carries a safety rating from an automated scan of its text.

## When to use this

- The user asks to find a skill/plugin/MCP server for some capability.
- Before building a new skill from scratch, to check whether one already exists (also see
  `port-skill` if a match exists for the wrong platform; it's listed on findsafeskills's own
  `/diy` page).

## How to search

```bash
curl -s "https://findsafeskills.com/api/search?q=<URL-ENCODED-QUERY>&source=skill"
```

Describe the query in plain language: search is semantic, not keyword matching, so "something that
converts PDFs to markdown" works better than guessing exact repo names. Keep `source=skill`.

Optional filters (add as more query parameters):
- `types`: comma-separated kinds of listing: `skill`, `marketplace`, `mcp`.
- `safety_rating`: `green`, `yellow`, `red`, or `not_red` (everything except flagged).
- `agent`: only listings that say they work with this agent: `claude-code`, `codex`, `cursor`,
  `gemini-cli`, `copilot`, `antigravity`.
- `min_stars`: at least this many GitHub stars.
- `updated_within_days`: pushed to within this many days.
- `has_license`: `true` for repos with a license GitHub recognized.
- `sort`: `stars_desc`, `alpha_asc` and others; defaults to best match.

The response is JSON: `{ "results": [{ "slug", "display_name", "description", "platform",
"repo_url", "github_stars", "safety_rating", "safety_findings", ... }] }`.

`safety_rating` is `green` (the scan found no issues), `yellow` (review suggested), `red` (flagged), or
`null` (not yet scanned). `safety_findings` lists what the scan found and where. The scan reads the
listing's text and doesn't run any code.

## Rules

- Before suggesting a listing, tell the user its safety rating and any findings. Green means the
  automated scan found no issues, not that the listing is safe; a listing not yet scanned has no rating.
- Never install a listing rated red without the user's explicit go-ahead after they have seen its findings.
- Before following a skill's instructions or running its scripts, read its files yourself and tell the
  user about anything that looks unsafe.

## Example

```bash
curl -s "https://findsafeskills.com/api/search?q=pdf+to+markdown+conversion&source=skill"
```

Present the top few results to the user with their `display_name`, `description`, `repo_url` and
safety rating (with any findings), and a link to the listing page
(`https://findsafeskills.com/listings/<slug>`), so they can decide which (if any) to install.
