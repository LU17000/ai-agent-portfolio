# Mission — implementing agent (TaskFlow: priority field + transition hardening)

## Role

Acting as **primary implementer** on `T-00042 — add task priority + harden the
status-transition function`.

Do not merge the PR. Do not start a parallel review pass.

## Mandatory startup

1. Read `AGENT_RULES.md`.
2. Read `docs/STATE.md`.
3. Sync `feature/T-00042-priority-and-transition` with the remote.
4. Confirm the working tree is clean.

## Objective

1. Add a `priority` column (`low` / `normal` / `high`) to `tasks`, defaulting to
   `normal`, exposed through the API and the task list UI.
2. The existing `set_task_status(task_id, new_status)` database function must
   reject any transition that isn't `todo → in_progress`, `in_progress → done`, or
   `in_progress → todo`. Done is terminal.

## Scope

- `db/schema/001_tasks.sql`, `db/schema/002_status_transition_fn.sql`
- `src/domain/tasks/*`
- `src/api/tasks/*`
- Corresponding tests.

## Out of scope

- Any UI redesign beyond exposing the new field.
- Notification/webhook behavior on status change (separate task).

## Required validation

- `npm run lint`
- `npm run typecheck`
- `npm test`
- `npm run build`
- `db/tests/status_transition.sql` and `db/tests/status_transition_concurrency.sh`
  against a local PostgreSQL instance.

## Output report

Write `docs/mission-agentA-report.md` with: starting commit, files changed, checks
run and results, and the final commit. Commit, push, then **stop and hand off to
the independent reviewer**.
