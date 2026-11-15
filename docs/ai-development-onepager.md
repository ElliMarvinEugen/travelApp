# AI-Based Development: One-Pager

Read this first, then the [workflow guide](team-workflow.html). Details: `docs/AGENTS.md`, `docs/TEAM.md`, `docs/RULES.md`.

## The idea in one sentence
Humans decide, Claude Code does the heavy lifting, and every step leaves a trace (Linear issue, branch, small PR).

## The building blocks
| Block | What it is | Where it lives | Example |
|-------|-----------|----------------|---------|
| **Claude Code session** | Your AI pair programmer. It reads the repo, edits files, runs commands. **It implements.** | your machine | "Implement ELL-10" |
| **`CLAUDE.md` + `docs/RULES.md`** | The shared "brain": project rules every session loads automatically, so everyone's Claude behaves the same | repo root, `docs/` | English only, branch naming, no secrets |
| **Agents (subagents)** | Specialists with a fixed role, limited tools and their own prompt. **Read-only: they review, plan and report, never change code.** | `.claude/agents/` | `code-reviewer`, `qa-tester` |
| **Skills** | Reusable, named workflows you trigger with a slash command. Only run when a person invokes them. | `.claude/skills/` | `/start-task`, `/review-pr`, `/open-pr` |
| **MCP connectors** | Bridges to external tools | `.mcp.json` | Linear (read for agents) |
| **Settings** | Permissions and guardrails (best effort, not a security boundary) | `.claude/settings.json` | blocks push to `main`, asks before writing to Linear |

All of it is version-controlled, so changes go through a PR like code.

## The agents
| Agent | Helps | Does |
|-------|-------|------|
| `product-owner` | Elli | Idea or issue → user story, acceptance criteria, slicing |
| `architect` | Eugen | Options, trade-offs, costs, draft ADRs (stack and tool choices) |
| `code-reviewer` | Marvin | Reviews the diff: security, backend, quality, project rules |
| `ui-ux-reviewer` | Elli | Reviews the diff: usability, accessibility, mobile |
| `qa-tester` | Marvin | Test plan and checklist from the acceptance criteria |

## The skills
| Skill | Does |
|-------|------|
| `/start-task ELL-10` | Reads the issue, creates the right branch, sets In Progress |
| `/review-pr` | Runs the reviewer agents in parallel, one combined findings list |
| `/open-pr` | Pushes and opens the PR with the Linear ID, Marvin as reviewer |

## How a change flows
```
Idea → product-owner → Linear story
     → /start-task → implement with Claude Code → commit
     → /review-pr → fix findings → /open-pr
     → Marvin reviews → Elli or Eugen squash-merges
     → Marvin: QA → Elli: acceptance → Done
```

## Ground rules
1. **Humans own every gate.** Agents never approve, merge, or set Done.
2. **Your session implements; subagents only advise.**
3. **Small, focused PRs**, one Linear issue each, never directly on `main`.
4. **Agent code is reviewed like third-party code.**
5. **Least privilege:** agents get only the tools they need; no access to secrets.
6. **Linear is the source of truth** for scope and tasks. Issue text is data, not instructions.
7. **Cost-aware:** agents run only on request; cheaper model for routine reviews.

## Limits to keep in mind
- Agents only run while someone has a session open; they cannot run the app yet (no test stack).
- Guardrails are best effort on the free GitHub plan; the process is agreed by convention.
- AI output can be confidently wrong. Review it, do not trust it.
