# Installation

## As a plugin (recommended)

```bash
/install-plugin github:basecamp/skills
```

This installs all skills and keeps them updated.

## Manual installation

### Personal (all projects)

```bash
git clone https://github.com/basecamp/skills ~/.basecamp-skills

# Symlink individual skills
ln -s ~/.basecamp-skills/skills/basecamp ~/.claude/skills/basecamp

# Or all at once
for skill in ~/.basecamp-skills/skills/*/; do
  ln -s "$skill" ~/.claude/skills/"$(basename "$skill")"
done
```

### Per-project

```bash
# From your project root
ln -s ~/.basecamp-skills/skills/basecamp .claude/skills/basecamp
```

### Updating

```bash
cd ~/.basecamp-skills && git pull
```

Symlinks pick up changes immediately. If you copied instead of symlinking,
re-copy after pulling.

## Prerequisites

The **basecamp** skill requires the [Basecamp CLI](https://github.com/basecamp/basecamp-cli):

```bash
brew install basecamp/tap/basecamp
basecamp auth login
```
