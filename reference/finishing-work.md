# Finishing Work

- **Merge:** `gh pr merge --merge`. **No squash, no fast-forward.** Never merge locally.
- **Abandon:** close the GitHub PR.
- **Retry:** see `reference/multiple-attempts.md`.

After merging or abandoning:

1. Remove the worktree using `ExitWorktree`.
2. Update the Linear ticket (via the Linear MCP):
   - Remove the `*:active` label; add `*:done` if not already set.
   - Move the ticket status to Done (or Cancelled if abandoned).
   - Post a short completion comment with the merged PR URL (or a note that the attempt was abandoned).
