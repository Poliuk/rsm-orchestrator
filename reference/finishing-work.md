# Finishing Work

- **Merge:** `gh pr merge --merge`. **No squash, no fast-forward.** Never merge locally.
- **Abandon:** close the GitHub PR.
- **Retry:** see `reference/multiple-attempts.md`.

After merging or abandoning:

1. Remove the worktree using `ExitWorktree`.
2. Update the Linear ticket (via the Linear MCP):
   - Move the ticket's workflow state to **Done** (merged) or **Cancelled** (abandoned) using `save_issue`. Look up state IDs with `list_issue_statuses` for the RSM team.
   - Post a short completion comment with the merged PR URL (or a note that the attempt was abandoned).
   - Do NOT touch the `🤖 Orchestrator config` marker comment — leave it as the historical record of how the ticket was run.
