# AI_EXECUTION_PROTOCOL.md

# AI Execution Protocol

This document defines the exact commands to use when working with Codex from `/ai-onboarding`.

All generated onboarding artifacts must be written to `/ai-onboarding/output`.

This protocol must be followed for every new task or session.

---

## Minimal Command Set (Preferred Quick Path)

Use these short prompts when you want the original simple workflow style.

### 1) Alignment

```text
Follow /ai-onboarding/ARCHITECTURE_ALIGNMENT.md.
No implementation changes.
```

### 2) Change Planning

```text
Follow /ai-onboarding/AGENT_RULES.md.

Begin Phase 2 - Change Planning only.
No implementation changes.

Task:
[Clearly describe the task here]
```

### 3) Implementation

```text
Follow /ai-onboarding/AGENT_RULES.md.

Proceed with implementation according to the approved Change Plan.
```

### 4) Mid-Thread Re-Anchor (Optional)

```text
Follow /ai-onboarding/AGENT_RULES.md.

Perform a quick re-alignment check against /ai-onboarding/output/MASTER_CONTEXT.md and /ai-onboarding/output/AI_ONBOARDING_SUMMARY.md.
Do NOT regenerate onboarding output.
No implementation changes in this message - alignment only.

Then continue from the already-approved Change Plan.
```

Notes:

- After the minimal Alignment prompt, the system must immediately ask for any missing Step 0 inputs before proceeding.
- The user should not be expected to know Step 0 fields unless asked.
- Keep phase separation strict; do not collapse alignment/planning/implementation.

---

## Step 0 — Declare Mode and Platform

Declare mode and execution platform first:

- `brownfield`: existing system/repository/process exists.
- `greenfield`: new project with little or no implementation artifacts.
- Platform: `Codex`, `Claude Code`, `ChatGPT`, or `Other`
- Platform version/model
- Capability profile (tools/file access/network/approval mode)
- If `brownfield`: target workspace path (absolute)
- If `brownfield`: brief project description (1-3 sentences)
- Optional: profile override (`software-brownfield`, etc.)

If any Step 0 input is missing, ask these questions before alignment work begins:

1. What mode should I use: `greenfield` or `brownfield`?
2. What platform are you using: `Codex`, `Claude Code`, `ChatGPT`, or `Other`?
3. What platform profile should I assume (model + capability summary)?
4. If brownfield: what is the target workspace absolute path?
5. If brownfield: give a brief project description (1-3 sentences).
6. Optional if brownfield: do you want to force a profile override?

If mode is `brownfield`, run:

- `/ai-onboarding/profiles/PROFILE_SELECTION_PROTOCOL.md`

If selected profile is `software-brownfield`, apply:

- `/ai-onboarding/profiles/software-brownfield/SOFTWARE_BROWNFIELD_MASTER_CONTEXT_ARTIFACT.md`

---

## Step 0.5 — Brownfield Profile Resolution

Run this step only when mode is `brownfield`.

- Resolve profile using `/ai-onboarding/profiles/PROFILE_SELECTION_PROTOCOL.md`.
- Persist profile id, selection method, confidence score, and evidence summary in onboarding outputs.
- If ambiguous, ask one disambiguation question within intake budget.

---

## Step 1 — Alignment (When Required)

Run this on first entry or after material context changes.

Send:

```text
Follow /ai-onboarding/ARCHITECTURE_ALIGNMENT.md.
Mode: [brownfield|greenfield]
Platform: [Codex|Claude Code|ChatGPT|Other]
Platform profile: [model + capability summary]
Target workspace: [absolute path, brownfield only]
Project brief: [1-3 sentences, brownfield only]
Profile override: [optional]
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
