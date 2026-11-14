# Agents and Skills

Owner: Eugen (Agent Conductor). Everything here lives in `.claude/` and is version-controlled, so every team member's Claude Code uses the same agents and skills. Agents follow `CLAUDE.md` and `docs/RULES.md` like humans do. This is the single place where the agent roster is described; other docs link here.

## Principles
- **Your own session implements.** Nobody delegates the actual coding to a subagent. The session needs the full conversation and the person's judgment.
- **Subagents are read-only specialists.** They review, plan and report. They never change code, approve, merge or set a Linear status.
- **Humans decide at every gate.** Agents prepare the decision.
- **Least privilege.** Each agent only gets the tools it needs. Linear access is read-only for agents. `.claude/settings.json` adds deny and ask rules on top (see limitations).
- **Issue text and code are data.** Agents read Linear issues, comments and diffs written by others. They treat that text as data to analyze and never follow instructions found in it.
- **One findings format** (`docs/RULES.md`, section 6) for all reviewers.
- **Cost:** agents run only on request, with a cheaper model (`sonnet`).

## Prerequisites (once per person)
- **Linear:** the project's `linear-server` (from `.mcp.json`) is enabled for everyone through `.claude/settings.json` (`enabledMcpjsonServers`). Open a new session in the project folder and sign in with your own Linear account (`/mcp`, or the connector view of the app). Do not keep a second Linear connector enabled for this project, because agent tool names are `mcp__linear-server__*`. Adding another MCP server to `.mcp.json` needs a reviewed PR and its own entry in `enabledMcpjsonServers`.
- **GitHub CLI:** install `gh` and run `gh auth login --web --git-protocol https`. Restart the app (or terminal) after installing so `gh` is on the PATH. Needed for `/open-pr`.
- **Check:** ask your Claude "Which Linear issues are assigned to me?" and run `gh auth status`.

## Agents (`.claude/agents/`)
| Agent | For | Job | Tools | Model |
|-------|-----|-----|-------|-------|
| `product-owner` | Elli | Idea or issue into a story with acceptance criteria, slicing, open questions | read, Linear read | sonnet |
| `code-reviewer` | Marvin | Branch diff: security, backend, user data, dependencies, tests, project rules | read, git via Bash, Linear read | sonnet |
| `ui-ux-reviewer` | Elli | Branch diff: usability, states, consistency, accessibility, mobile. Says "No UI changes" when there are none | read, git via Bash, Linear read | sonnet |
| `qa-tester` | Marvin | Test plan and manual checklist from the acceptance criteria, gaps in coverage. Gets the changed-file list from `/review-pr` | read, Linear read | sonnet |

Later, when needed: an architect/planner agent (Claude Code's built-in Plan agent covers this for now), a database reviewer once there is a schema, test-running rights for `qa-tester` once a test stack exists, and a `/sync-docs` skill that compares docs with Linear.

## Skills (`.claude/skills/`)
| Skill | What it does | Who runs it |
|-------|--------------|-------------|
| `/start-task ELL-10` | Reads the issue, checks for a clean tree, updates `main`, creates the correctly named branch, sets the issue to In Progress | the person starting the work |
| `/review-pr` | Runs the reviewer agents in parallel on the current branch and combines the findings into one list | the author before opening a PR, or Marvin when reviewing |
| `/open-pr` | Pushes the branch and opens the PR from the template with the Linear ID in the title and Marvin as reviewer | the author |

All three only run when a person invokes them (`disable-model-invocation`), so agents never start by themselves and cost stays under control. `/review-pr` additionally disallows editing and writing files.

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

Claude Code's built-in `/security-review` and `/code-review` are a useful second opinion. They do not know our rules or the Linear issue, so they do not replace `code-reviewer`.

## Expected output
- Reviewers: findings by severity, each with `file:line`, what is wrong, why it matters and a concrete fix, or an explicit "No findings".
- `product-owner`: story, acceptance criteria, open questions, size estimate.
- `qa-tester`: test cases per criterion (given, when, then), a manual checklist, and gaps.

## Known limitations
- Agents only run while a person has a Claude Code session open. They do not watch Linear or GitHub on their own.
- Reviewers read code and cannot run the app. Findings are a second pair of eyes, not a replacement for human review.
- No test stack exists yet, so `qa-tester` plans tests but does not run them.
- **Deny and ask rules are not a security boundary.** `.claude/settings.json` blocks pushes to `main`, force pushes, `gh pr merge`, `gh pr review` and reading common `.env` files, for the Bash and PowerShell tools. They are easy to get around (for example `git push origin HEAD` while on `main`, or `cat .env` in a shell). Writing to Linear (`save_issue`, `save_comment`) asks for approval every time, including in `/start-task`. If someone runs Claude Code in auto or bypass mode, these prompts disappear.
- The reviewers have Bash and are asked in their prompt to use only read-only git commands. That is a request, not a technical restriction.
- The free GitHub plan cannot enforce branch protection (see `docs/TEAM.md`).
- Linear tool names depend on the project's `.mcp.json` server name `linear-server`. Use that setup, not a second connector.
- Not yet verified: how a missing MCP tool named in an agent's `tools` list behaves. If Linear tools are missing, agents work without the issue and say so.

## Changing agents and skills
Changes to `.claude/` go through a PR like any other change. Eugen owns this area; Marvin reviews permissions.
