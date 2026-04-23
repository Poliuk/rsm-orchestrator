# Reviewing Work

For addressing review feedback — either from GitHub PR comments, Linear ticket comments, or from the owner reviewing directly in conversation.

Before doing anything, enter the existing worktree using `EnterWorktree` with the `<issue-slug>` as the name (`.claude/worktrees/<issue-slug>`). All agents launched from this point will inherit it.

**Always ask the owner first** how to handle the changes. Present the options:

1. **Orchestrator does it directly** — for small changes (typo, style, rename). Commits with `<description> (orchestrator)` and pushes.
2. **Single agent** — for medium changes. Follow `reference/launching-a-single-agent.md` with the requested changes as context in the prompt.
3. **Team** — for large changes. Use the `review` team configuration (see `reference/teams/review.md`) and follow `reference/launching-a-team.md`.

Do NOT proceed until the owner picks an option.
