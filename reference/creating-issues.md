# Creating Tickets

Work is tracked as Linear tickets. GitHub is used only for the PR.

- **Linear team:** `RSM` (Radical Speed Month)
- **Linear project:** [Bring Data Liberation into Studio Code](https://linear.app/a8c/project/bring-data-liberation-into-studio-code-8e53bd986fcc)

The RSM team contains many projects belonging to different efforts across the company. This orchestrator works **only** on the project above — every new ticket MUST be filed inside it. Don't touch tickets in other RSM projects.

1. The owner describes what needs to be done
2. Decide with the owner whether the ticket should use a **team** or a **single agent** (see `reference/team-configurations.md` for available team configurations)
3. Create a Linear ticket (via the Linear MCP) with:
   - **Team:** `RSM`
   - **Project:** `Bring Data Liberation into Studio Code` (required — never leave the project unset)
   - **State:** the RSM team's default backlog/triage state (no special handling — leave whatever Linear assigns)
   - **Description:** a **simple prompt** describing what to do
   - Describe WHAT to do, as simply as possible, but without omitting any relevant information
   - Do NOT include requirements — agents do their own research
   - No technical directions, no requirement lists, no suggested implementation
4. **Post the orchestrator config marker as the first comment on the new ticket** (via the Linear MCP):
   ```
   🤖 Orchestrator config
   - mode: <team:config-name | single-agent>
   ```
   For single-agent tickets, optionally add `- agent: <implementer | documentator | researcher>` if the owner has decided the flavor up front; otherwise omit it and let `starting-work.md` pick.

## Why a marker comment, not labels

The Linear MCP cannot create labels on the RSM team (the connector lacks workspace-admin scope). A marker comment carries the same configuration without any label vocabulary to bootstrap. Active/done state is tracked by the ticket's **native Linear workflow state** (`Todo` → `In Progress` → `Done`/`Cancelled`), set via `save_issue` — see the launch and finish reference docs.

The marker comment is read-only after creation: every later orchestrator step reads it to recover the configuration. Don't post a second marker on the same ticket. If the comment is missing or malformed, escalate to the owner instead of guessing.
