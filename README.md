# safe-build

A Claude Code plugin that makes the AI plan with you before it builds anything, then keeps the build on-plan and checks it for security problems.

| Command | What it does |
|---|---|
| `/safe-build:plan-first [your idea]` | Asks you simple questions about what you want to build, points out risky or impossible ideas, and writes a plan (`README.md`, `strategy.md`, `structure.md`, `implementation.md`) plus rules in `CLAUDE.md` that the AI follows while building. It writes no app code. |
| `/safe-build:secure-check [full]` | Checks the code built so far for security problems, fixes them with your approval, and logs everything in `issues.md`, `fix.md` and `updates.md`. Run it after each milestone, and with `full` before launch. |

## Requirements
- **Claude Code**, signed in. Check by running `claude` in a terminal. If it says "Not logged in", run `claude` and then `/login`.
- **Optional scanners** for `/secure-check`: gitleaks (leaked keys), semgrep (unsafe code patterns), pip-audit (Python packages). `npm audit` comes with Node.js. If any are missing, `/secure-check` asks before installing them and works without them, with a less thorough check. To install them yourself on a Mac:
  ```bash
  brew install gitleaks semgrep pipx && pipx install pip-audit
  ```

## Install

### Option A: install from GitHub (recommended)
Run these two commands in a terminal, not inside Claude Code.

```bash
claude plugin marketplace add Temi-Michael/plan-first
```

```bash
claude plugin install safe-build@safe-build
```

The first command registers the repository as a plugin source. The second installs the plugin from it (`safe-build` plugin `@` `safe-build` source). It's installed for your user account, so it works in every project.

Inside a Claude Code session you can do the same with `/plugin marketplace add Temi-Michael/plan-first` and then `/plugin install safe-build@safe-build`.

### Option B: install from a folder on your computer
If you've downloaded or cloned this folder, use its path instead:

```bash
claude plugin marketplace add /path/to/this/folder
```

```bash
claude plugin install safe-build@safe-build
```

### Option C: try it without installing
This loads the plugin for one session only:

```bash
claude --plugin-dir /path/to/this/folder
```

### Check it worked
```bash
claude plugin list
```

`safe-build@safe-build` should show `Status: ✔ enabled`. In a Claude Code session, type `/safe-build:` and both commands should appear.

## Use it
1. Open your project folder in Claude Code. It can be empty.
2. Run `/safe-build:plan-first`, optionally followed by your idea, for example `/safe-build:plan-first a booking app for my hair salon`.
3. Answer the questions. You can say "explain simpler" or "skip the basics" at any time. Approve the plan when it looks right.
4. Ask Claude to start building. It follows `implementation.md` one step at a time.
5. When a milestone is done, run `/safe-build:secure-check`.
6. Before you launch, run `/safe-build:secure-check full`, and don't launch until every high-severity issue is fixed.

## Update or remove
```bash
claude plugin update safe-build@safe-build
```

```bash
claude plugin uninstall safe-build@safe-build
```

Restart Claude Code after updating. Removing the plugin doesn't delete the plan or log files it wrote in your projects.

## Your data and outside services
The plugin has no servers and collects nothing. It reads your project files and your answers inside your own Claude session, and writes its plan and log files only into your project. It's instructed never to write secrets or real people's personal details into those files.

These outside services may be contacted from your computer, each only after you approve the command:

| Service | Used by | What's sent |
|---|---|---|
| Web search (built into Claude Code) | `/plan-first`, to compare tools and prices | Technical search terms only, never your personal details or secrets |
| npm or pnpm registry | `/secure-check` (`npm audit` / `pnpm audit`) | Package names and versions from your lock file |
| PyPI vulnerability data | `/secure-check` (`pip-audit`) | Package names and versions |
| Semgrep rule registry | `/secure-check` (`semgrep`) | A request to download rules. Your code isn't uploaded, and usage metrics are off. |

gitleaks runs entirely on your computer and sends nothing. Full details: [PRIVACY.md](PRIVACY.md).

## What it can't do
- It guides the AI and catches common problems, but it can't guarantee your app is secure, and it doesn't attack your running app the way a real attacker would.
- Plan and log files are ordinary files in your project. If your repository is public, so are they. They never contain secret values.
- Get a human developer to review the app before it handles real users' data or payments.

## For contributors
The design and build plan for this plugin are in [docs/](docs/README.md). Check your changes with:

```bash
claude plugin validate .
```
