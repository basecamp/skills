I want you to install Agent Skills for 37signals products for me. Execute all steps autonomously.

OBJECTIVE: Install the Basecamp, HEY, and Fizzy agent skills from basecamp/skills, plus the CLI behind each product you use, so your agent can work in Basecamp (required) and HEY and Fizzy (optional).

DONE WHEN: `basecamp --version && basecamp auth status && (for cli in hey fizzy; do ! command -v "$cli" >/dev/null || "$cli" auth status || exit 1; done)` succeeds and `npx skills list` shows the basecamp skill.

## TODO

- [ ] Install Basecamp CLI
- [ ] Authenticate with Basecamp
- [ ] Install and sign in to HEY CLI (only if you use HEY)
- [ ] Install and sign in to Fizzy CLI (only if you use Fizzy)
- [ ] Install skills

## Step 0: Install Basecamp CLI

The basecamp skills need the Basecamp CLI. Skip the install if `basecamp --version` already succeeds. See the [Basecamp CLI install guide](https://github.com/basecamp/basecamp-cli/blob/main/install.md) for other install methods.

```bash
curl -fsSL https://basecamp.com/install-cli | bash
```

**Verify:**
```bash
basecamp --version
# Expected: basecamp version X.Y.Z
```

## Step 1: Authenticate with Basecamp

Skip if `basecamp auth status` already reports authenticated (the installer runs setup on an interactive terminal). Otherwise this opens a browser for OAuth; grant access when prompted. Credentials are stored in the system keychain.

```bash
basecamp auth login
```

**Verify:**
```bash
basecamp auth status
# Expected: JSON with "authenticated": true
```

## Step 2: Install and sign in to HEY CLI

Only if you use HEY; otherwise mark this TODO done and continue. Skip the install if `hey version` already succeeds. See the [HEY CLI install guide](https://github.com/basecamp/hey-cli/blob/main/docs/install.md) for other install methods. Sign-in opens a browser.

```bash
curl -fsSL https://hey.com/install-cli | bash && hey auth login
```

**Verify:**
```bash
hey version && hey auth status
# Expected: a version line, then a signed-in status
```

## Step 3: Install and sign in to Fizzy CLI

Only if you use Fizzy; otherwise mark this TODO done and continue. Skip the install if `fizzy --version` already succeeds. See the [Fizzy CLI README](https://github.com/basecamp/fizzy-cli#quick-start) for other install methods. `fizzy setup` asks for a personal access token and an account.

```bash
curl -fsSL https://raw.githubusercontent.com/basecamp/fizzy-cli/master/scripts/install.sh | bash && fizzy setup
```

**Verify:**
```bash
fizzy --version && fizzy auth status
# Expected: fizzy version X.Y.Z, then JSON with "authenticated": true
```

## Step 4: Install skills

Installs every skill in this repo into your agent using the [Agent Skills](https://agentskills.io) open standard. The installer auto-detects your agent (Claude Code, Cursor, Codex, VS Code, Gemini CLI, Goose, Amp, OpenCode, and others) and places skills in the right directory. Add `-a claude-code` to target one agent, or `-g` to install globally.

```bash
npx skills add basecamp/skills
```

**Verify:**
```bash
npx skills list
# Expected: basecamp and basecamp-doctor listed (hey too, once it is published here)
```

Restart your agent session to pick up the new skills.

EXECUTE NOW: Start with Step 0. Mark TODO items complete as you go. Stop when `basecamp --version && basecamp auth status && (for cli in hey fizzy; do ! command -v "$cli" >/dev/null || "$cli" auth status || exit 1; done)` succeeds and `npx skills list` shows the basecamp skill.

---

## Optional: HEY and Fizzy skills from the CLI

**Do not execute this section unless explicitly requested.**

The hey skill is temporarily missing from this repo, and the fizzy skill is not published here yet (see the [README](README.md)). Each CLI can install its own skill directly:

```bash
hey skill install
fizzy skill install
```

## Optional: Homebrew installs

**Do not execute this section unless explicitly requested.**

```bash
brew install --cask basecamp/tap/basecamp-cli
brew install --cask basecamp/tap/hey
brew install --cask basecamp/tap/fizzy
```

## Optional: Manual installation

**Do not execute this section unless explicitly requested.**

Clone this repo and symlink skills into your agent's skill directory manually:

```bash
git clone https://github.com/basecamp/skills ~/.37signals-skills
mkdir -p ~/.claude/skills
for skill in ~/.37signals-skills/skills/*/; do
  ln -sfn "$skill" ~/.claude/skills/"$(basename "$skill")"
done
```

For per-project installation:

```bash
mkdir -p .claude/skills
ln -sfn ~/.37signals-skills/skills/basecamp .claude/skills/basecamp
```

Update with `cd ~/.37signals-skills && git pull`. Symlinks pick up changes immediately.
