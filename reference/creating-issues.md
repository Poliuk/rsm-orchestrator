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
   - **Description:** a **simple prompt** describing what to do
   - **Label:** `team:<config-name>` or `single-agent`
   - Describe WHAT to do, as simply as possible, but without omitting any relevant information
   - Do NOT include requirements — agents do their own research
   - No technical directions, no requirement lists, no suggested implementation

## Linear Labels

- `team:<config-name>` — maps to a team configuration (e.g., `team:spec-to-code`)
  - `team:active` / `team:done` — team status
- `single-agent` — for tasks without a team
  - `single-agent:active` / `single-agent:done` — single-agent status

Labels in Linear are scoped to the team, not the project. If any of these labels don't exist on the RSM team yet, create them via the Linear MCP before tagging.
