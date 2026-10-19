# AGENT_RULES.md — TaskFlow API

Filled-in instance of `templates/AGENT_RULES.template.md` for the fictional
TaskFlow example project.

The procedures below illustrate rules for a hypothetical implementation. They do
not indicate that TaskFlow application code or tests are included, or that the
procedures have been executed.

## Mandatory startup procedure

Before changing anything, every agent must:

1. Read `README.md`.
2. Read `docs/STATE.md` (current status of TaskFlow's fictional milestones).
3. Check the current branch and working tree state.
4. Sync with the remote before starting new work.
5. Identify the exact task and avoid unrelated changes.

## Development workflow

1. Understand the requirement.
2. Inspect the existing task/status model and its tests.
3. Define a bounded plan.
4. Implement the smallest coherent change.
5. Run `npm run lint`, `npm run typecheck`, `npm test`, `npm run build`.
6. Diagnose failures at the root cause.
7. Re-run checks.
8. Update `docs/STATE.md` if the real status changed.
9. Commit with a clear, scoped message.
10. Push.

## Validation rule

A task is not "done" because code was written. Passing tests, a passing build, and
passing lint/type checks are the minimum bar; anything not actually checked must be
stated as such.

## Change discipline

- Do not touch unrelated parts of the task model while fixing a status-transition
  bug.
- Do not change the storage engine or framework choice without recording the
  decision.
- Never commit secrets or real user data (this is a fictional project — there is
  none, and it stays that way).

## Sensitive-change rule

Anything touching concurrent status transitions requires a second, independent
agent review before being marked validated — see `docs/mission-agentB-review.md`.
