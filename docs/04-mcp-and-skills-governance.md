# Pattern: MCP integration and Skills governance

## MCP: authority order

An MCP server (for example, a documentation-lookup server) is a great way to pull
current, accurate library/API documentation into an agent's context instead of
relying on training data that might be stale. But it needs an explicit place in the
decision hierarchy, or an agent can end up treating "what the docs say a library
does" as equivalent to "what this project has decided to do."

The rule applied here:

1. The project's own rules and accepted decisions come first.
2. The project's current recorded state comes second.
3. External documentation (via MCP) is authoritative **only** for the literal
   syntax/behavior of a third-party library or API — never for how *this* project
   chooses to use it.

Concretely: if a library's docs recommend a pattern that conflicts with an accepted
project decision, the conflict gets reported and resolved explicitly — never silently
resolved by just following whichever source was consulted last.

## Skills governance: vet before you trust

A "Skill" (a packaged set of instructions/scripts an agent can load) is code and
instructions written by someone else, running with real capabilities in your
environment. Before adopting one:

1. **Name the exact capability gap.** Not "this looks useful," but "this workflow
   currently has no way to do X."
2. **Check it isn't already covered** by an existing tool, an installed dependency,
   or plain project documentation.
3. **Read the source.** Does it ship executable scripts? What do they actually do?
   Any flagged risk from a scanner gets manually inspected, not dismissed on the
   scanner's word alone and not accepted on the scanner's word alone either.
4. **Prefer the narrowest scope that solves the problem** (a project-local
   installation over a global one, when the capability is project-specific).
5. **Write down what you decided and why** — including the Skills you deliberately
   did *not* adopt, so a future session doesn't re-run the same evaluation from
   scratch or install something already rejected for a documented reason.
6. **A Skill never outranks the project's own rules.** It can add detail; it cannot
   quietly override an accepted architecture, security, or validation requirement.

## Why this matters for orchestration

Both of these are instances of the same principle: an external source of
information or capability is useful precisely because it's independent — but only if
its authority is bounded on purpose, in writing, before you start relying on it.

## See also

- `docs/05-tool-adoption-and-integration.md` for the same governance principle
  applied to a full external tool rather than a single Skill.
