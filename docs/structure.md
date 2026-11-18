# Structure

## Stack
- **Platform:** Claude Code skills, written in Markdown with YAML frontmatter.
- **Subagent:** a Claude Code agent file with tools limited to `Read, Grep, Glob`. It has no Bash, Edit or Write, so it truly can't change files or run commands. The `/secure-check` skill runs the scanners itself and passes the results to it.
- **Permissions:** no commands are pre-approved, so every scanner, install or test command shows the user a permission prompt. `/plan-first` removes Bash with `disallowed-tools`. Claude Code only applies that for the turn that starts the skill, so the skill's "no commands" rule covers the rest.
- **Secret detection:** gitleaks when it's installed. Otherwise a list of patterns for known key formats (`skills/plan-first/secret-patterns.md`, copied in the agent file).
- **Scanners**, run by the `/secure-check` skill (not the subagent) and optional:
  - `npm audit` / `pip-audit` for dependencies
  - `gitleaks` for secrets
  - `semgrep` for insecure code patterns
- **Claude Code features used:** web search (stack research, OWASP guidance), and the built-in question box with clickable choices (confirmations).
- **Distribution:** a Claude Code plugin. The project folder is the plugin root. Once installed, the commands are namespaced: `/safe-build:plan-first` and `/safe-build:secure-check`.

## Folders
```
skills/                          # plugin root
├── README.md                    # public page: what it is, install, use
├── .claude-plugin/
│   ├── plugin.json              # plugin manifest (name, version, description)
│   └── marketplace.json         # lets others install it: safe-build@safe-build
├── skills/                      # folder name = command name
│   ├── plan-first/
│   │   ├── SKILL.md             # triggers, comfort-level modes, flow, hard rules
│   │   ├── interview.md         # topic list, follow-up rules, by mode
│   │   ├── challenge.md         # challenge-gate rules
│   │   ├── secret-patterns.md   # known secret formats (for the self-check)
│   │   └── templates/           # README, strategy, structure, implementation, claude-block
│   └── secure-check/
│       ├── SKILL.md             # flow, logging rules, report format
│       └── templates/           # issues, fix, updates
├── agents/
│   └── security-reviewer.md     # subagent (Read, Grep, Glob only): checklist, secret patterns, report format
└── docs/                        # this project's own plan (not loaded by Claude Code)
    └── README.md, strategy.md, structure.md, implementation.md
```

**Layout rules**
- Skill folders have no `-skill` suffix, because the folder name becomes the command name.
- Subagents only register from `agents/`, so the reviewer can't live inside a skill folder.
- The checklist is part of the agent file, because the subagent can't reliably find files inside a skill folder.

## Files written into the user's project
| File | Written by | Contents |
|---|---|---|
| `README.md` | /plan-first | Vision, mission, audience |
| `strategy.md` | /plan-first | Decisions, scope, non-goals, risks, assumptions, rejected ideas, Later list, accepted risks, comfort level |
| `structure.md` | /plan-first | Stack (chosen and rejected, with reasons), folders, data model, architecture |
| `implementation.md` | /plan-first | Ordered steps with acceptance checks, a `/secure-check` step after each milestone, and a required final full-app `/secure-check` before launch |
| `CLAUDE.md` block | /plan-first | Marked rules: re-read the plan files, no code before approval, the scope guard, the `/secure-check` reminder, the limits notice |
| `issues.md` | /secure-check | Findings: severity, location, status |
| `fix.md` | /secure-check | Patch, root cause, the test that proves the fix |
| `updates.md` | /secure-check, scope guard | What was built and checked, and the changes made |

## Architecture
```
/plan-first ─► calibrate ─► discover ─► think beyond ─► research ─► challenge gate ─► confirm ─► generate ─► stop
                                                                                                    │
                                                         4 plan files + CLAUDE.md block ◄───────────┘
                                                                    │
                                              AI builds (re-reads the plan, scope guard)
                                                                    │
/secure-check ─► check plan exists ─► read plan ─► security-reviewer (read-only) ─► findings
            └─► main agent: failing test ─► patch ─► issues.md / fix.md / updates.md ─► report + limits notice
```
