# Secret patterns

Use these with the Grep tool (ripgrep syntax) to spot secrets in text you're about to write, or have written.

**What they catch:** well-known key formats.

**What they miss:** secrets with no recognisable format, and secrets with no label next to them.

**False positives:** placeholders like `your-api-key-here` match too. Treat a match as "check this", not as proof.

| Secret | Pattern |
|---|---|
| AWS access key | `\b(AKIA\|ASIA)[A-Z0-9]{16}\b` |
| GitHub token | `\b(gh[pousr]_[A-Za-z0-9]{36,}\|github_pat_[A-Za-z0-9_]{22,})` |
| Stripe live key | `\b[rs]k_live_[A-Za-z0-9]{20,}` |
| Slack token | `\bxox[abprs]-[A-Za-z0-9-]{10,}` |
| Google API key | `\bAIza[0-9A-Za-z_-]{35}\b` |
| Anthropic key | `\bsk-ant-[A-Za-z0-9_-]{20,}` |
| OpenAI-style key | `\bsk-(proj-)?[A-Za-z0-9_-]{20,}` |
| Private key | `-----BEGIN [A-Z ]*PRIVATE KEY-----` |
| JWT | `\beyJ[A-Za-z0-9_-]{10,}\.[A-Za-z0-9_-]{10,}\.[A-Za-z0-9_-]{10,}` |
| URL with a password | `[a-z][a-z0-9+.-]*://[^\s:/@]+:[^\s@/]+@` |
| Labelled secret | `(?i)(api[_-]?key\|secret\|token\|passw(or)?d\|pwd)\s*[:=]\s*["'][^"'\s]{8,}["']` |

The `\|` in the table means a plain `|` in the actual pattern.

This list is copied in `agents/security-reviewer.md`. If you change one, change both.
