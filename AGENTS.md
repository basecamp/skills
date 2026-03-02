# Basecamp Skills Repo

Distribution repo for Basecamp skills for Claude Code. Skills are auto-synced
from [basecamp/basecamp-cli](https://github.com/basecamp/basecamp-cli) on each
release by `scripts/sync-skills.sh`.

For installation, see [install.md](install.md).

## Key constraints

- **Do not edit skills here.** Edit in `basecamp-cli/skills/` and let the sync
  publish them. Manual edits will be overwritten on the next release.
- `.managed-skills` tracks which skill directories are owned by the sync script.
  Don't edit it manually.
- Non-skill files (README, AGENTS.md, install.md, .claude-plugin/) are safe to
  edit directly — the sync only touches `skills/` and `.managed-skills`.

## Repo structure

```
.claude-plugin/        # Plugin manifest for marketplace install
skills/
  basecamp/SKILL.md    # Synced from basecamp-cli
.managed-skills        # Auto-generated manifest
```
