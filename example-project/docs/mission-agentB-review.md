# Mission — independent reviewing agent (TaskFlow: priority field + transition hardening)

## Activation

Starts only after the implementing agent has pushed `feature/T-00042-priority-and-transition`
and written `docs/mission-agentA-report.md`. Start from that remote head, not a
local checkout.

Do not merge the PR.

## Role

Independent reviewer. Do not assume `set_task_status` is correct just because the
functional test passes — a functional test run once, sequentially, does not prove
anything about two callers hitting it at the same time.

## Mandatory startup

1. Read `AGENT_RULES.md`.
2. Read `docs/STATE.md`.
3. Read `docs/mission-agentA-report.md`.
4. Sync the branch; confirm a clean working tree.
5. Read the full diff against `main`.

## Mandatory review scope

- **Schema**: does the new `priority` column have a real constraint (an enum or a
  `CHECK`), or can invalid values slip in through a raw insert?
- **Transition function**: is illegal-transition rejection enforced in the
  database function itself, or only in application code (which a direct DB write
  would bypass)? What happens under two concurrent calls transitioning the same
  task at once — does one silently overwrite the other's effect, or does the
  database guarantee one consistent winner?
- **API**: does the endpoint trust a client-supplied status/priority value, or
  does it go through the same validated path either way?

## Corrections allowed

Only defects actually demonstrated in this scope. Add the test that would have
caught each one.

## Required validation

Real evidence for lint/typecheck/unit/build, plus the data-integrity job
(`db/tests/status_transition.sql`, `db/tests/status_transition_concurrency.sh`) —
including a concurrency scenario that actually fires two transitions at once,
not just two transitions run one after another.

## Output report

Write `docs/review-report-example.md` per the format in the parent portfolio's
`docs/02-independent-review-protocol.md`: starting point, findings ranked by
severity, evidence, fixes applied, and a verdict.

Commit and push the report and any fix, then **stop for final validation**.
