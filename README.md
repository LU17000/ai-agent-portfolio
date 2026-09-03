# AI Agent Portfolio

This repository documents methods and patterns for working with AI coding agents
(Claude Code, OpenAI Codex, and similar tools): multi-agent orchestration, hooks,
MCP integration, Skills governance, CI design, and independent-review protocols.

It accompanies my CV for roles involving AI agents, automation, and AI orchestration.

## Why this repository exists

Most of what I actually know about building reliable agentic workflows comes from
working, day to day, on a private software project. That codebase and its business
details are confidential and are **not** part of this repository. What *is* shareable
is the method: how the agent rules were written, how two agents divide work and
review each other, how hooks and CI enforce discipline automatically, and how
tool/Skill adoption is vetted before it's trusted.

Every file here is either a **generic, reusable template** or a **fictional example
project** built specifically for this portfolio. Nothing is copied from any private
codebase, and no proprietary architecture, roadmap, or business logic is disclosed.

## What's in this repository

| Path | Content |
|---|---|
| `docs/` | Written explanations of each pattern: orchestration, review protocol, hooks, MCP/Skills governance, tool adoption, risk gating. |
| `templates/` | Copy-paste-ready generic templates: shared agent rules, mission briefs, PR template, CI workflow, risk queue. |
| `examples/` | Minimal, fictional configuration snippets (hook config for two different agent tools). |
| `example-project/` | A small fictional project ("TaskFlow API") that runs the full workflow end to end: shared rules, two-agent mission briefs, a real CI workflow, an independent review report. |
| `case-studies/` | Short, anonymized narratives describing how these patterns played out in practice. |

## Skills demonstrated

- **Multi-agent orchestration**: splitting work between an implementing agent and an
  independent reviewing agent, with a formal handoff protocol and a no-merge-before-review rule.
- **Independent review & validation procedures**: a review report format with a
  strict verdict taxonomy (`PASS` / `PASS WITH RESERVATIONS` / `FAIL`), backed by
  reproducible CI evidence rather than self-reported success.
- **Hooks**: automated checks wired into an agent's tool-use lifecycle
  (`PostToolUse`, `Stop`), applied consistently across two different agent tools.
- **MCP integration**: bringing an external documentation/context server into an
  agent's workflow with an explicit authority order (external docs inform syntax,
  never override project decisions).
- **Skills governance**: a vetting checklist applied before trusting a third-party
  Skill (source review, permissions, executable scripts, actual capability gap).
- **Tool adoption and integration**: identifying a relevant third-party tool,
  adding it to a working environment, configuring it conservatively, and wiring it
  into an existing multi-agent workflow without giving it unattended authority.
- **CI design**: multi-job pipelines covering lint/typecheck/unit tests/build, a
  data-integrity job against an ephemeral database (schema constraints,
  concurrency behavior), and an end-to-end browser test job.
- **Git/GitHub discipline**: branch naming conventions, commit message conventions,
  a structured PR template, and explicit anti-destructive-action rules.
- **Risk gating for agentic workflows**: a queue for irreversible or sensitive
  actions that an agent must document but never execute without explicit human
  approval.

## What this is not

- Not a claim of a shipped, live production system.
- Not a security audit or penetration test.
- Not a disclosure of any private project's code, schema, architecture, or roadmap.

## Where to start

1. Read `docs/01-multi-agent-orchestration.md` and `docs/02-independent-review-protocol.md`
   for the core pattern.
2. Look at `example-project/` to see the pattern actually running (real CI, real
   mission briefs, a real review report) on a fictional codebase.
3. Read `case-studies/` for how this played out on a real (but unnamed) project.
