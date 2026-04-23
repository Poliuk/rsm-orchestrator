# Team Configurations

Each configuration defines a specific set of agents and a flow.

- **`prompt-to-spec`** (`reference/teams/prompt-to-spec.md`) — from rough idea to reviewed spec. Launches an inquisitor/researcher pair to clarify requirements, then a spec-writer and spec-reviewer. Produces a `spec.md` that can later be used with `spec-to-code`.
- **`spec-to-code`** (`reference/teams/spec-to-code.md`) — from existing spec to merged PR. A planner breaks the spec into `[code]` and `[docs]` tasks, implementers build code (TDD), a code-reviewer verifies, documentators write docs, and a doc-reviewer verifies docs and writes the PR description.
- **`prompt-to-code`** (`reference/teams/prompt-to-code.md`) — from rough idea to merged PR. Combines `prompt-to-spec` and `spec-to-code` into a single flow: requirements → spec → plan → code implementation → code review → documentation → doc review → PR.
- **`research`** (`reference/teams/research.md`) — investigate an open-ended question. A persistent research lead plans tasks, researchers execute them (codebase, web, experiments, browser tests), and the lead iterates until done and writes a final synthesis report.
- **`bugfix`** (`reference/teams/bugfix.md`) — investigate and fix a reported bug. An investigator reproduces the bug and finds the root cause, then a planner creates `[code]` and `[docs]` tasks, implementers fix code (TDD), code-reviewer verifies, documentators update docs if needed, and a doc-reviewer verifies docs and writes the PR description.
- **`review`** (`reference/teams/review.md`) — address review feedback on an existing PR. The orchestrator creates `[code]` and `[docs]` tasks from the owner's requested changes, implementers and documentators handle them, and code-reviewer and doc-reviewer verify.
