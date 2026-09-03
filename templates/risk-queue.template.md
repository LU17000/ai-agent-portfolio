# RISKY_ACTIONS.md — queue of sensitive/irreversible actions awaiting human approval

## Role

This is the official queue of sensitive or irreversible operations identified
during development, but **deliberately not executed** by an AI agent. Each entry
must be picked up individually by the project owner before execution.

An agent that identifies a new sensitive action creates or updates its entry here,
**does not execute it**, and continues with the rest of its safe, independent work.

## Convention

Identifiers: `RISK-001`, `RISK-002`, etc. An assigned identifier is never reused.

Allowed statuses:

- `PENDING` — identified, not all prerequisites met yet.
- `READY` — prerequisites met, only waiting on human approval and execution.
- `BLOCKED` — depends on an external decision or unavailable input.
- `DONE` — executed with the owner's approval (move the outcome into the project's
  normal state/validation records, but keep this entry as history rather than
  deleting it).

---

## RISK-001 — [Exact action name]

**Milestone**: `[e.g. M-003]`
**Status**: `PENDING`

**Exact action**: `[State precisely what would be executed — e.g. "run an import
script that writes N rows to the remote staging database"]`.

**Why it's risky**: `[What a mistake here would actually cost — wrong data written,
an irreversible deletion, a real notification sent to a real recipient, etc.]`

**Possible impact**: `[Best-case and worst-case outcome if this goes wrong.]`

**Prerequisites**: `[What must be true/tested/approved before this can move to
READY.]`
