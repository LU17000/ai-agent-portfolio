# Pattern: a risk queue for irreversible actions

## Problem

Some actions an agent might take are hard or impossible to undo cleanly: writing
real data to a shared remote environment, sending a real email/notification,
deleting something, rotating a credential, deploying to a live target. An agent
that's otherwise doing good, well-tested work can still cause real damage by
executing one of these on its own initiative, with good intentions and a plausible
justification.

## Pattern

When an agent identifies a sensitive or irreversible action while working:

1. It does **not** execute it.
2. It records it as a new entry in a dedicated, versioned queue, with:
   - a unique, never-reused identifier;
   - the exact action it would take, precisely enough that a human can approve or
     reject it without having to reverse-engineer the intent;
   - why it's risky (what a mistake here would actually cost);
   - its prerequisites and current status (`PENDING`, `READY` — prerequisites met,
     waiting only on human approval and execution — `BLOCKED`, or `DONE`);
   - any dependency on another queued action.
3. It **continues with the rest of its safe, independent work** instead of stalling
   the whole task on that one action.
4. A human reviews the queue and approves entries individually — the queue is never
   auto-approved in bulk, and an approval for one entry doesn't extend to another.
5. Once executed, the entry is marked done and cross-referenced into the project's
   normal state/validation records, but kept in the queue as history rather than
   deleted — so the decision trail survives.

## Why this is better than "just ask before anything risky"

A blanket "ask a human before anything sensitive" rule tends to either interrupt
constantly (and get rubber-stamped out of fatigue) or get silently narrowed in
practice. A named, written queue with a stable identifier does two things a verbal
check-in doesn't: it forces the agent to state precisely what it wants to do and
why, and it gives the human a durable, reviewable record instead of a one-off
chat approval that's gone once the conversation scrolls past it.

## See also

- `templates/risk-queue.template.md` for a ready-to-use version of this queue.
