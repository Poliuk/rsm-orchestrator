# Resuming Paused or Stopped Work

For picking up a ticket where a previous orchestrator session stopped, stalled, or was interrupted. The worktree, commits, team file, and Linear labels may all exist — the job is to diagnose where the flow stopped and continue from the right point through to completion.

## Detect state (do all before acting)

1. Ticket + labels: get the Linear ticket (via the Linear MCP) by ID `RSM-<N>`. Confirm it belongs to the `Bring Data Liberation into Studio Code` project — if it's in a different RSM project, stop and check with the owner; this orchestrator does not operate outside that project.
2. Worktree: `ls .claude/worktrees/ | grep rsm-<N>-`
3. Branch: `git branch -a | grep rsm-<N>-`
4. Issue folder: `ls issues/<issue-slug>/`
5. Recent commits on branch: `git -C .claude/worktrees/<issue-slug> log --oneline -20`
6. Team config file (if team): `~/.claude/teams/<issue-slug>/config.json`
7. PR: `gh pr list --search 'rsm-<N>'` (or look up by branch name)
8. Old orchestrator still alive? `ps aux | grep claude | grep -v grep`. If yes, ask the owner before resuming — split-brain is worse than paused.

## Determine the phase

The team-configuration reference (`reference/teams/<config>.md` for teams, or `reference/launching-a-single-agent.md` for single agents) defines the expected sequence. Walk the flow top-to-bottom and check the corresponding artifact + commit for each step:

- Artifact exists in `issues/<issue-slug>/`? Step completed.
- Commit with the expected message on the branch? Step completed.
- A review step that rejected, followed by a newer revision commit but no subsequent review? Stuck — the next review wasn't launched.
- A task list with partial execution (fewer implementation commits than planned tasks)? Stuck — the next task wasn't started.

Any ambiguity: read the most recent artifact end-to-end and let it speak.

## Enter the worktree

`EnterWorktree` with `path: .claude/worktrees/<issue-slug>`. Never `cd`.

## Verify before relaunching

Do not trust summaries, commit messages, or prior reports. Read files:

- Open the latest artifact in full.
- For any review verdict, confirm it in the file itself — the review file states APPROVED/REJECTED.
- For implementation work, run the verification commands the project uses (e.g. `npm run typecheck`, `npm test`) to confirm committed code is green before moving on.

## Post a resume comment on the Linear ticket

Always post this, regardless of whether the original start comment was posted:

```
🔄 **Work resumed**
- **Time:** YYYY-MM-DD HH:MM UTC
- **Mode:** <team-config-name | single-agent>
- **Ticket:** RSM-<N> <description>
- **Resumed from:** <phase / last commit>
```

## Back-fill other housekeeping

- Labels match the current state? (e.g. `team:active`/`team:done`, `single-agent:active`/`single-agent:done`).
- Health monitoring running? Restart per `reference/health-monitoring.md`.

## Handle the existing team

- In-process team members (`backendType: "in-process"` in the team config) are bound to the previous session and are dead — they cannot be resumed.
- Reuse the team by spawning new agents with `team_name: "<issue-slug>"` and a fresh unique `name`. The team config file persists on disk across sessions.
- Do NOT `TeamDelete` — it discards the task list and member history. Delete only if the owner explicitly asks for a fresh start (then follow `reference/multiple-attempts.md`).

## Continue the flow through to completion

Resume the next agent(s) the flow expects, and keep going through the rest of the flow until its natural finish. Two rules:

1. **Never re-run a completed step.** If an artifact exists and matches its expected commit, that step is done — do not relaunch its agent.
2. **Always re-run an incomplete loop.** A rejected review with a subsequent revision but no new review means the reviewer must fire again. A task list with missing commits means the next task owner must start at the first missing task.

Resume is a continuation, not a fresh start — do not pause for re-approval of the overall plan. Escalate to the owner only if the detect-state step surfaces something the owner must resolve (live old process, inconsistent artifacts, genuinely ambiguous state).
