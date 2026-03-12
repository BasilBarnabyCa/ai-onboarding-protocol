# AI_EXECUTION_PROTOCOL.md

# AI Execution Protocol

This document defines the exact commands to use when working with Codex from `/ai-onboarding`.

All generated onboarding artifacts must be written to `/ai-onboarding/output`.

This protocol must be followed for every new task or session.

---

## Step 0 — Declare Mode

Declare one mode first:

- `brownfield`: existing system/repository/process exists.
- `greenfield`: new project with little or no implementation artifacts.

---

## Step 1 — Alignment (When Required)

Run this on first entry or after material context changes.

Send:

```text
Follow /ai-onboarding/ARCHITECTURE_ALIGNMENT.md.
Mode: [brownfield|greenfield]
No implementation changes.
Write onboarding artifacts to /ai-onboarding/output.
```

Do not combine this with implementation instructions.

Wait for:

- Onboarding output
- Alignment confirmation statement
- Identified risks/ambiguities

If alignment is already complete and `/ai-onboarding/output/MASTER_CONTEXT.md` has not materially changed, skip to Step 2.

---

## Step 1.5 - Drift Audit Gate

After alignment outputs exist, send:

```text
Run mandatory self-critique and drift audit.
Generate /ai-onboarding/output/DRIFT_CHECK_REPORT.md.
Use /ai-onboarding/DRIFT_CHECK_TEMPLATE.md as the report format.
If drift is major, pause and ask for clarification.
No implementation changes.
```

Proceed only on `none` or `minor` drift with acceptable assumption risk.

---

## Step 2 — Change Planning

After onboarding alignment is complete (or confirmed unnecessary), send:

```text
Follow /ai-onboarding/AGENT_RULES.md.

Begin Phase 2 - Change Planning only.
No implementation changes.

Task:
[Clearly describe the task here]
```

The Change Plan must include:

- Files/artifacts to modify
- Commands/actions to run
- Risk assessment
- Rollback strategy
- Validation and testing steps

Do not allow implementation during this phase.

Review and explicitly approve the plan before proceeding.

---

## Step 2.5 - Pre-Implementation Drift Recheck

Before implementation, send:

```text
Re-run drift audit against approved Change Plan and current outputs.
Update /ai-onboarding/output/DRIFT_CHECK_REPORT.md.
Use /ai-onboarding/DRIFT_CHECK_TEMPLATE.md as the report format.
If drift is major, pause and ask for clarification.
No implementation changes in this message.
```

Proceed only when drift status is `none` or `minor`.

---

## Step 3 — Implementation

After approving the Change Plan, send:

```text
Follow /ai-onboarding/AGENT_RULES.md.

Proceed with implementation according to the approved Change Plan.
```

Implementation entry criteria:

- Standard-risk work: onboarding score `>=90` and drift not `major`.
- Score `85-89`: low-risk prep tasks only; no high-impact implementation.
- High-impact work (prod-critical controls, sensitive data paths, compliance boundaries, irreversible actions): onboarding score `>=92` (target `95`) and drift `none`.

Implementation must:

- Follow all rules in `/ai-onboarding/output/MASTER_CONTEXT.md`.
- Respect destructive-action and sensitive-data constraints.
- Avoid committing secrets.

---

## Mid-Thread Re-Anchor (Optional)

If work is in progress and re-alignment is needed, send:

```text
Follow /ai-onboarding/AGENT_RULES.md.

Perform a quick re-alignment check against /ai-onboarding/output/MASTER_CONTEXT.md and /ai-onboarding/output/AI_ONBOARDING_SUMMARY.md.
Do NOT regenerate onboarding output in this message.
No implementation changes in this message - alignment only.

Then continue from the already-approved Change Plan.
```

Use this when:

- Thread becomes long/complex
- Scope shifts mid-implementation
- You switch tools
- You are about to touch high-risk controls

---

## Non-Negotiable Rule

Never collapse Alignment, Planning, and Implementation into a single instruction.

The workflow must always follow:

1. Alignment (when required)
2. Change Planning
3. Implementation

This separation enforces operational safety and reduces breakage risk.
