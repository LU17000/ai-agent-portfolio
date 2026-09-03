# Pattern: adopting and integrating a third-party tool into an existing agent workflow

This is a general note on a recurring skill: recognizing that a capability gap
exists, finding a tool that closes it, and folding it into a workflow that already
has its own rules — without letting the new tool quietly take over decisions that
belong to the project or to a human.

## The process

1. **Identify the gap precisely.** Not "we should automate more," but a specific,
   named limitation of the current workflow (for example: two agents currently
   review each other's work only when a human remembers to trigger the second pass).
2. **Evaluate candidates against the existing stack first.** Check whether an
   already-adopted tool, a scriptable CI step, or a small custom script closes the
   gap before reaching for a new dependency.
3. **Add it deliberately, at the right scope.** Install/configure it for the project
   that needs it rather than globally, unless the capability is genuinely
   environment-wide.
4. **Configure it conservatively before trusting it.** Concretely, this means
   setting explicit, cautious bounds rather than accepting defaults: a cap on how
   many iterations or retries it can run unattended, a session/idle timeout so
   nothing runs indefinitely, and isolation (a dedicated worktree or environment)
   so the tool never operates directly on a shared working copy.
5. **Wire it into the existing rules, not around them.** The tool's output is
   subject to the same review, testing, and documentation requirements as any other
   contribution — its own confidence in its result doesn't count as validation.
6. **Never let it self-trigger.** A tool that can drive other agents or make
   changes is only ever started by an explicit, human decision — never launched
   automatically by another agent's own initiative, and never pointed at the
   project's primary working copy directly.
7. **Document the decision**, including the configuration values chosen and why,
   so the next person (or session) doesn't have to re-derive them from scratch or
   accidentally loosen a bound that was set on purpose.

## The underlying skill

This is the same evaluation discipline as `docs/04-mcp-and-skills-governance.md`,
scaled up to a full external tool that can itself drive other agents: identify the
gap, check for overlap, inspect before trusting, scope narrowly, bound it
conservatively, keep a human in the loop for anything irreversible, and write down
what was decided.

## See also

- `case-studies/tool-integration-case-study.md` for a narrative account of applying
  this process to a real (unnamed) third-party automation tool.
