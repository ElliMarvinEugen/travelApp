---
name: open-pr
description: Push the current branch and open a pull request against main from the project template, with the Linear issue ID in the title and Marvin requested as reviewer. Never approves or merges.
disable-model-invocation: true
allowed-tools: Bash(git status:*) Bash(git push:*) Bash(git log:*) Bash(git diff:*) Bash(gh pr create:*) Bash(gh pr edit:*) Read mcp__linear-server__get_issue
---

Open a pull request for the current branch. Follow `docs/RULES.md` and `docs/TEAM.md`. You never approve, merge or set a Linear status to Done.

1. **Check the branch:** it must not be `main`. Run `git status --short`; if there are uncommitted changes, tell the person and stop. Do not commit on your own.
2. **Find the Linear issue** from the branch name (`ELL-<number>`) and read it. Setup and meta changes without an issue are allowed.
3. **Push the branch:** `git push -u origin HEAD`.
4. **Fill the template** `.github/pull_request_template.md`:
   - "What and why" from the issue and the commits
   - "Changes" as a short list from `git diff main...HEAD --stat` and the commit messages
   - the checklist: tick only what is true. Leave "Marvin's review requested" and "Approved by Elli or Eugen" for the later steps.
5. **Create the PR:** `gh pr create --base main --title "<type>(<scope>): <summary> (ELL-<number>)" --body-file <file>` with the filled template written to a temporary file. Write the title in English, in the style of the commit convention in `docs/RULES.md`. Request Marvin as reviewer with `--reviewer marvinvec`, unless Marvin is the author.
6. **Report the PR URL** and remind the person: Marvin reviews first, then Elli or Eugen (never the author) approves and squash merges. If a Code Review status exists in Linear, mention that the author sets it.
