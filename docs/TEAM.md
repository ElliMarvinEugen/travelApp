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
- Uses agent: `product-owner` (refine stories) and Claude Code for implementation.

### Marvin, Security & Quality Manager
- Reviews pull requests for security and quality (see quality gates below).
- Owns the test strategy, CI checks, dependency and secret hygiene.
- **Leads QA:** tests every feature in "Ready for QA" against its acceptance criteria and confirms it before it becomes Done.
- Can block a release (veto on security findings).
- Uses agent: `security-reviewer` and `/security-review`.

### Eugen, Agent Conductor
- Owns `CLAUDE.md`, `.claude/` (agents, skills, settings, hooks) and `docs/TOOLS.md`.
- Decides which agents exist, what they may do and how they work together.
- Responsible for the overall system architecture and interfaces.
- Can approve and merge pull requests.
- Makes sure agents work traceably (small PRs, clear commits, no access to secrets).

## Workflow

1. **Idea → Linear issue** (Elli), as a user story with acceptance criteria, assigned to a milestone.
2. **Implementation** on a feature branch (`feat/ELL-12-…`, `fix/ELL-12-…`, `chore/ELL-12-…`), by a human or an agent.
3. **Pull request** using the template. No direct pushes to `main`.
4. **Review:** every PR needs approval from **Elli or Eugen**. Marvin reviews security and quality and can veto.
5. **Merge** via **squash merge**.
6. **QA and acceptance:** Marvin leads QA, Elli gives the final acceptance. The Definition of Done in Linear applies (acceptance criteria met, reviewed, tests pass, no critical bugs, QA done, docs updated, approved for release).

## Syncing
This is a hobby project, so there is no fixed meeting schedule. We sync ad hoc or when there is time, and Elli takes the lead. Day to day, the Linear board, open PRs and `main` show everyone what happened.

A visual guide to the whole workflow, including agents: [team-workflow.html](team-workflow.html) (open it in a browser after cloning).

Linear's target workflow statuses are Backlog, Ready, In Progress, Code Review, Ready for QA, Done (being set up in ELL-14). The branching and PR strategy is being finalized by Marvin in ELL-16; this section is the interim rule and gets aligned with that outcome.

## Quality gates (Marvin)
- Tests pass; new logic has tests.
- No secrets in the repo; no new dependencies without a short justification in the PR.
- Inputs are validated; user data (trip data, locations) is handled sparingly and protected.
- Agent-generated code is reviewed like third-party code.

## Rules for agents
- Work only on a branch, never directly on `main`.
- Commit/push only when instructed by a team member.
- Never read, write or output secrets.
- When unsure, ask instead of guessing.
