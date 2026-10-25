# Agent Skills for 37signals products

[Agent skills](https://agentskills.io) for Basecamp, HEY, and Fizzy. Each skill
teaches a coding agent to work in one product through that product's CLI.

```
npx skills add basecamp/skills
```

That installs every skill in `skills/`. See [install.md](install.md) for the
full setup, including installing and authenticating each CLI.

## Skills

| Skill | Product | Published from | Description |
|-------|---------|----------------|-------------|
| [basecamp](skills/basecamp/SKILL.md) | Basecamp | [basecamp-cli](https://github.com/basecamp/basecamp-cli/tree/main/skills/basecamp) | Interact with Basecamp via the Basecamp CLI. Full API coverage: projects, todos, cards, messages, files, schedule, check-ins, timeline, recordings, templates, webhooks, subscriptions, lineup, chat, pings, gauges, assignments, notifications, bookmarks, bubble-up, drafts, notes, calendars, and accounts. |
| [basecamp-doctor](skills/basecamp-doctor/SKILL.md) | Basecamp | [basecamp-cli](https://github.com/basecamp/basecamp-cli/tree/main/skills/basecamp-doctor) | Diagnose Basecamp CLI, authentication, and agent-plugin health. |
| [hey](skills/hey/SKILL.md) | HEY | [hey-cli](https://github.com/basecamp/hey-cli/tree/main/skills/hey) | Interact with HEY via the HEY CLI. Read and send email; manage contacts, boxes, labels, collections, calendars, todos, habits, time tracking, and journal entries. |
| fizzy | Fizzy | [fizzy-cli](https://github.com/basecamp/fizzy-cli/tree/master/skills/fizzy) | Interact with Fizzy via the Fizzy CLI. Manage boards, cards, columns, comments, steps, reactions, tags, users, notifications, pins, webhooks, and account settings. **Not published here yet** (see below). |

**fizzy** is not published here yet: fizzy-cli's release sync landed in
[fizzy-cli#214](https://github.com/basecamp/fizzy-cli/pull/214), and the skill
arrives with the first fizzy-cli release after it. Until then, get it from
[fizzy-cli/skills/fizzy](https://github.com/basecamp/fizzy-cli/tree/master/skills/fizzy),
or run `fizzy skill install`.

## Requirements

Each skill drives its product's CLI, so install and authenticate the CLI for
the products you use. One is enough; the skills for the others sit idle.

**Basecamp** — [basecamp-cli](https://github.com/basecamp/basecamp-cli)
([install guide](https://github.com/basecamp/basecamp-cli/blob/main/install.md))

```bash
curl -fsSL https://basecamp.com/install-cli | bash   # or: brew install --cask basecamp/tap/basecamp-cli
basecamp auth login
```

**HEY** — [hey-cli](https://github.com/basecamp/hey-cli)
([install guide](https://github.com/basecamp/hey-cli/blob/main/docs/install.md))

```bash
curl -fsSL https://hey.com/install-cli | bash   # or: brew install --cask basecamp/tap/hey
hey auth login
```

**Fizzy** — [fizzy-cli](https://github.com/basecamp/fizzy-cli)
([install guide](https://github.com/basecamp/fizzy-cli#quick-start))

```bash
curl -fsSL https://raw.githubusercontent.com/basecamp/fizzy-cli/master/scripts/install.sh | bash   # or: brew install --cask basecamp/tap/fizzy
fizzy setup   # personal access token, account, default board
```

## Contributing

Skills are never edited in this repo; a change made here is overwritten by the
next release of the CLI that owns it. Open issues and pull requests against the
skill's source instead:

- Basecamp: [basecamp-cli/skills](https://github.com/basecamp/basecamp-cli/tree/main/skills)
- HEY: [hey-cli/skills](https://github.com/basecamp/hey-cli/tree/main/skills)
- Fizzy: [fizzy-cli/skills](https://github.com/basecamp/fizzy-cli/tree/master/skills)

Issues about this repo itself (the README, install.md, the plugin manifest, or
the publishing) belong here.

## About

This repo is a publish target. On each release, a CLI's `scripts/sync-skills.sh`
copies its `skills/` tree into `skills/` here, records the directories it owns
in a manifest, and commits straight to `main`. Only the README, install.md,
AGENTS.md, and `.claude-plugin/` are written by hand.
