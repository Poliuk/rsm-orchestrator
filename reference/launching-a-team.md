# Launching a Team

## Setup

**Prerequisites:** if the worktree hasn't been set up yet, follow `reference/starting-work.md` first.

Choose the team configuration for the ticket — see `reference/team-configurations.md` for available options.

## Launch

1. **Post a start comment on the Linear ticket:**
   ```
   🤖 **Agent team started**
   - **Time:** YYYY-MM-DD HH:MM UTC
   - **Team config:** <config-name>
   - **Ticket:** RSM-<N> <description>
   ```
2. Update the Linear ticket label: `team:<config-name>` → add `team:active`
3. Create the team with `TeamCreate`
4. Launch agents as defined by the team configuration.
5. Follow the flow defined by the team configuration. Escalate to the owner if stuck.
6. Start health monitoring — see `reference/health-monitoring.md`

## After agents finish

1. Update label: `team:active` → `team:done`
2. **Post a completion comment on the Linear ticket:**
   ```
   ✅ **Agent team finished**
   - **Time:** YYYY-MM-DD HH:MM UTC
   - **Team config:** <config-name>
   - **Ticket:** RSM-<N> <description>
   - **Result:** <brief summary of what was done>
   ```
