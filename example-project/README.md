# TaskFlow API (fictional example project)

TaskFlow API is a fictional task-management scenario illustrating the multi-agent
workflow described in the parent portfolio's `docs/` folder. This directory
contains documentation and example configuration, not application code or executable tests.

This is not a real product. It exists to show:

- a shared agent-rules file both agents read (`AGENT_RULES.md`);
- a proposed three-job GitHub Actions workflow (`.github/workflows/ci.yml`)
  showing quality, data-integrity and browser-test checks; no successful execution
  is evidenced in this repository;
- a filled-in mission brief for an implementing agent and an independent reviewer
  (`docs/mission-agentA-implement.md`, `docs/mission-agentB-review.md`);
- an illustrative independent review report showing how to document a hypothetical
  concurrency defect, proposed fix, required checks and qualified verdict
  (`docs/review-report-example.md`).

## Fictional scenario

In the fictional scenario, TaskFlow would let a team create tasks and move them
through a status workflow (`todo` → `in_progress` → `done`). The mission briefs
specify a `priority` field and a concurrency-related status-transition fix.
These are requirements for an illustrative engineering task, not features of an
implemented API included in this repository.
