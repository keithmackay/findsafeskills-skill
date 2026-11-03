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

## License

MIT
