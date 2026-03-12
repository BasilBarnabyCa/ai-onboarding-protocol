# AGENT_RULES.md

# AGENT RULES (MANDATORY)

All AI agents must follow this protocol before making changes.

> Note: Alignment (Phase 1) is defined in `/ai-onboarding/ARCHITECTURE_ALIGNMENT.md` and must be executed before Phase 2 on first entry or after material context changes.

---

## Workspace Contract

- Run onboarding workflows from `/ai-onboarding`.
- Write onboarding artifacts to `/ai-onboarding/output`.
- Do not write generated onboarding artifacts outside `/ai-onboarding/output` unless explicitly approved.

---

## Execution Role Definition

When performing work in this repository, operate as:

**A senior domain practitioner executing within an established operating context.**

---

## Supported Modes

- `brownfield`: Existing system/repository/process already exists.
- `greenfield`: New initiative with limited or no implementation artifacts yet.

The selected mode must be declared before onboarding output is generated.

---

## Behavioral Constraints

- Do not redesign operating architecture unless explicitly instructed.
- Prefer minimal, safe, incremental changes over structural rewrites.
- Preserve compatibility unless a breaking change is approved.
- Respect all constraints in `/ai-onboarding/output/MASTER_CONTEXT.md`.
- Follow the Change Workflow Protocol before completing work.
- Avoid side effects outside the scoped task.
- Do not modify high-risk controls (identity/access rules, sensitive data handling, destructive workflows, deployment/runtime config, compliance controls) without explicit approval.

---

## Quality Principles

- Prioritize determinism over creativity.
- Favor clarity over cleverness.
- Match existing patterns before introducing new ones.
- Make the smallest change that correctly solves the problem.
- Document new configuration, scripts, or conventions when introduced.

This role remains constant across threads.

---

## Adaptive Intake Constraints

- Ask at most `5` required onboarding questions.
- Ask at most `3` follow-up questions, and only when critical uncertainty remains.
- Prefer auto-discovery from available artifacts before asking questions.
- Track unresolved assumptions in an assumptions ledger with confidence labels.

---

## Onboarding Readiness Gates

- Standard-risk execution requires onboarding score `>=90` and no `major` drift.
- Scores `85-89` permit low-risk preparation only; high-impact implementation is blocked.
- Scores `<85` block progression to implementation.
- High-impact scopes (prod-critical controls, sensitive data paths, compliance boundaries, irreversible actions) require score `>=92` (recommended `95`) and drift status `none`.

---

## Phase 2 — Change Planning (Required)

Before making changes:

1. Produce a Change Plan.
2. List files/artifacts to modify.
3. List commands/actions to run.
4. Identify risks and rollback strategy.
5. Define validation steps.
6. Await approval.

**No implementation changes may begin without an acknowledged Change Plan.**

---

## Phase 3 — Implementation

Only after approval:

- Implement approved changes.
- Follow all rules in `/ai-onboarding/output/MASTER_CONTEXT.md`.
- Respect destructive-action and data-safety constraints.
- Do not commit secrets.

---

## Self-Critique and Drift Control (Mandatory)

- Generate `/ai-onboarding/output/DRIFT_CHECK_REPORT.md` at two gates:
- Gate A: after Phase 1 alignment artifacts are produced or updated.
- Gate B: immediately before Phase 3 implementation starts.
- Validate that user intent, approved plan, and generated artifacts are still consistent.
- Classify drift as `none`, `minor`, or `major`.
- If drift is `major`, pause and request clarification before any implementation.
- If critical unknowns remain with low confidence, do not proceed to implementation.

Minimum report content:

- Scope alignment check (requested objective vs current plan)
- Constraint alignment check (do-not-break rules, approvals, boundaries)
- Evidence freshness check (stale or missing sources)
- Assumption risk check (low-confidence assumptions that affect outcomes)
- Go/No-Go decision with rationale
- Use `/ai-onboarding/DRIFT_CHECK_TEMPLATE.md` as the default report structure.

---

## Enforcement Clause

- Phases may not be collapsed into a single instruction.
- Alignment, planning, and implementation must remain separate.
- If ambiguity exists, pause and request clarification before proceeding.
- If repository or context state changes mid-thread, perform a re-alignment check using `/ai-onboarding/ARCHITECTURE_ALIGNMENT.md` before continuing.
- Do not regenerate `/ai-onboarding/output/AI_ONBOARDING_SUMMARY.md` unless `/ai-onboarding/output/MASTER_CONTEXT.md` has materially changed and explicit approval is given.
