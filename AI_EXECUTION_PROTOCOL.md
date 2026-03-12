# AI_EXECUTION_PROTOCOL.md

# AI Execution Protocol

This document defines the exact commands to use when working with Codex after the following files exist in the repository root:

- `/MASTER_CONTEXT.md`
- `/AI Agent Bootstrap & Architectural Comprehension Contract.md`
- `/AGENT_RULES.md`
- `/ARCHITECTURE_ALIGNMENT.md`

This protocol must be followed for every new task or session.

---

## Step 1 — Architectural Alignment (New Session Only When Required)

> ⚠ Run this step only on first entry to the repository or after material architectural changes.

When starting a new session that requires alignment, send exactly:

```text
Follow ARCHITECTURE_ALIGNMENT.md.
No code changes.
```

Do not combine this with implementation instructions.

Wait for:

- Onboarding output
- Alignment confirmation statement
- Any identified risks or ambiguities

If alignment has already been completed and `MASTER_CONTEXT.md` has not changed, skip to Step 2.

---

## Step 2 — Change Planning

After onboarding alignment is complete (or confirmed unnecessary), send:

```text
Follow AGENT_RULES.md.

Begin Phase 2 — Change Planning only.
No code changes.

Feature:
[Clearly describe the task here]
```

The Change Plan must include:

- Files to modify
- Commands to run (migrations, builds, etc.)
- Risk assessment
- Rollback strategy
- Validation and testing steps

Do not allow implementation during this phase.

Review and explicitly approve the plan before proceeding.

---

## Step 3 — Implementation

After approving the Change Plan, send:

```text
Follow AGENT_RULES.md.

Proceed with implementation according to the approved Change Plan.
```

Implementation must:

- Follow all rules in `/MASTER_CONTEXT.md`.
- Respect destructive-script constraints.
- Respect authentication and database constraints.
- Avoid committing secrets.

---

## Mid-Thread Re-Anchor (Optional but Recommended)

If work is already in progress and you need to ensure alignment without restarting Phase 1, send:

```text
Follow AGENT_RULES.md.

Perform a quick re-alignment check against MASTER_CONTEXT.md and AI_ONBOARDING_SUMMARY.md.
Do NOT regenerate AI_ONBOARDING_SUMMARY.md.
No code changes in this message — alignment only.

Then continue from the already-approved Change Plan.
```

Use this when:

- The thread becomes long or complex.
- Scope shifts mid-implementation.
- You switch tools (Cursor ↔ Codex).
- You are about to touch schema, auth, or deployment.

Do NOT use this for trivial UI-only edits.

---

## Non-Negotiable Rule

Never collapse Alignment, Planning, and Implementation into a single instruction.

The workflow must always follow:

1. Alignment (when required)
2. Change Planning
3. Implementation

This separation enforces architectural safety and prevents unintended production breakage.

---

End of Protocol.
