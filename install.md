I want you to install Agent Skills for Basecamp for me. Execute all steps autonomously.

OBJECTIVE: Install Basecamp agent skills so your agent can manage projects, todos, cards, messages, schedule, campfire, and more via the Basecamp CLI.

DONE WHEN: `basecamp --version && ls ~/.claude/skills/basecamp/SKILL.md` both succeed (or equivalent skill path for your agent).

## TODO

- [ ] Install Basecamp CLI
- [ ] Authenticate with Basecamp
- [ ] Clone skills repo
- [ ] Symlink skills into agent

## Step 0: Install Basecamp CLI

Check if the Basecamp CLI is already installed:

```bash
basecamp --version
```

If `basecamp` is not installed, install it. See the [Basecamp CLI install guide](https://github.com/basecamp/basecamp-cli/blob/main/INSTALL.md) for full options, or use Homebrew:

```bash
brew install --cask basecamp/tap/basecamp
```

If `basecamp: command not found` after install, add to PATH:

```bash
export PATH="$HOME/.local/bin:$PATH"
```

**Verify:**
```bash
basecamp --version
# Expected: basecamp version X.Y.Z
```

## Step 1: Authenticate with Basecamp

```bash
basecamp auth login
```

This opens a browser for OAuth. Grant access when prompted. The CLI stores credentials securely in the system keychain.

**Verify:**
```bash
basecamp auth status
# Expected: Authenticated (scope: read)
```

## Step 2: Clone skills repo

```bash
git clone https://github.com/basecamp/skills ~/.basecamp-skills
```

If already cloned, pull latest:

```bash
cd ~/.basecamp-skills && git pull
```

**Verify:**
```bash
ls ~/.basecamp-skills/skills/basecamp/SKILL.md
# Expected: /Users/you/.basecamp-skills/skills/basecamp/SKILL.md
```

## Step 3: Symlink skills into agent

Create the agent skills directory and symlink each skill:

```bash
mkdir -p ~/.claude/skills
for skill in ~/.basecamp-skills/skills/*/; do
  ln -sfn "$skill" ~/.claude/skills/"$(basename "$skill")"
done
```

For agents other than Claude Code, symlink or copy skill directories from `~/.basecamp-skills/skills/` into your agent's skill discovery path. Skills follow the [Agent Skills](https://agentskills.io) open format and work with any compatible agent.

**Verify:**
```bash
ls ~/.claude/skills/basecamp/SKILL.md
# Expected: /Users/you/.claude/skills/basecamp/SKILL.md
```

Restart your agent session to pick up the new skills. The basecamp skill provides full CLI coverage: projects, todos, cards, messages, files, schedule, check-ins, timeline, recordings, templates, webhooks, subscriptions, lineup, and campfire.

EXECUTE NOW: Start with Step 0. Mark TODO items complete as you go. Stop when `basecamp --version && ls ~/.claude/skills/basecamp/SKILL.md` both succeed.

---

## Optional: Per-project installation

**Do not execute this section unless explicitly requested.**

To scope skills to a single project instead of installing globally:

```bash
mkdir -p .claude/skills
ln -sfn ~/.basecamp-skills/skills/basecamp .claude/skills/basecamp
```

## Optional: Claude Code plugin install

```bash
/plugin marketplace add basecamp/skills
/plugin install basecamp-skills@basecamp-skills
```

## Optional: Updating

```bash
cd ~/.basecamp-skills && git pull
```

Symlinks pick up changes immediately. No re-install needed.
