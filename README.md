# Agent Skills for Basecamp

Skills that extend [Claude Code](https://docs.anthropic.com/en/docs/claude-code)
with Basecamp project management capabilities — todos, cards, messages,
schedule, campfire, and more.

## Quick start

```
/install-plugin github:basecamp/skills
```

Or see [INSTALL.md](INSTALL.md) for manual installation.

## Available skills

| Skill | Description |
|-------|-------------|
| [basecamp](skills/basecamp/SKILL.md) | Full Basecamp CLI integration — 130 endpoints across todos, cards, messages, files, schedule, check-ins, timeline, recordings, templates, webhooks, subscriptions, lineup, and campfire. |

## Requires

- [Basecamp CLI](https://github.com/basecamp/basecamp-cli) (`brew install basecamp/tap/basecamp`)
- An authenticated Basecamp account (`basecamp auth login`)

## About

These skills are automatically published from
[basecamp/basecamp-cli](https://github.com/basecamp/basecamp-cli) on each
release. To contribute, open issues or PRs there.
