# Creating Tickets

Work is tracked as Linear tickets in the RSM (Radical Speed Month) team's project. GitHub is used only for the PR.

1. The owner describes what needs to be done
2. Decide with the owner whether the ticket should use a **team** or a **single agent** (see `reference/team-configurations.md` for available team configurations)
3. Create a Linear ticket (via the Linear MCP) with a **simple prompt** as the description + the appropriate label (`team:<config-name>` or `single-agent`)
   - Describe WHAT to do, as simply as possible, but without omitting any relevant information
   - Do NOT include requirements — agents do their own research
   - No technical directions, no requirement lists, no suggested implementation

## Linear Labels

- `team:<config-name>` — maps to a team configuration (e.g., `team:spec-to-code`)
  - `team:active` / `team:done` — team status
- `single-agent` — for tasks without a team
  - `single-agent:active` / `single-agent:done` — single-agent status

If any of these labels don't exist in the Linear project yet, create them via the Linear MCP before tagging.
