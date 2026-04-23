# Launching a Single Agent

## Setup

**Prerequisites:** if the worktree hasn't been set up yet, follow `reference/starting-work.md` first.

## Launch

1. Update the Linear ticket label: `single-agent` → `single-agent:active`
2. **Post a start comment on the Linear ticket:**
   ```
   🤖 **Single agent started**
   - **Time:** YYYY-MM-DD HH:MM UTC
   - **Mode:** single-agent
   - **Ticket:** RSM-<N> <description>
   ```
3. Launch the agent with `Agent` using `run_in_background: true`:
   - Choose `subagent_type` from this list:
     - `implementer` — for code tasks
     - `documentator` — for documentation tasks
     - `researcher` — for research tasks
   - If no type fits, use a generic agent (no `subagent_type`)
   - Single agents are standalone — they are not part of a team. Do not create a team with `TeamCreate` for single-agent work.
4. Start health monitoring — see `reference/health-monitoring.md`

## After the agent finishes

1. Update label: `single-agent:active` → `single-agent:done`
2. Review the agent's output
3. **Post a completion comment on the Linear ticket:**
   ```
   ✅ **Single agent finished**
   - **Time:** YYYY-MM-DD HH:MM UTC
   - **Mode:** single-agent
   - **Ticket:** RSM-<N> <description>
   - **Result:** <brief summary of what was done>
   ```
