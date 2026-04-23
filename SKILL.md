---
name: orchestrator
description: Coordinates development work through Linear tickets, agent teams, and GitHub PRs. Use when the owner wants to create, start, review, or finish work on a ticket.
user-invocable: true
---

# Orchestrator

The orchestrator coordinates development work between the project owner and AI agents. It manages the full lifecycle of every change — from creating a Linear ticket to merging the final GitHub PR — by setting up branches and worktrees, launching and monitoring agent teams or single agents, handling review iterations, and cleaning up when done.

## Conventions

- **Source of truth:** work is tracked as Linear tickets in the RSM (Radical Speed Month) team's project. GitHub is used only for the PR (branch push, review, merge).
- **Ticket ID:** RSM tickets have IDs like `RSM-123`; `<ticket-number>` refers to the numeric part (`123`).
- **Issue slug:** `rsm-<ticket-number>-<short-description>` (e.g. `rsm-123-dark-mode`) — referred to as `<issue-slug>` in all reference docs. Used for the git branch, worktree name, and folder name.
- **Branch naming:** `<issue-slug>` (e.g. `rsm-123-dark-mode`) — matches Linear's branch convention (lowercase team prefix + ticket number + description). `EnterWorktree` creates the branch with a `worktree-` prefix by default; rename it to the bare slug right after entering: `git -C .claude/worktrees/<issue-slug> branch -m worktree-<issue-slug> <issue-slug>`.
- **Worktrees:** all work happens in `.claude/worktrees/<issue-slug>` (managed by `EnterWorktree`). Never work in the main directory.
- **Issue folders:** `issues/<issue-slug>/` — one subfolder per ticket, contains prompt, spec, PR description, screenshots, etc.

## Workflows

Before executing ANY workflow, you MUST read the corresponding reference file(s) listed below — in full, not from memory. This applies every time, even if you have read the file before in this conversation. Always re-read before executing.

| When the owner wants to...    | Read                             |
| ----------------------------- | -------------------------------- |
| Create a ticket               | `reference/creating-issues.md`   |
| Start working                 | `reference/starting-work.md`     |
| Resume paused or stopped work | `reference/resuming-work.md`     |
| Review and iterate            | `reference/reviewing-work.md`    |
| Finish and merge              | `reference/finishing-work.md`    |
| Retry with a new attempt      | `reference/multiple-attempts.md` |
