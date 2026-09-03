# AGENTS.md — Codex entrypoint (TaskFlow API)

This file is the entrypoint for Codex on the fictional TaskFlow example project.

## Required reading order

1. `AGENT_RULES.md`
2. `docs/STATE.md`
3. `README.md`

If any of these is missing, inconsistent, or outdated: stop and report it before
changing application code.

## Source of truth

- The Git repository is the source of truth, not chat history.
- Work from the current repository state; do not assume what a previous session did.

## Coordination with other agents

- `AGENT_RULES.md` has priority for anything shared across tools.
- When another agent has already worked on related code, check the latest commits
  before continuing — see `docs/mission-agentA-implement.md` and
  `docs/mission-agentB-review.md` for how implementation and independent review are
  split on this example project.
