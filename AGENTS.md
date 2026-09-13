# 37signals Skills Repo

Publish target for the agent skills of 37signals products: Basecamp, HEY, and
Fizzy. Each product's CLI mirrors its `skills/` tree into `skills/` here on
release, via that CLI's `scripts/sync-skills.sh`. Nothing under `skills/` is
written by hand.

For installation, see [install.md](install.md).

## Sources

| Source | Skills | Publishes here |
|--------|--------|----------------|
| [basecamp-cli](https://github.com/basecamp/basecamp-cli/tree/main/skills) | `basecamp`, `basecamp-doctor` | On each stable release |
| [hey-cli](https://github.com/basecamp/hey-cli/tree/main/skills) | `hey` | On each stable release. Absent right now: see [#5](https://github.com/basecamp/skills/issues/5) |
| [fizzy-cli](https://github.com/basecamp/fizzy-cli/tree/master/skills) | `fizzy` | Not yet; a release sync is proposed in [fizzy-cli#214](https://github.com/basecamp/fizzy-cli/pull/214) |

## Key constraints

- **Do not edit skills here.** Edit them in the CLI repo that owns them
  (`basecamp-cli/skills/`, `hey-cli/skills/`, `fizzy-cli/skills/`) and let the
  next release publish them. Manual edits here are overwritten by that release.
- **Manifests are per source, and owned by the sync scripts.**
  `.managed-skills.basecamp-cli` and `.managed-skills.hey-cli` (and
  `.managed-skills.fizzy-cli` once Fizzy publishes) each list the skill
  directories that source's sync owns. A sync only ever deletes directories
  listed in its own file, so one product's release cannot remove another's
  skills. The legacy shared `.managed-skills` is kept as a comment-only
  tombstone so a CLI still running the old script deletes nothing. Don't edit
  any of these manually.
- **Safe to edit directly:** `README.md`, `AGENTS.md`, `install.md`, and
  `.claude-plugin/`. The sync only touches `skills/` and its own manifest.

## Repo structure

```
.claude-plugin/                  # Plugin manifest for marketplace install
skills/
  basecamp/SKILL.md              # Synced from basecamp-cli
  basecamp-doctor/SKILL.md       # Synced from basecamp-cli
  hey/SKILL.md                   # Synced from hey-cli (absent until its next release, see #5)
.managed-skills.basecamp-cli     # Skill directories owned by basecamp-cli's sync
.managed-skills.hey-cli          # Skill directories owned by hey-cli's sync
.managed-skills                  # Legacy shared manifest, comment-only tombstone
```

The per-source manifests and the tombstone appear with the first release of
each CLI after its sync fix ships; until then the legacy `.managed-skills` is
the only manifest present.
