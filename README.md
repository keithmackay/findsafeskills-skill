# findsafeskills-skill

A Claude Code skill that searches [findsafeskills](https://findsafeskills.com), a search engine for
coding-agent skills, plugins, plugin marketplaces and MCP servers with a safety rating on every
listing, directly from your agent, so you don't have to write one from scratch if something similar
already exists.

The skill tells your agent to report each result's safety rating and findings before suggesting it,
never to install a red-rated listing without your go-ahead, and to read a skill's files before
following it.

This skill only performs lookups against findsafeskills's own search API. It does not run any
static safety analysis itself; that's a separate, fully offline skill
([scanskillsafety-skill](https://github.com/keithmackay/scanskillsafety-skill)) that makes no
network calls back to findsafeskills.

## Installation

Install it for every project:

```bash
git clone https://github.com/keithmackay/findsafeskills-skill ~/.claude/skills/findsafeskills-search
```

For other agents, or to use findsafeskills's MCP server instead, see
[Connect your agent](https://findsafeskills.com/agent-setup).

## Usage

See `SKILL.md` for the full instructions Claude Code reads. In short: describe what you need in
plain language ("something that converts PDFs to markdown") and the skill queries findsafeskills's
search API and returns matching skills, plugins and MCP servers with their safety ratings.

## What it sends

Each search is one `GET` request to `https://findsafeskills.com/api/search` carrying your search text,
any filters, and `source=skill`. Nothing from your project, files or conversation is sent unless it
ends up in the search text your agent writes.

findsafeskills keeps the search text and filters, without any visitor identifier, to see which
searches find nothing. The skill keeps no cookies. As with every search, the IP address is recorded
for rate limiting and deleted after about two days, and the search text is sent to an embeddings
service to find matches. The full details are in the
[privacy policy](https://findsafeskills.com/privacy).

## License

MIT
