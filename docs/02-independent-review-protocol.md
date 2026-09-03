# Pattern: independent review protocol with a strict verdict taxonomy

## Problem

"Looks good to me" is not evidence. Without a forced format, a review degenerates
into a vague thumbs-up, and a task gets marked done because code was written and
some tests happened to pass — not because anyone checked it was actually correct.

## Pattern

Every independent review produces a written report with the same structure,
regardless of who (or what) is reviewing:

1. **Exact starting point** — the commit/branch state the review actually looked at,
   never "the general direction of recent changes."
2. **Scope actually covered** — schema/data model, access control, application
   logic, CI/operational concerns, documentation accuracy — whatever applies to the
   change.
3. **Findings, ranked by severity** — `CRITICAL` / `MAJOR` / `MINOR` / `NOTE`. Each
   finding names the exact location, the concrete failure scenario (not just "this
   looks risky"), the evidence, and the fix if one was applied.
4. **Real evidence, not claims.** A check that could not actually be run locally
   must be stated as not run — never presented as if it passed. A "PASS" without
   reproducible evidence (a CI run, a test log) doesn't count as a PASS.
5. **A verdict**, one of exactly three values:
   - `PASS` — no open critical or major finding in scope.
   - `PASS WITH RESERVATIONS` — no blocking finding, but a known non-blocking gap is
     explicitly recorded (e.g. a test that could be more precise, a case deferred on
     purpose) so it doesn't quietly get forgotten.
   - `FAIL` — at least one open critical or major finding. A `FAIL` triggers a
     remediation pass, tracked as its own follow-up, not silently reopened as if the
     original review never happened.
6. **Final state** — the commit/branch after any corrections the reviewer made
   directly (scoped strictly to the defects it found — never a drive-by refactor).

## Why the taxonomy is strict

A three-way, closed vocabulary is deliberate: it prevents both false confidence
("basically fine") and endless hedging ("mostly okay but..."). If the reviewer can't
honestly pick one of the three words, that itself is a signal the review isn't
finished.

## Escalation on FAIL

A `FAIL` verdict does not get overwritten quietly. In practice this means: the
project's live status document names the `FAIL` explicitly, a remediation plan is
written down as its own artifact, and the next review only earns a `PASS` once every
finding it lists has actually closed — not once a fix "seems" to address it.

## See also

- `example-project/docs/review-report-example.md` — a filled-in example, including
  a `FAIL`-to-`PASS` remediation cycle on a fictional concurrency defect.
- `templates/mission-reviewer.template.md` for the brief that sets this protocol up
  before the review starts.
