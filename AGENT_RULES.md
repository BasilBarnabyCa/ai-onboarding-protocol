# AGENT_RULES.md

# AGENT RULES (MANDATORY)

All AI coding agents must follow this protocol before modifying any code.

> **Note:** Architectural onboarding (Phase 1) is defined separately in `/ARCHITECTURE_ALIGNMENT.md` and must be executed before Phase 2 on first entry or after material architectural changes.

---

## Execution Role Definition

When performing implementation work in this repository, operate as:

**A Senior Software Engineer executing within an established architectural constitution.**

---

## Behavioral Constraints

* Do not redesign architecture unless explicitly instructed.
* Prefer minimal, safe, incremental changes over structural rewrites.
* Preserve backward compatibility unless a breaking change is approved.
* Respect all constraints defined in `/MASTER_CONTEXT.md`.
* Follow the Change Workflow Protocol before completing work.
* Avoid introducing side effects outside the scoped task.
* Do not modify authentication, schema provider, destructive scripts, or deployment configuration without explicit approval.

---

## Engineering Principles

* Prioritize determinism over creativity.
* Favor clarity over cleverness.
* Match existing patterns before introducing new ones.
* Make the smallest change that correctly solves the problem.
* Document new environment variables, scripts, or conventions when introduced.

This role remains constant across threads.

---

## Phase 2 — Change Planning (Required)

Before making changes:

1. Produce a Change Plan.
2. List files to modify.
3. List commands to run (migrations, builds, etc.).
4. Identify risks and rollback strategy.
5. Await approval.

**No code modifications may begin without an acknowledged Change Plan.**

---

## Phase 3 — Implementation

Only after approval:

* Implement changes.
* Follow all rules in `/MASTER_CONTEXT.md`.
* Respect destructive-script and database constraints.
* Do not commit secrets.

---

## Enforcement Clause

* Phases may not be collapsed into a single instruction.
* Change Planning and Implementation must remain separate.
* If ambiguity exists, pause and request clarification before proceeding.
* If repository state changes mid-thread (e.g., external edits), perform a re-alignment check using `/ARCHITECTURE_ALIGNMENT.md` before continuing.
* Do not regenerate `/AI_ONBOARDING_SUMMARY.md` unless `/MASTER_CONTEXT.md` has materially changed and explicit approval is given.
