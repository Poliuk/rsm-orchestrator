# Starting Work on a Ticket

**Do NOT start automatically** — the owner and I review open Linear tickets together and agree which one to start.

**Never change the team configuration.** The mode in the ticket's `🤖 Orchestrator config` marker comment (`team:<config-name>` or `single-agent`) is the owner's decision. Always use the configuration specified there. If the marker comment is missing or unreadable, stop and ask the owner.

**One active workflow per worktree.** A worktree can have either one single-agent or one team working on it — never both, and never two of either. If the current workflow needs to be replaced, follow `reference/multiple-attempts.md` to create a new worktree.

## Setup

1. Read the Linear ticket (via `get_issue`) and its comments (via `list_comments`). Find the `🤖 Orchestrator config` marker comment to recover `mode`. The current workflow state on the issue (`state.name`) tells you whether work has already started.
2. Check for previous attempts: `git branch -a | grep 'rsm-<ticket-number>-'`. If any branches exist, report them to the owner before proceeding — follow `reference/multiple-attempts.md` to choose a versioned slug.
3. Choose an `<issue-slug>`: `rsm-<ticket-number>-<short-description>` (e.g. `rsm-123-dark-mode`). This is used everywhere — git branch, worktree name, and folder name.
4. Enter a worktree using `EnterWorktree` with `name` set to `<issue-slug>`. This creates (or re-enters) the worktree at `.claude/worktrees/<issue-slug>`. `EnterWorktree` creates the branch as `worktree-<issue-slug>` — immediately rename it to match the slug:
   ```
   git -C .claude/worktrees/<issue-slug> branch -m worktree-<issue-slug> <issue-slug>
   ```
   All agents launched from this point will inherit the worktree as their working directory.
   - **Never touch the main working directory.** Never `git checkout`, commit, or modify files outside the worktree.
   - **Install dependencies:** Run `npm install` right after entering the worktree.
5. Create folder: `issues/<issue-slug>/`
6. Generate `issues/<issue-slug>/prompt.md` using this format:

   ```markdown
   # RSM-<N>: <ticket title>

   - **Ticket:** <Linear ticket URL>
   - **Branch:** `<issue-slug>`

   <ticket body, adapted as a prompt — describe what to do, not how>
   ```

   - Copy the Linear ticket content and adapt it as a prompt directed at the agents
   - Do NOT add requirements, technical directions, or implementation details — agents do their own research
   - If the ticket has a spec from a previous `prompt-to-spec`: copy it to `issues/<issue-slug>/spec.md`. The issue folder must be self-contained.
   - If the ticket has attachments/screenshots: download via the Linear MCP and copy to `issues/<issue-slug>/screenshots/`. Reference them explicitly in the prompt.

7. Commit the issue folder with the message: `Add ticket context (orchestrator)`

## Launch

Proceed depending on the `mode` from the marker comment:

- **`team:<config-name>`:** follow `reference/launching-a-team.md`
- **`single-agent`:** follow `reference/launching-a-single-agent.md`

## After agents finish

1. Ensure `PR-description.md` has been written following `.github/pull_request_template.md` (Studio's template includes a "How AI was used in this PR" section — fill it honestly)
2. Push the branch and create a GitHub PR using the `PR-description.md` as the body
3. Post a comment on the Linear ticket with the PR URL
4. The owner reviews — see `reference/reviewing-work.md` if changes are needed
5. When approved — see `reference/finishing-work.md`
