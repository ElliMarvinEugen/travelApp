# Team & Roles

We are three people. Each role has clear decision authority. Agents (Claude Code) work on behalf of these roles and do not replace them.

**Source of truth:** the Linear project [Travel Planner App](https://linear.app/elli-huynh/project/travel-planner-app-226f2629a820) is leading for product vision, MVP scope, milestones, Definition of Done and task ownership. The tech stack there is only an idea until the team decides (see `docs/TOOLS.md`). Project-wide rules live in `docs/RULES.md`. This repo only documents how we work in code. If something here conflicts with Linear, Linear wins and this file gets fixed.

| Person | GitHub | Role | Decides on |
|--------|--------|------|------------|
| **Elli** | [@elliHuynh](https://github.com/elliHuynh) | Product Owner & Lead Dev | What gets built (backlog, priorities, acceptance criteria) and how it is implemented technically (code structure) |
| **Marvin** | [@marvinvec](https://github.com/marvinvec) | Security & Quality Manager | Whether something is release-ready (security review, test strategy, quality gates, dependencies, secrets) |
| **Eugen** | [@ekutschkin-priv](https://github.com/ekutschkin-priv) | **Agent Conductor** (Architect for Agents; "AI & Agent Engineer" in Linear) | How we work with agents (agent definitions, prompts, tooling, guardrails, system architecture) |

> "Conductor": Eugen conducts the orchestra of humans and agents. The name is a proposal and easy to change (alternatives: Agent Whisperer, Maestro, Orchestrator).

## Responsibilities

### Elli, Product Owner & Lead Dev
- Maintains the backlog (Linear) and writes/prioritizes user stories.
- Defines acceptance criteria and gives the final acceptance of a finished feature (after Marvin's QA).
- Leads the team: sets the direction and takes the lead when we sync.
- Has the final say on everyday code architecture.
- Can approve and merge pull requests.
- Uses agents: `product-owner` (refine stories) and `ui-ux-reviewer`, plus Claude Code for implementation.

### Marvin, Security & Quality Manager
- Reviews pull requests for security and quality (see quality gates below).
- Owns the test strategy, CI checks, dependency and secret hygiene.
- **Leads QA:** tests every feature in "Ready for QA" against its acceptance criteria and confirms it before it becomes Done.
- Can block a release (veto on security findings).
- Uses agents: `code-reviewer` and `qa-tester`, and the `/review-pr` skill (see `docs/AGENTS.md`).

### Eugen, Agent Conductor
- Owns `CLAUDE.md`, `.claude/` (agents, skills, settings, hooks) and `docs/TOOLS.md`.
- Decides which agents exist, what they may do and how they work together.
- Responsible for the overall system architecture and interfaces.
- Can approve and merge pull requests.
- Makes sure agents work traceably (small PRs, clear commits, no access to secrets).

## Workflow

1. **Idea → Linear issue** (Elli), as a user story with acceptance criteria, assigned to a milestone.
2. **Implementation** on a branch named per `docs/RULES.md` (e.g. `feat/ELL-12-trip-list`), by a human with their Claude Code. `/start-task ELL-12` creates the branch and sets the issue to In Progress.
3. **Pull request** using the template, with the Linear ID in the title. `/review-pr` first, `/open-pr` to open it. No direct pushes to `main`.
4. **Review and merge** as described below.
5. **QA and acceptance:** Marvin leads QA, Elli gives the final acceptance. The Definition of Done in Linear applies (acceptance criteria met, reviewed, tests pass, no critical bugs, QA done, docs updated, approved for release).

### Review and merge
1. The **author** opens the PR and moves the Linear issue to Code Review.
2. **Marvin** is requested as reviewer on every PR, runs the `code-reviewer` agent (for example via `/review-pr`) and reviews the result. A "Request changes" review from Marvin blocks the merge until he resolves it.
3. The **approver** is Elli or Eugen, never the author. The approver approves and merges via **squash** after Marvin has reviewed, or after 48 hours without a response from him.
4. After the merge, the approver moves the issue to Ready for QA.
5. **Marvin** runs QA and writes the result as a comment. If a criterion fails, the issue goes back to In Progress.
6. **Elli** gives the final acceptance and sets the issue to Done.

Agents never approve, merge or set an issue to Done.

### Linear statuses
Target statuses are Backlog, Ready, In Progress, Code Review, Ready for QA, Done. Until Elli has set them up in Linear, use this mapping:

| Target | Today in Linear |
|--------|-----------------|
| Backlog | Backlog |
| Ready | Todo |
| In Progress | In Progress |
| Code Review | In Progress, with the PR linked |
| Ready for QA | In Progress, plus a comment "Ready for QA" |
| Done | Done |

### Keeping the repo and Linear in sync
- Do not copy changing Linear data into the repo (assignees, issue statuses, "who works on what"). Link to Linear instead.
- A branch or PR title that contains the issue ID (`ELL-12`) links to the issue automatically. Linear's own suggested branch name uses another format; use ours, it links just as well.
- Once the statuses exist, set up the Linear GitHub integration so that an opened PR moves the issue to Code Review and a merged PR moves it to Ready for QA, not Done.
- When you notice a difference between a doc and Linear, Linear wins; fix the doc in a small PR. Occasionally ask your Claude Code to compare the docs with Linear.

## Syncing
This is a hobby project, so there is no fixed meeting schedule. We sync ad hoc or when there is time, and Elli takes the lead. Day to day, the Linear board, open PRs and `main` show everyone what happened.

A visual guide to the whole workflow, including agents: [team-workflow.html](team-workflow.html) (open it in a browser after cloning).

## Guardrails on the free GitHub plan
Branch protection and rulesets are not available for private repos on the free plan, so the rules above are agreed by convention, with these supports:
- Repo settings: only squash merges allowed, head branches deleted after merge.
- Shared Claude Code settings (`.claude/settings.json`) block pushes to `main`, force pushes, `gh pr merge`, `gh pr review` and reading common `.env` files in the Bash and PowerShell tools, and ask before writing to Linear. This is easy to get around (for example `git push origin HEAD` while on `main`, or `cat .env`), so it is best effort for Claude Code sessions, not a security boundary. A shared git hook is a possible later step.
- PR template and CODEOWNERS request the right reviews.
- We revisit real enforcement if the repo goes public or we move to a paid plan.

## Quality gates (Marvin)
- Tests pass; new logic has tests.
- No secrets in the repo; no new dependencies without a short justification in the PR.
- Inputs are validated; user data (trip data, locations) is handled sparingly and protected.
- Agent-generated code is reviewed like third-party code.

## Rules for agents
- Work only on a branch, never directly on `main`.
- Commit/push only when instructed by a team member.
- Never read, write or output secrets.
- Never approve or merge a PR and never set an issue to Done.
- When unsure, ask instead of guessing.
