# Case study: adopting a third-party automation tool into an existing agent workflow

**Context**: a private software project (not named here), already running the
two-agent implementer/independent-reviewer workflow described in
`docs/01-multi-agent-orchestration.md`.

## The gap

The existing workflow already split implementation and independent review across
two agent tools, but starting the second pass still depended on a human noticing
that the first agent had finished and manually kicking off the review. On a
project with intermittent availability, that created delay between "implementation
done" and "reviewed" — and an easy point for the review step to simply get skipped
under time pressure.

## Evaluating a candidate tool

A third-party orchestration tool was identified (through an external
recommendation, not built in-house) that could drive both agent tools through an
iterate-then-review loop automatically. Before adopting it:

- The gap was named precisely (automating the *handoff*, not replacing the review
  itself — the independent-review protocol and its verdict format stayed exactly
  as they were).
- The tool's configuration surface was read in full before turning anything on.
- It was installed at project scope, not globally, since the need was specific to
  this one workflow.

## Configuring it conservatively

Rather than accepting defaults, explicit bounds were set before trusting it with
anything: a cap on how many iterations it could run unattended, a session and idle
timeout so nothing could run indefinitely, and isolation — every run works in its
own dedicated workspace, never directly on the project's primary working copy. It
was also confined to a separate clone of the repository entirely, so a
misconfiguration in the orchestrator could never touch the working copy actually
used for day-to-day development.

The most important rule, applied from the start and never relaxed: the tool is
**only ever started by an explicit human decision**. No agent following the
project's shared rules is permitted to launch it on its own initiative, and it is
never pointed at anything other than its own dedicated, isolated checkout.

## Outcome

The tool now automates the mechanical part of the handoff — kicking off the
independent review once the implementer has actually finished — while every rule
that mattered before adopting it (independent review, verdict format, evidence
requirements, no self-certification) stayed exactly in place. Its output is
reviewed and validated by the same standard as any other agent's contribution; a
clean run from the tool is not, by itself, treated as proof that a change is
correct.

## What this demonstrates

- Recognizing a real gap in an existing workflow, distinct from wanting to
  automate for its own sake.
- Evaluating and integrating a third-party tool without letting it inherit
  unattended authority it wasn't given on purpose.
- Keeping a human decision point on anything that can drive other agents or touch
  a working environment, even after the tool is trusted for routine use.
