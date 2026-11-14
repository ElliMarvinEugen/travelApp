# Architecture Decision Records (ADRs)

An ADR records one architecture or tooling decision, with its context, the options considered and the consequences. The reasoning stays in the repo, so later sessions and new team members do not have to rediscover it.

## When to write one
- Choosing or changing the tech stack, a framework or a paid service.
- A design decision that is expensive to reverse (auth approach, data model foundations, real-time approach, how AI plugs in).
- Anything where cost, security or lock-in matter.

Small, reversible implementation choices do not need an ADR.

## Process
1. The `architect` agent (see `docs/AGENTS.md`) or a team member drafts the ADR from `0000-template.md` as `NNNN-short-kebab-title.md`, status `Proposed`.
2. It goes through a pull request like any other change, with a Linear issue.
3. **Eugen** decides on the architecture. **Elli** decides on business and functional impact (scope, cost the product has to bear). **Marvin** reviews the security aspects first.
4. On approval the status becomes `Accepted` and the PR is squash-merged by Elli or Eugen (never the author). An accepted ADR is changed only by a new ADR that supersedes it.

## Index
| ADR | Title | Status |
|-----|-------|--------|
| none yet | | |
