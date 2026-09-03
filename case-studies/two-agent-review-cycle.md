# Case study: a two-agent review cycle catching a concurrency defect

**Context**: a private software project (not named here), developed with two AI
coding agents working in the implementer/independent-reviewer split described in
`docs/01-multi-agent-orchestration.md`.

## What happened

A feature added an administrative action that could change a record's state based
on its current state — the kind of "promote this to primary" or "transition this to
the next stage" operation that reads a row, checks it's currently valid to change,
and then writes the new state. The implementing agent built it, wrote functional
tests, and all of them passed.

The independent reviewer did not stop there. Instead of trusting the passing
functional test — which only ever exercised one call at a time — it asked what
would happen if the same action fired twice at once for the same record: two
requests, or one request retried after a slow response. Working through the
function's actual statements, it found that the read-check-write sequence had no
lock in between, so two concurrent callers could both read the same starting state,
both pass the validity check, and both write — with the second one silently
overwriting the first's effect instead of being correctly rejected.

## Resolution

The fix added a row lock at the read step, so a second concurrent caller blocks
until the first transition commits, then re-reads the now-current state and
correctly rejects its own change as no longer valid. A new test was added that
fires two real concurrent calls against the same record (not two sequential calls)
and asserts that exactly one succeeds — the test that would actually have caught
the original defect. Both the original review report and the project's live status
document recorded the finding, the fix, and the review verdict, tied to the actual
CI run that proved it.

## What this demonstrates

- A second, independent pass finds a class of defect (a race condition) that a
  single agent's own functional tests structurally cannot catch, because it wasn't
  looking for one at all.
- The review protocol's requirement for a *concrete failure scenario*, not just "this
  seems risky," is what turned a vague concern into a specific, reproducible test.
- The fix and the test that proves it were written together, not as an
  afterthought — the review report wasn't considered closed until both existed and
  the CI evidence backed the verdict.

See `example-project/docs/review-report-example.md` for a fully worked, fictional
version of the same defect class end to end.
