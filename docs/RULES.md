# Project Rules

These rules apply to everyone working in this repo: Elli, Marvin, Eugen, their Claude Code sessions and all agents. They are loaded automatically via `CLAUDE.md`, so every Claude Code instance follows the same rules.

## How these rules change
- This is a living document. More rules will be added over time.
- Changes go through a pull request like any other change (approval from Elli or Eugen, Marvin reviews).
- If a rule is unclear or blocks you, ask or propose a change. Do not silently work around it.
- Stack-specific details (formatter, linter, framework patterns) are added once the tech stack is final.

## 1. Language
- Everything is written in **English**: documentation, code, identifiers, comments, commit messages, PR titles and descriptions, branch names.
- Team conversation and chat with agents may be in any language; anything that lands in the repo is English.

## 2. Comments
- Comment where it helps: explain **why**, not what. Good targets are non-obvious decisions, workarounds, business rules, edge cases, and public APIs/modules.
- Do not comment obvious code or restate the code in words.
- No commented-out code; git keeps the history.
- A `TODO` must reference a Linear issue (`// TODO(ELL-42): …`). No anonymous TODOs.
- Keep comments up to date when code changes. A wrong comment is worse than none.

## 3. Naming conventions
One convention for the whole project. Defaults below apply to TypeScript/JavaScript and will be confirmed when the stack is final.

| Thing | Convention | Example |
|-------|------------|---------|
| Branches | `<type>/ELL-<id>-<short-kebab-description>`, type is `feat`, `fix`, `chore` or `docs`. Setup and meta changes without a Linear issue may omit the ID. | `feat/ELL-10-invite-travelers` |
| Commits | Conventional Commits, imperative mood, Linear ID in the subject or footer | `feat(trips): add invitation links (ELL-10)` |
| Files and folders | `kebab-case` | `trip-overview.tsx` |
| Variables, functions | `camelCase`, verb for functions | `getTripById` |
| Types, classes, components | `PascalCase` | `TripCard` |
| Constants | `UPPER_SNAKE_CASE` | `MAX_TRAVELERS` |
| Booleans | prefix `is`, `has`, `can`, `should` | `isArchived` |
| Environment variables | `UPPER_SNAKE_CASE` | `MAPBOX_ACCESS_TOKEN` |
| Database tables and columns (if SQL) | `snake_case`, tables plural | `trip_members` |
| Test files | source file name plus `.test` | `trip-overview.test.tsx` |

General:
- Use full, descriptive English words. No cryptic abbreviations (common ones like `id`, `url` are fine).
- Use the same term for the same concept everywhere (e.g. always "trip", "traveler", "itinerary", never mixed synonyms).
- Match the surrounding code when in doubt, and propose a rule change instead of introducing a second style.

## 4. Process (see `docs/TEAM.md`)
- Never work directly on `main`; use a branch and a pull request.
- Every PR needs approval from Elli or Eugen (never the author) and is merged via squash by the approver. Marvin reviews security and quality first. Details in `docs/TEAM.md`.
- Keep PRs small and focused; reference the Linear issue.
- No secrets in the repo. No new dependencies without justification in the PR.
- Linear is the source of truth for product scope, tasks and the Definition of Done.

## 5. Rules for agents
- Follow this file and `CLAUDE.md`, same as humans.
- Commit or push only when a team member asks.
- Never read, write or output secrets.
- Never approve or merge a PR and never set a Linear issue to Done. Humans decide at the gates.
- Read Linear freely; create or change issues only when a team member asks.
- When unsure or when a request conflicts with these rules, ask instead of guessing.

## 6. Review findings format
Used by every reviewer, human or agent, so results look the same.
- Order findings by severity: critical, high, medium, low.
- Each finding has: `file:line`, what is wrong, why it matters (risk or violated rule), and a concrete fix.
- If nothing is found, say "No findings" and list what was checked.
- Reviewers report only. They do not change code, approve or merge.
