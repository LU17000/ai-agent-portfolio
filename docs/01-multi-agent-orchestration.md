# Pattern: two-agent orchestration with separated responsibilities

## Problem

A single AI agent implementing and then reviewing its own work tends to rubber-stamp
its own decisions: it doesn't second-guess a design choice it just made, and it stops
looking for problems once its own tests pass. On anything sensitive (payments, auth,
data integrity, concurrency), that's not enough evidence that the change is actually safe.

## Pattern

Split the work across two agents (in practice: Claude Code and OpenAI Codex, but the
pattern doesn't depend on which two tools you use) with **strictly separated roles**:

- **Agent A — implementer.** Reads the shared rules, implements the smallest coherent
  change, runs the applicable checks, writes an implementation report, and **stops**.
  It never merges its own work.
- **Agent B — independent reviewer.** Starts only after Agent A has pushed and
  written its report. Reads the same shared rules plus Agent A's report, but does
  **not** assume the implementation or its tests are correct just because they pass.
  It actively looks for what could slip through the existing tests: missing
  constraints, race conditions, authorization gaps, silent fallbacks. It writes an
  independent review report with a verdict (see
  `02-independent-review-protocol.md`) and, if it makes corrections, documents them
  separately from Agent A's work.

## Why the strict handoff matters

- **No parallel work on the same surface.** Agent B never starts until Agent A has
  fully finished and pushed — otherwise you get two agents editing the same files
  from diverging states, which is worse than no review at all.
- **No self-certification.** The agent whose reasoning produced the design is not
  the one deciding whether that reasoning was sound.
- **A single source of truth for both agents.** Both read the *same* shared rules
  file and the *same* repository state — not each other's chat history. See
  `templates/AGENT_RULES.template.md`.
- **A recorded handoff, not a verbal one.** Each mission has a written brief
  (`templates/mission-implementer.template.md`,
  `templates/mission-reviewer.template.md`) and a written report. Anyone — a human,
  or a third agent picking up the work later — can reconstruct what happened without
  replaying a conversation.

## What this pattern is not

- It is not real-time, concurrent multi-agent collaboration. The two agents never
  work on the same branch at the same time.
- It does not replace human review for genuinely high-stakes changes — it raises the
  floor before a human looks at it, it doesn't remove the human.

## See also

- `example-project/docs/mission-agentA-implement.md` and
  `example-project/docs/mission-agentB-review.md` for a filled-in instance of this
  pattern on a fictional project.
- `case-studies/two-agent-review-cycle.md` for a narrative account of one full cycle.
