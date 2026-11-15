# Setup Guide

One-time setup for every team member. Afterwards, working on the project means opening your clone in Claude Code. Context: [one-pager](ai-development-onepager.md), [workflow guide](team-workflow.html), [agents and skills](AGENTS.md).

## 1. Get access
- **GitHub:** you are a collaborator on the private repo `ElliMarvinEugen/travelApp`.
- **Linear:** you are a member of the workspace (team key `ELL`).

## 2. Install the tools
Git, the GitHub CLI (`gh`) and the Claude desktop app (Code tab).

```bash
# Windows
winget install GitHub.cli
# macOS
brew install gh
```

Restart the app (or terminal) afterwards so `gh` is on the PATH.

## 3. Sign in to GitHub
The CLI shows a one-time code; enter it in the browser while logged in to your own GitHub account.

```bash
gh auth login --web --git-protocol https
```

## 4. Clone the repo and open it in Claude Code
```bash
git clone https://github.com/ElliMarvinEugen/travelApp.git
```

Open the folder as the project in Claude Code. It loads `CLAUDE.md` and `docs/RULES.md` automatically, so your session follows the same rules as everyone else's.

## 5. Connect Linear
The repo already contains the Linear connection (`.mcp.json`, enabled in `.claude/settings.json`).
1. Open a **new** session in the project folder and approve the project server if asked.
2. Sign in to Linear with your own account (`/mcp`, or the connector view of the app).
3. Do **not** add a second Linear connector in the app settings. Agents rely on the tool names `mcp__linear-server__*`.

## 6. Check that it works
```bash
gh auth status
```

Then ask your Claude: "Which Linear issues are assigned to me?" and "List the agents and skills of this project." You should see the five agents (`product-owner`, `architect`, `code-reviewer`, `ui-ux-reviewer`, `qa-tester`) and the skills `/start-task`, `/review-pr`, `/open-pr`.

## Your first task
1. Pick an issue in Linear and run `/start-task ELL-<number>`.
2. Implement with Claude Code, commit when you are ready.
3. `/review-pr`, fix the findings, then `/open-pr`.

## Good to know
- Everybody signs in with their own account. Never share tokens or passwords, and never put them in the repo.
- Never work on `main`. Use a branch named per `docs/RULES.md`.
- Do not run Claude Code in auto or bypass permission mode: the shared guardrails (no push to `main`, ask before writing to Linear) would stop applying.

## Troubleshooting
| Problem | Fix |
|---------|-----|
| `gh` not found | Restart the app or terminal after installing |
| Linear tools missing | Start a new session in the project folder, run `/mcp`, sign in. Check that no second Linear connector is enabled |
| Agents or skills not listed | You opened the wrong folder. Open the repo root |
