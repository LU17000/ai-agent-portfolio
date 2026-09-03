# Pattern: hooks as an automated safety net, mirrored across agent tools

## Problem

An agent can be told, in writing, to always check something after editing a file —
and forget, especially several turns into a long session. Instructions in a rules
document are read once at the start; they are not enforced.

## Pattern

Wire the check into the tool-use lifecycle itself, so it runs whether or not the
agent "remembers" to ask for it:

- **`PostToolUse`** — right after an edit/write, run a fast, narrow check scoped to
  the kind of file that just changed (for example: a UI file just got touched, so
  run a lightweight consistency check against the project's design conventions).
  This has to be fast — a few seconds at most — since it fires on every relevant edit.
- **`Stop`** — when the agent is about to end its turn, run a deeper pass over
  everything that changed in the session. This can afford to take longer since it
  runs once, not per edit.

See `examples/claude-settings.example.json` and `examples/codex-hooks.example.json`
for the actual hook configuration shape (fictional script path, no project-specific
content).

## Why mirror the same hook across two different agent tools

If Agent A and Agent B are both allowed to touch the same kind of file, the check
has to fire for both, or the guarantee only holds half the time. Each tool has its
own hook configuration format and its own place to declare it, but the underlying
check (the actual script) is the same file, referenced from both configs. That's the
detail that makes "the same discipline, enforced consistently across tools" true
rather than aspirational.

## What the hook should (and shouldn't) do

- It should be **fast and narrow** for the per-edit trigger, and can be **broader
  and slower** for the end-of-turn trigger.
- It should **fail loud, not silent** — a hook that swallows its own errors is worse
  than no hook, because it creates false confidence.
- It should **not** replace the project's actual test suite or CI. A hook is a
  fast, local nudge during the session; the committed test suite is what actually
  gates merging.

## See also

- `docs/06-risk-gating-pattern.md` for the complementary pattern that governs
  *irreversible* actions, which hooks alone cannot safely gate.
