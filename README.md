# rsm-orchestrator

A Claude Code skill that coordinates multi-agent development work — from Linear ticket to merged GitHub PR. Built for Automattic's **Radical Speed Month (RSM)** initiative, specifically the [Bring Data Liberation into Studio Code](https://linear.app/a8c/project/bring-data-liberation-into-studio-code-8e53bd986fcc) project, driving code changes into the [Studio](https://github.com/automattic/studio) repo.

## What it does

You describe what you want built. The orchestrator (running inside Claude Code) then:

1. Creates a **Linear ticket** in the RSM team's _Bring Data Liberation into Studio Code_ project with a simple prompt
2. Sets up an isolated **git worktree** in the Studio repo
3. Launches one or more **Claude agents** — either a single worker or a coordinated team with specialist roles
4. Monitors progress, handles review iterations, and recovers from stalls
5. Opens a **GitHub PR** on Studio and links it back to the Linear ticket
6. Merges and cleans up once you approve

The orchestrator itself is just a set of markdown reference docs that Claude reads. There's no runtime, no daemon, no separate service — Claude Code does all the work.

## How it works

```
You ──idea──▶ Orchestrator (Claude Code)
                    │
                    ├─ creates Linear ticket: RSM-123
                    ├─ creates worktree: .claude/worktrees/rsm-123-foo
                    ├─ spawns agent(s) in the worktree
                    │      │
                    │      └─ agents write code, tests, docs, reviews
                    │
                    ├─ opens PR on automattic/studio
                    ├─ posts PR URL to the Linear ticket
                    └─ waits for your review
```

Every ticket gets its own worktree on a branch named `rsm-<ticket-number>-<description>`. The orchestrator never touches your main working directory, so you can keep working on other things in parallel.

## Single agent vs. team

An **agent** is a Claude instance spawned to do work. A ticket can be handled by:

- **Single agent** — one Claude does it all. Fast, cheap, fine for small/scoped work. Flavors: `implementer` (code), `documentator` (docs), `researcher` (investigation).
- **Team** — multiple Claudes with specialist roles that hand off work through committed artifacts (spec → plan → code → review). Slower, but with built-in review gates that catch mistakes before you see them.

### Team configurations

| Config | Input | Output | Use when… |
|---|---|---|---|
| `prompt-to-spec` | rough idea | reviewed `spec.md` | design the thing first, implement later |
| `spec-to-code` | existing spec | merged PR | spec exists, just build it |
| `prompt-to-code` | rough idea | merged PR | end-to-end (most common) |
| `research` | open-ended question | synthesis report | investigate before committing to a design |
| `bugfix` | bug report | merged PR with fix + regression test | reported bug with unknown root cause |
| `review` | PR + feedback | updated PR | address review comments mid-flow |

Each team configuration has its own reference doc under `reference/teams/` describing the exact agents, flow, and review loops.

## Conventions

| | |
|---|---|
| **Linear team** | `RSM` |
| **Linear project** | [Bring Data Liberation into Studio Code](https://linear.app/a8c/project/bring-data-liberation-into-studio-code-8e53bd986fcc) |
| **Ticket ID** | `RSM-<N>` (team-scoped, not project-scoped) |
| **Issue slug** | `rsm-<N>-<short-description>` (e.g. `rsm-123-dark-mode`) |
| **Branch** | same as slug, pushed to `automattic/studio` |
| **Worktree** | `.claude/worktrees/<issue-slug>/` (inside the Studio clone) |
| **Issue folder** | `issues/<issue-slug>/` (committed alongside the code — holds prompt, spec, reviews, PR description, screenshots) |
| **Linear labels** | `team:<config>`, `single-agent`, `*:active`, `*:done` |

## Requirements

- [Claude Code](https://claude.com/claude-code) (opus-class model recommended — the teams all specify `opus`)
- Linear MCP server configured and authenticated, with access to the RSM team and the _Bring Data Liberation into Studio Code_ project
- GitHub CLI (`gh`) authenticated, with access to `automattic/studio`
- A local clone of `automattic/studio` for worktrees and code changes
- Node.js 22+ and `npm` (Studio's package manager)

## Setup

1. Clone this repo into your Claude Code skills directory (or symlink it):
   ```
   git clone https://github.com/Poliuk/rsm-orchestrator.git ~/.claude/skills/orchestrator
   ```
2. Inside your local Studio clone, start Claude Code.
3. Ask Claude to use the orchestrator: _"Use the orchestrator — here's my idea: …"_

Claude will read `SKILL.md` and walk through the right workflow based on what you ask for.

## Usage: the zero-to-PR flow

1. **Describe the idea.** Rough is fine — the orchestrator will help you scope it.
2. **Pick a mode.** Together you decide: single agent or team, and which team config.
3. **Orchestrator creates the Linear ticket** with a short prompt + label.
4. **You pick which ticket to start.** Orchestrator sets up the worktree and spawns agents.
5. **Agents work in the background.** A health-check loop fires every 15 minutes to detect stalls.
6. **Review the PR** when it opens. Small changes → orchestrator tweaks directly; larger → `review` team.
7. **Approve → merge.** Orchestrator merges on GitHub, marks the Linear ticket Done, and removes the worktree.

## File layout

```
.
├── SKILL.md                    ← Claude Code entry point; defines conventions + workflow table
├── README.md                   ← this file
└── reference/
    ├── creating-issues.md      ← how to file a new Linear ticket
    ├── starting-work.md        ← setting up a worktree and launching agents
    ├── resuming-work.md        ← picking up a stalled or interrupted session
    ├── reviewing-work.md       ← handling review feedback
    ├── finishing-work.md       ← merge / abandon / retry
    ├── multiple-attempts.md    ← versioning slugs for parallel retries (`-v2`, `-v3`)
    ├── health-monitoring.md    ← recurring health-check loop for running agents
    ├── launching-a-single-agent.md
    ├── launching-a-team.md
    ├── team-configurations.md  ← index of the six team configs
    └── teams/
        ├── prompt-to-spec.md
        ├── spec-to-code.md
        ├── prompt-to-code.md
        ├── research.md
        ├── bugfix.md
        └── review.md
```

Every workflow doc is designed to be read in full before execution — not recalled from memory. If you edit one, keep it self-contained.

## Credits

Thanks to [@luisherranz](https://github.com/luisherranz) for sharing his original orchestrator, which this one is adapted from — and for his ongoing work on [Radical Pipelines](https://github.com/Automattic/radical-pipelines), a broader take on coordinating AI development work.
