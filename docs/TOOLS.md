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

## Process & tooling
| Purpose | Tool |
|---------|------|
| Code & version control | Git, GitHub (`ekutschkin-priv/travelApp`) |
| Backlog, planning, kanban/agile board | Linear, workspace "Elli Huynh", team key `ELL` |
| Code review | GitHub pull requests, template in `.github/`, squash merge |
| AI-assisted development | Claude Code with subagents (configuration in `CLAUDE.md` and `.claude/`) |
| Security check | `/security-review` (Claude Code) plus agent `security-reviewer` |

Still to be defined by the team (tracked in Linear): linting/formatting (ELL-18), env vars and secrets (ELL-19), CI and testing, secret scanning.

## Linear
- Linear is the source of truth for the backlog and planning. GitHub Issues are not used.
- Claude Code accesses Linear through the Linear connector (MCP), so agents can read issues, projects, documents and comments.
- Link work to Linear: use the Linear issue ID in branch names and PR titles (e.g. `feat/ELL-12-trip-list`) so Linear and GitHub connect automatically.
- Write access (creating or editing issues, changing status) by agents only on request of a team member.

## Agents (`.claude/agents/`)
| Agent | For | Purpose | Status |
|-------|-----|---------|--------|
| `product-owner` | Elli | Refine ideas into user stories with acceptance criteria | exists |
| `security-reviewer` | Marvin | Review changes for backend/security and quality problems | exists |
| UI/UX reviewer | Elli | Review UI changes for usability and design quality | planned (ELL-24) |
| QA/testing | Marvin | Test planning and QA checks | planned (ELL-24) |

The initial subagent architecture is Eugen's task ELL-24; the table above is a starting point and follows the outcome of that issue.
