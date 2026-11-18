<!-- safe-build:plan:start -->
# Implementation

> **In plain words:** {{the build order, and what's built first}}
<!-- Keep the summary above for beginner and intermediate users. Delete it for developers. -->

Build one step at a time. Each step's check must pass before moving to the next.

## Milestone 1: {{name}}
1. {{step}}
   - ✅ Check: {{how we know it works}}
2. {{step}}
   - ✅ Check: {{how we know it works}}
- 🔒 **Security check:** run `/safe-build:secure-check`.

<!-- Repeat the milestone block for each milestone. Every milestone ends with the security check. -->

## Before launch (required)
- 🔒 Run `/safe-build:secure-check` on the full app. **Don't launch until all high-severity issues are fixed.**
- Set up backups for the app's data.
- {{If it handles personal data or payments: have an experienced developer review it, especially logins and payments.}}

## Change log
- {{date}}: Plan created.
<!-- safe-build:plan:end -->
