# findsafeskills-skill

A Claude Code skill that searches [findsafeskills](https://skillfinder-neon.vercel.app) — a
semantic search engine for coding-agent skills, plugin marketplaces, and MCP servers — directly
from your agent, so you don't have to write one from scratch if something similar already
exists.

This skill only performs lookups against findsafeskills's own search API. It does not run any
static safety analysis itself — that's a separate, fully offline skill (zero network calls back
to findsafeskills) maintained alongside the main findsafeskills project.

## Installation

Copy `SKILL.md` into your Claude Code skills directory (or install via your usual skill
distribution method).

## Usage

See `SKILL.md` for the full instructions Claude Code reads. In short: describe what you need in
plain language ("something that converts PDFs to markdown") and the skill queries
findsafeskills's semantic search API and returns matching skills/plugins/MCP servers.

## License

MIT
