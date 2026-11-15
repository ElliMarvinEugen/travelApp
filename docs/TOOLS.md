# Tools

Owner: Eugen (Agent Conductor). Changes to this list go through a PR.

## Tech stack: idea, NOT final
The Linear project [Travel Planner App](https://linear.app/elli-huynh/project/travel-planner-app-226f2629a820) lists the stack below as an idea. It is not decided yet. We still need to agree how to handle it, including costs (hosting, Supabase plan, Mapbox usage, Claude API usage). Until then, nobody sets up a stack or paid service on their own.

| Area | Idea |
|------|------|
| Frontend | Next.js (App Router), React, TypeScript |
| Styling | Tailwind CSS, shadcn/ui, Lucide icons |
| Backend & database | Supabase / PostgreSQL |
| Authentication | Supabase Auth |
| Collaboration (real-time) | Supabase Realtime |
| Maps | Mapbox |
| AI integration (later, after MVP) | Anthropic Claude API |
| Hosting | Vercel (preview deployments for PRs) |

Principles from Linear: build the MVP before AI features, keep the app fully functional without AI, modular architecture, secure auth.

Open decisions: final stack, cost limits per service (free tiers vs. paid), who owns accounts and billing.

How it gets decided: the `architect` agent compares the options (cost is an explicit criterion) and drafts an ADR in `docs/adr/`. Eugen decides on the technical architecture, Elli on business and functional impact including the cost the product has to bear, and Marvin reviews the security aspects. Until an ADR is accepted, the stack stays an idea.

## Process & tooling
| Purpose | Tool |
|---------|------|
| Code & version control | Git, GitHub (`ekutschkin-priv/travelApp`, free plan) |
| Backlog, planning, kanban/agile board | Linear, workspace "Elli Huynh", team key `ELL` |
| Code review | GitHub pull requests, template in `.github/`, squash merge |
| AI-assisted development | Claude Code with subagents (configuration in `CLAUDE.md` and `.claude/`) |
| Security check | `/security-review` (Claude Code, general-purpose) and agent `code-reviewer` (knows our rules and the Linear issue) |

Still to be defined by the team (tracked in Linear): linting and formatting, environment variables and secrets, CI and testing, secret scanning.

## Linear
- Linear is the source of truth for the backlog and planning. GitHub Issues are not used.
- Claude Code accesses Linear through the project's `.mcp.json` (server `linear-server`). This is the only supported way, so agent tool names are the same on every machine. Claude Code asks you to approve the project server once; then sign in via `/mcp`. Do not add a second Linear connector in the app settings.
- Link work to Linear: use the Linear issue ID in branch names and PR titles (e.g. `feat/ELL-12-trip-list`) so Linear and GitHub connect automatically.
- Agents read Linear freely. Creating or editing issues only on request of a team member, and agents never set an issue to Done.

## Agents (`.claude/agents/`)
Agents (`product-owner`, `architect`, `code-reviewer`, `ui-ux-reviewer`, `qa-tester`) and skills (`/start-task`, `/review-pr`, `/open-pr`) are described in `docs/AGENTS.md`, including prerequisites, permissions and limitations.
