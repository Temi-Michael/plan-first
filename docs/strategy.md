# Strategy

## Key decisions and why
| Decision | Why |
|---|---|
| Build as Claude Code **skills**, not an MCP server | An interview and file generation need only markdown instructions. MCP is for connecting outside tools or data. |
| **Two commands** (`/plan-first`, `/secure-check`) | Each stays focused, so it triggers reliably. `implementation.md` reminds users to run the second one. |
| The skills share information **through files**, not direct calls | The plan files act as lasting memory and keep the vision in context. |
| Ask for **comfort level** first (new / know some / developer), changeable at any time | Stops beginners being overloaded and developers being slowed down. |
| Beginners decide *what* they want; Claude decides *how* and explains why | Beginners can't make good technical choices ("SQL or NoSQL?"). |
| Questions are **generated from a fixed list of topics** | The list guarantees coverage; generating the wording keeps the interview natural. |
| A **challenge gate** runs before any file is written | Risky or infeasible ideas never reach the plan. |
| Security review runs in a **read-only subagent** | Fresh eyes on the code, a clean main conversation, and enforced separation (it only reports; the main agent patches). |
| Use **existing free scanners** and write fixes at the time a flaw is found | Fixes depend on the actual code, so they can't be pre-written. |
| **Append** to CLAUDE.md and never overwrite it | Protects the user's existing rules. |
| Ask breaking-change confirmations with a **clickable choice that states the consequence** | Deliberate but convenient. Tab auto-fill was rejected (see below). |
| Plugin name **safe-build** | Short and describes the purpose. Commands are `/safe-build:plan-first` and `/safe-build:secure-check`. |
| **Least privilege:** the reviewer gets only Read, Grep and Glob; the skill runs the scanners; nothing is pre-approved | Tool limits are enforced by Claude Code, not just requested in instructions. The user sees and approves every command. |
| **Safe scanner commands only:** no fix modes; skip pip-audit when packages aren't pinned; skip npm audit with no lock file; gitleaks always runs with `--redact` | Scanning must never install or run project code, and must never print secret values. |
| **Secret detection:** gitleaks first, with a list of known key formats as a fallback | Patterns catch known formats only, so gitleaks (hundreds of rules plus randomness checks) is preferred. |
| A **required final check before launch**, in addition to the milestone checks | Catches problems that only appear late or once everything is connected: secrets added after the last check, newly announced flaws in packages, live server settings. The skill can't block a launch, so "required" means the plan says "don't launch until high-severity issues are fixed", and the limits notice repeats it. |

## Scope
**Interview topics `/plan-first` must cover:** problem, users, data, logins, payments, scale, hosting, budget, success, never-do.

**What `/plan-first` also does:**
- Researches the stack on the web, against the user's real constraints.
- Thinks beyond the user: edge cases, user types, legal issues, 10 vs. 10,000 users.
- Has a change mode for updating an existing plan.

**`/secure-check`:**
- Scanners: `npm audit` / `pip-audit`, `gitleaks`, `semgrep`, with a pattern-search fallback.
- Checks the plan's own rules.
- Writes a failing test before each patch.
- Reports in the user's comfort level, with a coverage footer.

**Both skills:**
- A scope guard on every change.
- A project-specific limits notice.

## Non-goals
- Writing application code during planning.
- Guaranteeing security, or replacing pentests, DAST or compliance audits.
- Legal advice.
- Shipping pre-written security fixes.

## Rules
**Challenge gate.** Every user idea goes into one bucket:
- **Feasible:** goes into the plan.
- **Risky:** explained plainly, with a safe alternative.
- **Infeasible / false assumption:** said honestly.

The user confirms. Rejected ideas are logged in the project's strategy.md.

**Follow-ups.** Only when an answer is vague, contradictory, risky or missing, with about 2 per topic at most. If the user says "I don't know", Claude proposes a default and records it as an assumption.

**Project description.** `/plan-first <details>` treats the details as the user's first answers. The interview and challenge gate still always run.

**Scope guard.** Every change is compared with the 4 plan files.
- **Small changes** touch none of these: data model, logins or permissions, payments, new packages or services, how a feature behaves.
  - They get a one-line note that references the plan, and are logged.
  - If one grows partway through, stop and switch to the full explanation.
- **All other changes:**
  1. Clarify vague requests with concrete options tied to the project.
  2. Explain what users get, what changes, cost, privacy needs, a simpler alternative, and where it fits.
  3. Sort it, then act:
     - **In scope:** confirm, build, log in updates.md.
     - **New but safe:** add now, add later, use the alternative, or save to the Later list.
     - **Breaking:** explain what could break. Accept with the consequence choice, update via `/plan-first`, defer, or cancel. Accepted risks are recorded with the date.
     - **Previously rejected:** remind why. Go ahead only with a new reason.

**Limits notice.** Shown at the end of `/plan-first`, on every `/secure-check` report, and in the CLAUDE.md block.
- **Beginner version:** what it does, what it can't do, risks for this app specifically (data stored, laws, payments or login), and what to still do (run `/secure-check`, get a developer review before real users, keep backups).
- **Developer version:** what is covered and what isn't (logic flaws beyond the plan's rules, DAST, infrastructure, supply chain, compliance), and the highest-risk areas in this project.
- **`/secure-check` footer:** a Check | How | Result table, including fallbacks and anything not checked, ending with "No findings means these checks passed, not that the app is secure."

## Risks
- Skills may not trigger reliably. Mitigation: write the skill descriptions carefully.
- Long sessions drift from the plan. Mitigation: the CLAUDE.md rule to re-read the plan files.
- Scanners may be missing or blocked. Mitigation: offer to install them, fall back to pattern search, and say so in the report.
- Users may skip `/secure-check`. Mitigation: milestone steps in implementation.md.
- The scope guard may feel tiring. Mitigation: the small-change exception.

## Rejected ideas and why
- **MCP server:** not needed, because there are no outside tools or data to connect.
- **One command for everything:** too long, and the security phase triggers unreliably late in a session.
- **Asking for job title instead of comfort level:** many people are somewhere in between.
- **Tab auto-fill for confirmations:** Claude Code's suggested messages can't be controlled by a skill and can be turned off.
- **A plain "Yes" confirmation:** gets clicked without reading.
- **Pre-written security fixes, or downloading a ready-made "security agent":** fixes depend on the actual code.

## Open decisions
None.
