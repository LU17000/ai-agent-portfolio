# Case Study — Designing a Controlled Multi-Agent Software Development Workflow

*Personal R&D prototype · Experimental · Anonymized account*

## Vision

The long-term goal is to turn a software idea expressed in natural language into a functional, tested, deliverable application with minimal human intervention.

This is the **goal**, not a claim that fully autonomous idea-to-product delivery has been achieved. The present project investigates the smaller, verifiable steps needed to make this possible.

## Challenge

AI coding agents can generate and modify software, but combining them into a dependable development process introduces failure modes: a model can claim success without sufficient evidence, validate an outdated revision, repeat a remote action after a crash, or advance beyond an authorization boundary.

The challenge was to turn a collection of agent interactions into a controlled workflow with independent checks, recoverable progress, and human oversight.

## Approach

The prototype separates model-driven implementation from deterministic workflow control:

1. Assign bounded implementation work to coding agents, including Claude Code and Codex.
2. Run defined checks and request independent review.
3. Route findings back into a constrained correction cycle.
4. Recheck the resulting changes and verify evidence against the expected revision.
5. Require explicit authorization for sensitive operations and preserve sufficient state to resume after interruptions.

Third-party coordination and model tools are integrated components, not claimed as original inventions.

## Implemented mechanisms

The inspected prototype contains code and targeted tests for:

- **Orchestration and bounded remediation:** implementation, review, correction, and repeat validation under explicit limits.
- **Independent assessment:** separation between implementation participants and a distinct final reviewing stage.
- **Commit-specific CI verification:** checks for matching repository, revision, workflow, run attempt, and required jobs rather than accepting an agent's declaration of success.
- **Recovery:** persisted mission state and handling of interrupted or uncertain operations.
- **Human authorization:** controls bound to specific actions and relevant conditions.
- **Execution boundaries:** container-based isolation and checks on agent execution.
- **Controlled delivery:** steps for repository integration and review, not deployment of a production application.

## Validation and observed results

Automated tests with controlled actors cover a review rejection followed by correction and new checks, as well as recovery, authorization, and stale-evidence scenarios.

Project documentation records limited live trials with real coding agents on disposable repositories. Some runs reached review-ready or controlled delivery states, but also required troubleshooting and corrections. These trials should not be interpreted as sustained unattended operation.

Certain GitHub CI checks passed for specific revisions; these results do not certify subsequent local changes or the overall system.

The key demonstrated principle is that **an agent reporting success is not the same as independently verified completion**.

## My role and tool attribution

I defined the project's objective and guided the system's design, operating rules, acceptance criteria, and review priorities. I supervised AI-assisted implementation and validation, with Claude Code, Codex, and other integrated tools participating in execution and review.

This describes a project-owner and AI-systems-design role; it does **not** claim that I manually authored all underlying code.

## Limitations

- Experimental prototype; not production-ready.
- Full idea-to-finished-product autonomy remains an objective, not a validated capability.
- Deterministic automated test coverage is broader than evidence from repeated real-model trials.
- Isolation and permission checks mitigate specific risks but are not a security certification.
- No verified productivity, cost-saving, or broad reliability metrics are claimed.
- A complete public reproduction is not provided; the private source and infrastructure remain confidential.

## Skills illustrated

AI systems design; multi-agent orchestration; AI-assisted development workflows; independent review; CI evidence validation; failure recovery; human-in-the-loop authorization; bounded automation; integration testing; technical documentation.

---

**Evidence note:** This is an anonymized summary informed by inspection of a private experimental project and its tests. It contains no private source code, internal paths, secrets, or proprietary architecture. Detailed original evidence is not published here.
