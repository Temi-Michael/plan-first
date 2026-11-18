# Implementation

Build in this order. Each step has a check that must pass before moving on.
Test locally by starting Claude Code with `claude --plugin-dir <this folder>`.

## Milestone 1: /plan-first
1. **skills/plan-first/SKILL.md**: the description that triggers the skill (a draft is in place), the comfort-level modes, the 8-step flow, and the hard rules (no app code, always run the interview and challenge gate).
   - ✅ Check: typing `/safe-build:plan-first`, or "help me plan an app", triggers it.
2. **interview.md**: the topic list, problem-first questions, follow-up rules, and the "I don't know" defaults.
   - ✅ Check: a beginner gets plain, 3-question rounds, and every topic gets covered.
   - **research.md**: tool type first, at least 3 sourced candidates, a comparison at every level, recommendation plus runner-up.
   - ✅ Check: "free and easy database" shows a dated comparison (for example Supabase, Neon, Firebase) with a runner-up. A note-taking app with offline mobile sync gets a document database considered.
3. **challenge.md**: the rules for the three buckets, and how results are logged to "Rejected ideas".
   - ✅ Check: "store card numbers" and "100% unhackable" are caught, and each gets a safe alternative or an honest explanation.
4. **templates/**: the 4 plan files and the CLAUDE.md block.
   - ✅ Check: running the skill on a sample project produces all 4 files. The CLAUDE.md block is appended once and existing content is kept. `implementation.md` has a `/secure-check` step after each milestone and ends with the required pre-launch check: "Before launch: run `/safe-build:secure-check` on the full app. Don't launch until all high-severity issues are fixed."
5. **Change mode and scope guard**, written into the CLAUDE.md block.
   - ✅ Check: a small change gets a one-line note; "add notifications" gets the clarify-and-explain flow; a breaking change shows the consequence choice.
6. **Review milestone 1** against strategy.md, and check the limits notice names project-specific risks.

## Milestone 2: /secure-check
7. **agents/security-reviewer.md**: tools limited to Read, Grep and Glob, the read-only rules, the checklist (secrets, injection, auth and access control, dependencies, input validation, error handling, the plan's own rules), and the finding format.
   - ✅ Check: it makes no file changes, and each finding includes severity, file and line, a fix, and a confidence level.
8. **skills/secure-check/SKILL.md**: checks the plan exists, detects scanners (offering installs or falling back to pattern search), calls the reviewer, then failing test → patch → log, then the report and coverage footer.
   - ✅ Check: with no plan files, it sends the user to `/plan-first`. On a sample app with a planted secret and a missing auth check, both are found, tested, patched and logged.
9. **templates/**: issues, fix, updates.
10. **Review milestone 2**, including both comfort-level report styles and the footer.

## Milestone 3: Release
11. Add `.claude-plugin/marketplace.json` so others can install the plugin, and write install instructions in README.md.
    - ✅ Check: a fresh install works in a new project.
