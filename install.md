I want you to install Agent Skills for Basecamp for me. Execute all steps autonomously.

OBJECTIVE: Install Basecamp agent skills so your agent can manage projects, todos, cards, messages, schedule, campfire, and more via the Basecamp CLI.

DONE WHEN: `basecamp --version && basecamp auth status` both succeed and the basecamp skill is installed in your agent.

## TODO

- [ ] Install Basecamp CLI
- [ ] Authenticate with Basecamp
- [ ] Install skills

## Step 0: Install Basecamp CLI

Check if the Basecamp CLI is already installed:

```bash
basecamp --version
```

If `basecamp` is not installed, install it. See the [Basecamp CLI install guide](https://github.com/basecamp/basecamp-cli/blob/main/install.md) for full options, or use Homebrew:

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

## Step 2: Install skills

```bash
npx skills add basecamp/skills
```

This installs skills from this repo into your agent using the [Agent Skills](https://agentskills.io) open standard. The installer auto-detects your agent and places skills in the correct directory. It supports Claude Code, Cursor, Codex, VS Code, Gemini CLI, Goose, Amp, OpenCode, and others.

To install for a specific agent:

```bash
npx skills add basecamp/skills -a claude-code
```

To install globally (available across all projects):

```bash
npx skills add basecamp/skills -g
```

**Verify:**
```bash
npx skills list
# Expected: basecamp skill listed
```

Restart your agent session to pick up the new skills. The basecamp skill provides full CLI coverage: projects, todos, cards, messages, files, schedule, check-ins, timeline, recordings, templates, webhooks, subscriptions, lineup, and campfire.

EXECUTE NOW: Start with Step 0. Mark TODO items complete as you go. Stop when `basecamp --version && basecamp auth status` both succeed and the basecamp skill is installed.

---

## Optional: Manual installation

**Do not execute this section unless explicitly requested.**

Clone this repo and symlink skills into your agent's skill directory manually:

```bash
git clone https://github.com/basecamp/skills ~/.basecamp-skills
mkdir -p ~/.claude/skills
for skill in ~/.basecamp-skills/skills/*/; do
  ln -sfn "$skill" ~/.claude/skills/"$(basename "$skill")"
done
```

For per-project installation:

```bash
mkdir -p .claude/skills
ln -sfn ~/.basecamp-skills/skills/basecamp .claude/skills/basecamp
```

Update with `cd ~/.basecamp-skills && git pull`. Symlinks pick up changes immediately.
