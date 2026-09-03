# Independent review report — T-00042 (priority field + transition hardening)

**Reviewer**: independent reviewing agent (per `docs/mission-agentB-review.md`)
**Reviewed head**: `feature/T-00042-priority-and-transition` @ implementer's final commit
**Scope**: schema, status-transition function, API validation, tests (per mission brief)

## Findings

### MAJOR — status-transition function does not serialize concurrent callers

**Location**: `db/schema/002_status_transition_fn.sql`

**Failure scenario**: two requests both call `set_task_status(task_id, ...)` for
the same task at nearly the same time — for example a user double-clicking a
"start task" button, or a retried request after a slow network response. The
original function reads the current status, checks it's a legal source state, then
writes the new status as two separate statements with no row lock in between. Under
that interleaving, both calls can read the *same* pre-transition status before
either writes, both pass the legality check, and both writes apply — the second
one silently overwriting the first's effect instead of one of the two being
correctly rejected as "no longer a legal transition."

**Evidence**: `db/tests/status_transition_concurrency.sh`, run before the fix,
fires two concurrent `in_progress → done` / `in_progress → todo` calls against the
same row and shows both succeeding when exactly one should.

**Fix applied**: the function now takes the row lock (`SELECT ... FOR UPDATE`) on
the target task before reading its status, so the second concurrent caller blocks
until the first transition commits, then re-reads the now-current status and
correctly rejects its own transition as no longer legal.

### NOTE — concurrency test could assert the exact error more precisely

**Location**: `db/tests/status_transition_concurrency.sh`

The test currently asserts that exactly one of the two concurrent calls succeeds,
which is sufficient to catch the MAJOR finding above, but it does not additionally
assert *which* database error code the losing call receives. Tightening this would
make a future regression easier to diagnose from CI output alone. Non-blocking;
recorded in `docs/STATE.md` rather than fixed in this pass, since it doesn't affect
correctness.

## Checks run

- `npm run lint` — pass
- `npm run typecheck` — pass
- `npm test` — pass (existing suite + new unit test for the rejected-transition case)
- `npm run build` — pass
- `db/tests/status_transition.sql` — pass
- `db/tests/status_transition_concurrency.sh` — failed before the fix (both calls
  succeeded), pass after (exactly one succeeds, the other receives a clean
  rejection)
- CI run on the fixed head: `quality`, `data-integrity`, `e2e` — all green

## Verdict

**PASS WITH RESERVATIONS** — no open critical/major finding; the `NOTE` above is a
non-blocking test-robustness improvement, tracked in `docs/STATE.md` rather than
left silently unrecorded.

## Final state

Fix committed and pushed on `feature/T-00042-priority-and-transition`; `docs/STATE.md`
updated to reflect the `PASS WITH RESERVATIONS` verdict and the open `NOTE`.
