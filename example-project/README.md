# TaskFlow API (fictional example project)

A small, entirely fictional task-management API, built only to demonstrate the
multi-agent workflow described in the parent portfolio's `docs/` folder — running
for real, not just described.

This is not a real product. It exists to show:

- a shared agent-rules file both agents read (`AGENT_RULES.md`);
- a real two-job... three-job CI pipeline that actually runs on GitHub Actions
  (`.github/workflows/ci.yml`);
- a filled-in mission brief for an implementing agent and an independent reviewer
  (`docs/mission-agentA-implement.md`, `docs/mission-agentB-review.md`);
- a filled-in independent review report following the protocol in
  `docs/02-independent-review-protocol.md`, including a defect found by the
  reviewer and its fix (`docs/review-report-example.md`).

## Fictional scenario

TaskFlow lets a team create tasks and move them through a status workflow
(`todo` → `in_progress` → `done`). The example feature below adds a `priority`
field and tightens the status-transition logic against a concurrency edge case —
chosen because it's a realistic, reviewable defect class, not because it maps to
any real system.
