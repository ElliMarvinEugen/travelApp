---
name: review-pr
description: Run the reviewer agents on the current branch (changes against main) in parallel and combine their findings into one list. Use before opening or approving a PR. Reports only, never approves or merges.
argument-hint: (optional) ELL-<number>
allowed-tools: Agent Bash(git diff:*) Bash(git log:*) Bash(git status:*) mcp__linear-server__get_issue
---

Review the current branch against `main` using the reviewer agents. Follow `docs/RULES.md`. You only report: never approve, merge, comment on the PR, change code or change Linear.

1. **Check there is something to review:** `git diff main...HEAD --stat`. If the diff is empty, say so and stop.
2. **Find the Linear issue** from the argument or from the branch name (`ELL-<number>`). If there is none (setup or meta change), review without it.
3. **Run the agents in parallel** (one message, several Agent calls), each with the branch name and the issue ID:
   - `code-reviewer`: security, backend, rules compliance
   - `ui-ux-reviewer`: only if the diff touches UI files; otherwise skip it
   - `qa-tester`: test plan and gaps against the acceptance criteria (needs an issue; skip it if there is none)
4. **Combine the results into one list** in the findings format from `docs/RULES.md` (section 6): remove duplicates, sort by severity (critical, high, medium, low), and tag each finding with the agent that raised it. If an agent found nothing, say "No findings" for it.
5. **Finish with a short summary:** which agents ran, the number of findings per severity, and a reminder that Marvin decides on veto and Elli or Eugen (not the author) approves.
