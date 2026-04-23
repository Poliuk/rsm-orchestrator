# Multiple Attempts (Versioning)

When a previous result isn't good enough, or the owner wants to run two variations in parallel:

1. Keep v1 as reference
2. Choose a new `<issue-slug>`: `<original-slug>-v2` (then `-v3`, etc.)
3. Create new worktree and folder: `issues/<issue-slug>-v2/` (follow `reference/starting-work.md` using the new slug)
4. Launch a new team or single agent pointing to the new folder/worktree (see `reference/launching-a-team.md` or `reference/launching-a-single-agent.md`)
5. Compare results side by side

Never reuse an existing worktree for a different approach. Each attempt gets its own worktree.
