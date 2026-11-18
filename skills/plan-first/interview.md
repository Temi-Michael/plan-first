# Interview guide

## How the questions are made
- **What must be covered is fixed.** The 11 topics below are always covered, so nothing important is missed.
- **How each question is worded is generated.** You write each question from the user's earlier answers and comfort level, so it fits their project and never feels like a form.
- **Only ask what matters.** Skip a topic, or part of one, when earlier answers already settle it. For example, if there are no payments, don't ask about refunds. Record skipped topics as "not applicable".

## Question rules
Every question must pass all of these:
1. **One thing per question.** Never two questions joined with "and" or "or".
2. **Short.** At most 20 words for beginners.
3. **Everyday words.** If a technical term can't be avoided, explain it in brackets in 8 words or fewer.
4. **Easy to answer.**
   - When the likely answers are predictable, give 2–4 choices with AskUserQuestion.
   - For beginners, always include a "Not sure" choice, which leads to a default (see below).
   - Use open questions only for things only the user knows: the problem, the users, the idea itself.
5. **Explain only when needed.** Add one short "why I'm asking" sentence only when the reason isn't obvious.
6. **About the user's world, not the technology.** Ask beginners what should happen, never how to build it.

| ❌ Too complicated | ✅ Better |
|---|---|
| "What authentication strategy and authorization model do you need?" | "Should each person only see their own bookings?" (Yes / No, some people see everything / Not sure) |
| "What are your scalability and hosting requirements?" | "Roughly how many people will use it in the first year?" (Under 100 / 100–1,000 / Over 1,000 / Not sure) |
| "Describe your users, their goals, and pain points." | "Who will use it most?" |

## Rounds
- **Round size:** beginner 3 questions on one theme; intermediate 4–5; developer open-ended. One AskUserQuestion call can hold up to 4 choice questions.
- **Order:** problem, users and must-haves first; hosting and budget last.
- **After each round, play back "So far" in 1–2 sentences.** For example: "So far: an online booking page for your salon, so customers stop calling to book." This helps the user see their idea taking shape, and correct it early.

## Topics
| # | Topic | What to find out | Beginner example |
|---|---|---|---|
| 1 | Problem | Who has it, how they cope today, what it costs them, how they know it's real | "Who has this problem today?" |
| 2 | Users | Types (customer, staff, admin), how many, how comfortable they are with tech, what devices they use | "Who will use it most?" |
| 3 | Past attempts | What has been tried or seen fail, and why someone would switch | "Have you tried anything else for this?" |
| 4 | Must-haves | The smallest version that solves the problem, vs. nice-to-haves | "If it could only do 3 things on day one, what would they be?" |
| 5 | Data | What's stored, how sensitive it is (personal, health, children, financial), who can see what | "What information will people type into it?" |
| 6 | Logins and permissions | Who logs in, and who can see or edit what | "Should each person only see their own things?" |
| 7 | Payments | Who pays whom, one-off or subscription, refunds | "Will anyone pay money through it?" |
| 8 | Scale | Users at launch and after one year | "Roughly how many people in the first year?" |
| 9 | Hosting and budget | Monthly budget, where it runs, existing accounts or tools | "How much can you spend each month to keep it running?" |
| 10 | Success | The single outcome that means it worked, and the target date | "How will you know it's working?" |
| 11 | Never-do | Things the app must never do | "Is there anything it must never do?" |

Keep a coverage list: for each topic, record the answer, an assumption, or "not applicable". Don't move to step 3 until every topic has one.

## Follow-ups
After each round, check every answer for these four problems:
- **Vague** ("lots of users", "make it fast"): ask for a number or an example, offering choices.
- **Contradictory** (for example: free, no ads, and no hosting budget): point out the conflict in one sentence, and ask which matters more.
- **Risky:** note it for the challenge gate. You can ask one clarifying question.
- **Missing:** ask for it.

Ask **at most 2 follow-ups per topic**. After that, record your best understanding as an assumption.

## "Not sure" or "I don't know"
1. Propose a sensible default and explain it in one line.
2. Record it in strategy.md under Assumptions, as: `Assumed: <default>. You can change this.`

For example, if the user doesn't know how many users to expect: assume up to 500 in the first year. Cheap hosting handles that, and upgrading later is easy.

## Before moving on
Show the coverage list:
- **Beginner:** one line, such as "We've covered everything I need. Next, a few things you may not have thought of."
- **Developer:** a compact list, topic → answer.
