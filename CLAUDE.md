# travelApp

Collaborative, AI-powered travel planning web app (itineraries, multi-city trips, maps, bookings, budgets, shared planning with friends).

**Linear is the source of truth** for vision, MVP scope, milestones, Definition of Done and tasks: [Travel Planner App](https://linear.app/elli-huynh/project/travel-planner-app-226f2629a820) (team key `ELL`). Read the project and the relevant issue there before starting work. If this file conflicts with Linear, Linear wins.

## Tech stack
**Not final.** Linear lists an idea (Next.js, Supabase, Mapbox, Vercel), but the team has not decided yet, partly because of costs. Do not assume or introduce a stack, framework or paid service on your own; ask first. Stack and tool choices are decided by Eugen (architecture) with Elli (business/functional impact) and Marvin (security review) through ADRs in `docs/adr/`. See `docs/TOOLS.md`.

## Team
- **Elli** (`elliHuynh`): Product Owner & Lead Dev
- **Marvin** (`marvinvec`): Security & Quality Manager
- **Eugen** (`ekutschkin-priv`): Agent Conductor (Architect for Agents), owns the technical architecture

Details on roles, workflow and quality gates: `docs/TEAM.md`.

## Project rules (apply to everyone, humans and agents)
@docs/RULES.md

## Agents and skills
Agents live in `.claude/agents/`, skills in `.claude/skills/` (`/start-task`, `/review-pr`, `/open-pr`). You implement in the main session; subagents are read-only reviewers and planners. See `docs/AGENTS.md`.

## Agent essentials
- Never work directly on `main`; always use a branch named per the rules above.
- Only commit/push when a team member asks for it.
- Never read, write or output secrets. Never commit `.env` files.
- Reference the Linear issue ID in branch names and PR titles.
- When unsure, ask. Decisions belong to the responsible role (see `docs/TEAM.md`).
