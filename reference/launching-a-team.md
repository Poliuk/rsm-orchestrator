# Launching a Team

## Setup

**Prerequisites:** if the worktree hasn't been set up yet, follow `reference/starting-work.md` first.

Choose the team configuration for the ticket — see `reference/team-configurations.md` for available options.

## Launch

1. Move the Linear ticket to **In Progress** via `save_issue` (look up the RSM team's `In Progress` state ID via `list_issue_statuses` if you don't already have it).
2. **Post a start comment on the Linear ticket:**
   ```
   🤖 **Agent team started**
   - **Time:** YYYY-MM-DD HH:MM UTC
   - **Team config:** <config-name>
   - **Ticket:** RSM-<N> <description>
   ```
3. Create the team with `TeamCreate`
4. Launch agents as defined by the team configuration.
5. Follow the flow defined by the team configuration. Escalate to the owner if stuck.
6. Start health monitoring — see `reference/health-monitoring.md`

## After agents finish

1. Leave the Linear ticket in **In Progress** for now — final state transition (`Done` / `Cancelled`) happens in `reference/finishing-work.md` once the PR has merged or been abandoned.
2. **Post a completion comment on the Linear ticket:**
   ```
   ✅ **Agent team finished**
   - **Time:** YYYY-MM-DD HH:MM UTC
   - **Team config:** <config-name>
   - **Ticket:** RSM-<N> <description>
   - **Result:** <brief summary of what was done>
   ```
