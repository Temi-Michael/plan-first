# Challenge gate

Purpose: only feasible, safe ideas reach the plan.

## Process
1. **List everything to check:** every idea, feature and belief from the user's description, the interview and step 3.
2. **Sort each one** into a bucket (below). Before sorting a claim about a third-party API, a price or a law, check it with a web search. Don't guess.
3. **Show the results** to the user (see "Presenting"), then ask with AskUserQuestion: "Looks right" / "I disagree with one". An "Other" answer counts as "I disagree with one".
4. **If they disagree,** discuss that item:
   - A **risky** idea can stay only as an accepted risk. Use the consequence confirmation (see templates/claude-block.md), and log it in strategy.md.
   - An **infeasible** idea can't stay. Explain why, and offer the nearest feasible version.

## Buckets
| Bucket | Meaning |
|---|---|
| ✅ Feasible | Can be built within the budget, skill level and timeline, with no unmanaged security, legal or money risk |
| ⚠️ Risky | Can be built, but creates a security, privacy, legal or money risk. Always comes with a safe alternative |
| ❌ Infeasible / false assumption | Can't be done, can't be done within the budget or time, or rests on a wrong belief |

## Common cases
| Idea | Bucket | What to say or offer instead |
|---|---|---|
| Store card numbers | ⚠️ | A payment provider (such as Stripe) handles the cards |
| Store passwords yourself | ⚠️ | A sign-in provider, or a proven library that hashes passwords |
| Anyone can edit any record | ⚠️ | Owners edit their own records, and an admin role covers the rest |
| Collect data from children | ⚠️ | Legal rules apply (COPPA, GDPR). Add an age check, or drop it |
| Copy content or data from other sites | ⚠️ | Use an official API, and check its terms |
| "It will be 100% unhackable" | ❌ | No app is. The plan reduces risk, with checks after each milestone and before launch |
| "Free real-time data from X" | ❌ (often) | Search for whether an API exists and what it costs |
| Huge scale at launch on a $0 budget | ❌ | Plan for launch size, and design it so it can grow |
| Build your own payments, maps or AI model | ❌ (usually) | Use an existing provider |

## Presenting
**Beginner and intermediate:** a table with these columns:

| Idea | Verdict | Why (plain words) | What we'll do instead |
|---|---|---|---|

**Developer:** the same table, shorter, with the technical reason.

## Where each result goes
- **Feasible:** into the plan.
- **Risky, and the alternative is accepted:** the plan uses the alternative. Record the original idea in strategy.md under "Rejected ideas and why".
- **Risky, kept anyway:** record it in strategy.md under "Accepted risks", with the date.
- **Infeasible:** record it in strategy.md under "Rejected ideas and why".
