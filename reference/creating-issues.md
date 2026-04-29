# Creating Tickets

Work is tracked as Linear tickets. GitHub is used only for the PR.

- **Linear team:** `RSM` (Radical Speed Month)
- **Linear project:** [Bring Data Liberation into Studio Code](https://linear.app/a8c/project/bring-data-liberation-into-studio-code-8e53bd986fcc)

The RSM team contains many projects belonging to different efforts across the company. This orchestrator works **only** on the project above — every new ticket MUST be filed inside it. Don't touch tickets in other RSM projects.

1. The owner describes what needs to be done
2. Decide with the owner whether the ticket should use a **team** or a **single agent** (see `reference/team-configurations.md` for available team configurations)
3. Create a Linear ticket via the Linear MCP `save_issue` tool. The call **must** pass these fields together — `team` alone is not enough; the RSM team holds many projects and a ticket created without `project` lands in the team's general bucket and has to be moved by hand:
   - `team: "RSM"`
   - `project: "Bring Data Liberation into Studio Code"` — **required, no exceptions**
   - `title: <short title>`
   - `description: <simple-prompt body>`
   - Leave `state` unset — accept whatever Linear assigns as the backlog/triage default.
   - Describe WHAT to do, as simply as possible, but without omitting any relevant information
   - Do NOT include requirements — agents do their own research
   - No technical directions, no requirement lists, no suggested implementation
4. **Verify the ticket landed in the right project.** Immediately after `save_issue` returns, call `get_issue` on the new ID and confirm `project.id` is non-null and that `project.name` is `"Bring Data Liberation into Studio Code"`. If it isn't (e.g., the project name didn't resolve, or you forgot the `project` field), call `save_issue` again with the new issue's `id` and `project: "Bring Data Liberation into Studio Code"` to fix it before doing anything else. Never proceed past this step with an unprojected ticket.
5. **Post the orchestrator config marker as the first comment on the new ticket** (via the Linear MCP):
   ```
   🤖 Orchestrator config
   - mode: <team:config-name | single-agent>
   ```
   For single-agent tickets, optionally add `- agent: <implementer | documentator | researcher>` if the owner has decided the flavor up front; otherwise omit it and let `starting-work.md` pick.

## Follow-up tickets

This procedure applies to **every** ticket the orchestrator creates, not just the initial one the owner described. That includes:

- **Research → implementation handoff.** When a `research` team finishes, the orchestrator may decide to file a separate ticket so the implementation runs as its own attempt with its own worktree and team. That follow-up is a brand-new `save_issue` call — re-do steps 3–5 in full, including the `project` field and the verification step. Link the new ticket to the original via the description body (and optionally `relatedTo`).
- **Bug discovered mid-flow.** If an agent surfaces a bug that warrants its own ticket, the orchestrator files it through the same procedure.
- **Retries.** New attempts that need a fresh ticket (see `reference/multiple-attempts.md`) follow the same procedure.

If you find yourself reaching for `save_issue` without re-reading this file, stop and re-read it. Skipping the project field is the easiest mistake to make and the easiest to prevent.

## Why a marker comment, not labels

The Linear MCP cannot create labels on the RSM team (the connector lacks workspace-admin scope). A marker comment carries the same configuration without any label vocabulary to bootstrap. Active/done state is tracked by the ticket's **native Linear workflow state** (`Todo` → `In Progress` → `Done`/`Cancelled`), set via `save_issue` — see the launch and finish reference docs.

The marker comment is read-only after creation: every later orchestrator step reads it to recover the configuration. Don't post a second marker on the same ticket. If the comment is missing or malformed, escalate to the owner instead of guessing.
