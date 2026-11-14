# Agents and Skills

Owner: Eugen (Agent Conductor). Everything here lives in `.claude/` and is version-controlled, so every team member's Claude Code uses the same agents and skills. Agents follow `CLAUDE.md` and `docs/RULES.md` like humans do.

## Principles
- **Your own session implements.** Nobody delegates the actual coding to a subagent. The session needs the full conversation and the person's judgment.
- **Subagents are read-only specialists.** They review, plan and report. They never change code, approve, merge or set a Linear status.
- **Humans decide at every gate.** Agents prepare the decision.
- **Least privilege.** Each agent only gets the tools it needs. Linear access is read-only. `.claude/settings.json` adds deny rules on top (best effort, not a security boundary).
- **One findings format** (`docs/RULES.md`, section 6) for all reviewers.
- **Cost:** agents run only on request, with a cheaper model (`sonnet`, `haiku` for the QA planner).

## Agents (`.claude/agents/`)
| Agent | For | Job | Tools | Model |
|-------|-----|-----|-------|-------|
| `product-owner` | Elli | Idea or issue into a story with acceptance criteria, slicing, open questions | read, Linear read | sonnet |
| `code-reviewer` | Marvin | Branch diff: security, backend, user data, dependencies, tests, project rules | read, read-only git, Linear read | sonnet |
| `ui-ux-reviewer` | Elli | Branch diff: usability, states, consistency, accessibility, mobile. Says "No UI changes" when there are none | read, read-only git, Linear read | sonnet |
| `qa-tester` | Marvin | Test plan and manual checklist from the acceptance criteria, gaps in coverage | read, Linear read | haiku |

Later, when needed: an architect/planner agent, a database reviewer once the stack is decided, a docs keeper. Claude Code's built-in Plan agent covers planning for now.

## Skills (`.claude/skills/`)
| Skill | What it does | Who runs it |
|-------|--------------|-------------|
| `/start-task ELL-10` | Reads the issue, checks for a clean tree, updates `main`, creates the correctly named branch, sets the issue to In Progress | the person starting the work |
| `/review-pr` | Runs the reviewer agents in parallel on the current branch and combines the findings into one list | the author before opening a PR, or Marvin when reviewing |
| `/open-pr` | Pushes the branch and opens the PR from the template with the Linear ID in the title and Marvin as reviewer | the author |

`/start-task` and `/open-pr` have side effects, so they only run when a person invokes them. `/review-pr` only reads.

## How a task flows through them
```
Elli:    idea → product-owner agent → story in Linear (Ready/Todo)
Anyone:  /start-task ELL-10 → implement with your Claude Code → commit
Author:  /review-pr → fix findings → /open-pr
Marvin:  reviews the PR (/review-pr on the branch if useful)
Elli or Eugen (not the author): approve and squash merge
Marvin:  QA with qa-tester's checklist → Elli: final acceptance, Done
```

## Invoking agents directly
Ask your Claude Code in plain words, naming the agent:
- "Use the product-owner agent to refine this idea into a story: friends should be able to split costs on a trip."
- "Run the code-reviewer agent on this branch and summarize the findings."
- "Use the qa-tester agent to write a test plan for ELL-10."

## Expected output
- Reviewers: findings by severity, each with `file:line`, what is wrong, why it matters and a concrete fix, or an explicit "No findings".
- `product-owner`: story, acceptance criteria, open questions, size estimate.
- `qa-tester`: test cases per criterion (given, when, then), a manual checklist, and gaps.

## Known limitations
- Agents only run while a person has a Claude Code session open. They do not watch Linear or GitHub on their own.
- Reviewers read code and cannot run the app. Findings are a second pair of eyes, not a replacement for human review.
- No test stack exists yet, so `qa-tester` plans tests but does not run them.
- Deny rules in `.claude/settings.json` help, but they are not a security boundary. The free GitHub plan cannot enforce branch protection (see `docs/TEAM.md`).
- Linear tool names depend on the project's `.mcp.json` server name `linear-server`. Use that setup, not a second connector.

## Changing agents and skills
Changes to `.claude/` go through a PR like any other change. Eugen owns this area; Marvin reviews permissions.
