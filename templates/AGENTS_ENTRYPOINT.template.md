# AGENTS.md / CLAUDE.md — per-tool entrypoint template

Most agent tools look for their own entrypoint file (for example, an `AGENTS.md`
for one tool and a `CLAUDE.md` for another). Keep each one short and pointing back
at the same shared rules, instead of duplicating the rules themselves — duplication
is exactly how two tools end up following silently different versions of "the rules."

```markdown
# [CLAUDE.md / AGENTS.md] — [Tool name] entrypoint

This file is the entrypoint for [Tool name] on [Project name].

## Required reading order

1. `AGENT_RULES.md`
2. `[PROJECT_STATE.md or equivalent]`
3. `[AI_TOOLING.md or equivalent, if you track installed MCP/Skills/plugins]`
4. `README.md`

If any of these is missing, inconsistent, or outdated: stop and report it before
changing application code.

## Source of truth

- The Git repository is the source of truth, not chat history.
- Work from the current repository state; do not assume what a previous session did.

## Coordination with other agents

- `AGENT_RULES.md` has priority for anything shared across tools.
- Tool-specific instructions here must not contradict it.
- Before continuing related work, check the latest commits for what another agent
  already did.
```

## Why keep these separate from the shared rules file

Each agent tool has its own convention for where it looks for instructions. Having
a thin, tool-specific file that just points to the shared rules (rather than
copying them) means the shared rules only ever have one place to go stale.
