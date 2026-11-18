# Privacy policy

**Effective:** 2026-11-18

Safe Build is a Claude Code plugin made of instruction files. It has no servers, no accounts, no analytics and no tracking. The author never receives any of your data.

## What the plugin does with your information
- **Your conversation and code** are processed by Claude, inside your own Claude Code, Cowork or Claude app session, exactly as they would be without the plugin. That processing is covered by [Anthropic's privacy policy](https://www.anthropic.com/legal/privacy), not this one.
- **Files it writes** stay in your project folder: the plan (`README.md`, `strategy.md`, `structure.md`, `implementation.md`), a rules section in `CLAUDE.md`, and the security logs (`issues.md`, `fix.md`, `updates.md`). They're never uploaded anywhere by the plugin. If you push your project to a public repository, these files become public too.
- **Secrets:** the plugin is instructed never to write passwords, API keys or tokens into any file, and to show at most the first 4 characters of any secret it finds.

## Outside services it may use
These only run on your computer, through your own Claude Code session, and Claude Code asks your permission before each command.

| Service | When | What's sent |
|---|---|---|
| Web search (part of Claude Code) | `/plan-first`, to compare tools and prices | Technical search terms only, such as "free Postgres hosting pricing". The plugin is instructed never to include your personal details or secrets in searches. |
| npm or pnpm registry | `/secure-check`, if your project has a lock file | Package names and versions, to check for known flaws |
| PyPI vulnerability data | `/secure-check`, if your Python packages have exact versions | Package names and versions |
| Semgrep rule registry | `/secure-check`, if semgrep is installed | A request to download rules. Your code isn't uploaded, and Semgrep's usage metrics are turned off. |
| gitleaks | `/secure-check`, if installed | Nothing. It runs entirely on your computer. |

Scanners are installed only if you agree, using their official install commands.

## Removing the plugin
Uninstalling removes the plugin's instructions. Files it wrote in your projects stay until you delete them.

## Changes and contact
Changes to this policy are published in this file, with a new effective date. Questions: open an issue at [github.com/Temi-Michael/plan-first/issues](https://github.com/Temi-Michael/plan-first/issues).
