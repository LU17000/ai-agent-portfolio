# AGENT_RULES.md — shared operating rules template

This is a generic template for a rules file that every AI agent (Claude Code,
Codex, or any other) reads before touching a repository. Fill in the bracketed
sections for your project. Keep it short enough that an agent actually reads it in
full at the start of a session.

## Purpose

This file defines the common operating rules for every AI assistant contributing to
`[PROJECT NAME]`. The Git repository, not conversation history, is the source of
truth.

## Mandatory startup procedure

Before changing anything, every agent must:

1. Read `README.md`.
2. Read `[PROJECT_STATE.md or equivalent]`.
3. Check the current branch and working tree state.
4. Sync with the remote before starting new work.
5. Identify the exact task and avoid unrelated changes.

Unexpected uncommitted changes are never discarded or overwritten without explicit
authorization.

## Development workflow

1. Understand the requirement.
2. Inspect existing implementation and documentation.
3. Define a bounded plan.
4. Implement the smallest coherent change.
5. Run the applicable checks.
6. Diagnose failures at the root cause rather than working around them.
7. Re-run checks.
8. Update documentation if the project's real state changed.
9. Commit with a clear, scoped message.
10. Push so other agents/sessions see the same state.

## Validation rule

A task is not "done" because code was written. Completion requires evidence
appropriate to its scope: passing tests, a passing build, passing lint/type checks,
manual verification when relevant, and an explicit note of anything left unverified.

## Change discipline

- Do not rewrite unrelated areas while handling a narrow task.
- Do not silently change dependencies, providers, or major architecture choices —
  record the decision instead.
- Never commit secrets, credentials, or real user/customer data.

## Git discipline

- Clear, scoped commit messages; no force-push on shared branches without explicit
  authorization; no deleting branches/history/files just to make something pass.

## Agent handoff

At the end of a session, update the project's state document so the repository is
understandable without relying on the conversation that produced the work: current
status, known issues, validation status, next recommended task.

## Conflict rule

If a tool-specific instruction conflicts with this document, the conflict is
reported and resolved explicitly — never silently resolved by picking one version.
