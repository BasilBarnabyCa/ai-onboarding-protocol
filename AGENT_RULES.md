# AGENT_RULES.md

# AGENT RULES (MANDATORY)

All AI agents must follow this protocol before making changes.

> Note: Alignment (Phase 1) is defined in `/ai-onboarding/docs/protocols/ARCHITECTURE_ALIGNMENT.md` and must be executed before Phase 2 on first entry or after material context changes.

---

## Workspace Contract

- Run onboarding workflows from `/ai-onboarding`.
- Write onboarding artifacts to `/ai-onboarding/output`.
- If `/ai-onboarding/output` does not exist, create it before writing artifacts.
- Do not write generated onboarding artifacts outside `/ai-onboarding/output` unless explicitly approved.

---

## Command Invocation Safety

- Command shortcuts are recognized only when input begins with `cmd:`.
- Valid command format: `^(cmd:(onboard|drift-audit|impl|reanchor|brownfield:select)|cmd:plan: \S.*)$`
- If input does not match valid command format exactly, treat it as normal conversation text.
- `plan` requires inline task description in strict form: `cmd:plan: <task description>`.

---

## Execution Role Definition

When performing work in this repository, operate as:

**A senior domain practitioner executing within an established operating context.**

Optional Step 0 role profile:

- User may provide `Execution role profile` as `domain - role` (example: `cybersecurity - SOC analyst`).
- If provided, use it as execution posture guidance for the thread.
- If omitted, use the default role definition above.

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

Effective role posture (default or user-provided optional role profile) remains constant across threads unless explicitly changed.

---

## Adaptive Intake Constraints

- Ask required onboarding questions sequentially (one question at a time).
- Ask at most `6` required onboarding questions (including one mode-specific composite question when needed).
- Ask at most `3` follow-up questions, and only when critical uncertainty remains.
- Prefer auto-discovery from available artifacts before asking questions.
- Capture execution platform profile (platform, version/model, capabilities) at onboarding start.
- Offer optional execution role capture as `domain - role`.
- If mode is `brownfield`, capture target workspace path and a 1-3 sentence project brief.
- Resolve brownfield profile selection using `/ai-onboarding/profiles/PROFILE_SELECTION_PROTOCOL.md`.
- If profile selection is ambiguous, ask one disambiguation question within question budget.
- Track unresolved assumptions in an assumptions ledger with confidence labels.
- Step 0 required fields are: mode, platform, platform profile, and for brownfield target workspace path + project brief.
- Do not assume or infer missing Step 0 required fields.
- Optional Step 0 field: execution role profile (`domain - role`).
- Do not paste template-like multi-field intake blocks to the user.

---

## Step 0 Hard Gate (Strict)

- If any Step 0 required field is missing, onboarding is blocked at Step 0.
- While blocked at Step 0, do not run bootstrap, produce onboarding artifacts, or declare Phase 1 complete.
- Ask `mode` first, then branch to the next appropriate required question by mode.
- Request only the missing required fields, then continue once all required fields are present.
- Optional profile override may be requested after required fields are complete; it is never a blocker.

## Core Intake Hard Gate (Strict)

- After Step 0, collect core intake required fields before artifact generation:
- primary outcome
- scope boundaries
- top do-not-break constraints
- required approvals
- onboarding success criteria
- While core intake required fields are incomplete, do not generate or update onboarding output artifacts.

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
- Use `/ai-onboarding/templates/DRIFT_CHECK_TEMPLATE.md` as the default report structure.

---

## Enforcement Clause

- Phases may not be collapsed into a single instruction.
- Alignment, planning, and implementation must remain separate.
- If ambiguity exists, pause and request clarification before proceeding.
- If repository or context state changes mid-thread, perform a re-alignment check using `/ai-onboarding/docs/protocols/ARCHITECTURE_ALIGNMENT.md` before continuing.
- Do not regenerate `/ai-onboarding/output/AI_ONBOARDING_SUMMARY.md` unless `/ai-onboarding/output/MASTER_CONTEXT.md` has materially changed and explicit approval is given.
