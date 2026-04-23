# Health Monitoring

Whenever agents are running — whether a team or a single agent — set up a recurring health check to detect stalls:

```
/loop 15m Check if the agents working on Linear ticket RSM-<N> are still making progress. Look for signs of stalling: an agent that hasn't produced output recently, a team agent that failed to start or didn't receive a message, or the Claude Code session approaching its time limit. If anything is stalled, diagnose the problem and restart or re-send as needed. Report to the owner if the issue can't be resolved automatically.
```

**When to start:** Immediately after launching agents (team or single agent).

**When to stop:** Once all agents have finished.
