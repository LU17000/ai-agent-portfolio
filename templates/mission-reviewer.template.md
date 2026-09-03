# Mission template — independent reviewing agent

## Activation

This mission starts **only after** the implementing agent has finished, pushed, and
written its report. Start from the final remote state, never from an older local
checkout.

Do not merge any pull request.

## Role

You are acting as **independent reviewer and targeted corrector**. Do not assume the
implementation, or its passing tests, are correct just because they exist. Actively
look for what the existing checks could miss.

## Mandatory startup

1. Read `AGENT_RULES.md`.
2. Read the current project-state document.
3. Read the implementer's report.
4. Read whatever design/requirements documents apply.
5. Sync the branch with the remote; confirm a clean working tree.
6. Examine the full diff against the base branch, not just the summary.

## Mandatory review scope

`[Adapt to the task, e.g.:]`
- Data model / schema: missing or contradictory constraints, states that should be
  impossible but are still representable, migration safety.
- Access control: what an unauthorized actor could read or write that they
  shouldn't be able to.
- Application logic: server-authoritative values, error handling, silent fallback
  paths, race conditions on concurrent writes.
- CI / operational: whether the pipeline actually proves what the report claims.
- Documentation: whether the project-state document matches the real code.

## Corrections allowed

- Fix only demonstrated defects directly related to this task's scope.
- Add the test that would have caught each defect fixed.
- Do not refactor by preference, change architecture, or add unrelated features.

## Required validation

Obtain real evidence (not assumptions) for every check that applies. If nothing
needed to change, still verify the last CI run on the reviewed head.

## Output report

Write `[review report path]` per the format in
`docs/02-independent-review-protocol.md`: starting point, scope covered, findings
ranked `CRITICAL`/`MAJOR`/`MINOR`/`NOTE` with evidence, checks run, untested limits,
and a verdict — `PASS`, `PASS WITH RESERVATIONS`, or `FAIL`.

A `PASS` is only valid if no open critical/major finding remains in scope.

Commit and push the report and any corrections, then **stop for final validation**.
