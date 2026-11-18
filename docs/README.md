# Plan-First & Secure-Check

A planning-and-safety layer for Claude Code. It's two skills plus a read-only security subagent.

## Vision
Anyone, including people who have never coded, can build software with an AI tool that understands exactly what to build, why, and what to avoid. The result is apps that are well planned and safer.

## Mission
- Before code is written: interview the user, challenge infeasible or risky ideas, and produce an approved plan the AI must follow.
- During the build: keep the AI on-plan, explain every change, and run security reviews that log, test and patch flaws.

## Audience
- **Primary:** non-developers who build with AI coding tools.
- **Secondary:** intermediate users and developers who want structured planning and security checks.

## What it includes
| Part | Command | What it does |
|---|---|---|
| Planning skill | `/plan-first [project details]` | Interviews the user, runs the challenge gate, and writes `README.md`, `strategy.md`, `structure.md`, `implementation.md` plus a CLAUDE.md rules block |
| Security skill | `/secure-check` | Audits the code against the plan and writes `issues.md`, `fix.md`, `updates.md` |
| Security subagent | used by `/secure-check` | Audits read-only and reports findings without editing anything |

## Limits
These skills guide the AI coding tool and reduce risk. They don't write the app, and they don't guarantee it is secure. A human review is still advised before handling real users' data or payments.

## Status
Milestones 1 and 2 are written and pass `claude plugin validate`, but haven't been run live yet. Milestone 3 has started: `.claude-plugin/marketplace.json` and the install instructions in the [root README](../README.md) are done; a fresh install from GitHub is still to be tested. See [implementation.md](implementation.md).
