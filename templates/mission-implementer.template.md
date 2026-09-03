# Mission template — implementing agent

## Role

You are acting as **primary implementer** on `[TASK ID / short description]`.

Do not merge any pull request. Do not start a parallel review pass yourself.

## Mandatory startup

1. Read `AGENT_RULES.md`.
2. Read the current project-state document.
3. Read whatever design/requirements documents apply to this task.
4. Sync the working branch with the remote.
5. Confirm the working tree is clean before changing anything.

## Objective

`[State the exact, bounded objective. Name what "done" looks like concretely.]`

## Mandatory scope of work

`[List the specific areas to touch: data model, access rules, application logic,
UI, CI — whatever applies. Be as concrete as the real task requires.]`

## Out of scope

- Changing the technology stack, providers, or previously accepted architecture
  decisions.
- Work belonging to a later, unrelated task.
- Creating real external state (accounts, remote environments, real data) without
  going through the risk-queue process first.

## Required validation before reporting done

Run and report the real result of:

- `[lint command]`
- `[typecheck command]`
- `[unit test command]`
- `[build command]`
- `[e2e test command, if applicable]`

Anything that could not actually be run locally must be stated as not run — never
reported as passing without evidence.

## Output report

Write `[report path]` containing: starting commit, files inspected/changed, defects
found and fixed (if any) ranked by severity, checks actually run and their results,
known remaining risks, and the final commit/branch state.

Commit and push everything, then **stop and hand off to the independent reviewer**.
