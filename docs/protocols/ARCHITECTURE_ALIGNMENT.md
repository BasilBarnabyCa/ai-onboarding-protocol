# Phase 1 - Context Alignment (Required)

This document defines the mandatory onboarding/alignment protocol for any AI agent before it is allowed to plan or modify implementation artifacts.

> Goal: Establish a shared, evidence-based understanding of context and safe-change constraints.
>
> Scope: Alignment only - no implementation work.

---

## Workspace and Output Contract

- Run from `/ai-onboarding`.
- Persist onboarding artifacts under `/ai-onboarding/output`.

---

## When to Run Phase 1

Run Phase 1:

- On first entry to the repository/process
- After material changes to `/ai-onboarding/output/MASTER_CONTEXT.md`
- After significant refactors or context shifts

Do not re-run for normal low-risk work if context has not materially changed.

---

## Inputs and Source of Truth

- Primary source: `/ai-onboarding/output/MASTER_CONTEXT.md` (when available)
- Rules of engagement: `/ai-onboarding/AGENT_RULES.md`

### Source of Truth Hierarchy (Agnostic Template)

If documentation conflicts with implementation/operations, use this precedence:

1. Executable reality (active systems, deployed configs, enforced controls)
2. Primary implementation/process entry points
3. Operational modules/workflows that are actually invoked
4. Client/integration contracts
5. Documentation and plans

For this repository, concrete paths should be recorded in `MASTER_CONTEXT.md`.

---

## Phase 1 Steps (Do Not Skip)

### 0) Declare Mode

Declare one mode before alignment work:

- `brownfield`
- `greenfield`

Also declare execution platform profile:

- Platform (`Codex`, `Claude Code`, `ChatGPT`, or `Other`)
- Platform version/model
- Capability profile (tools/file access/network/approval mode)

If mode is `brownfield`, also declare:

- Target workspace path (absolute)
- Brief project description (1-3 sentences)
- Optional profile override

Then resolve selected profile via:

- `/ai-onboarding/profiles/PROFILE_SELECTION_PROTOCOL.md`

**Output required:** Mode + platform declaration (+ brownfield project brief and selected profile when applicable).

Step 0 interaction rule:

- If the user starts with a minimal alignment prompt and Step 0 fields are missing, the assistant must ask for missing fields before proceeding.
- The assistant must not assume the user already knows which Step 0 questions to provide.

---

### 1) Read `/ai-onboarding/output/MASTER_CONTEXT.md` if present

- If present: read end-to-end and treat as current context constitution.
- If absent: mark as `UNKNOWN` and proceed to bootstrap generation flow.

**Output required:** Confirmation of read or explicit absence note.

---

### 2) Execute `/ai-onboarding/docs/protocols/AI_AGENT_BOOTSTRAP_AND_ARCHITECTURAL_COMPREHENSION_CONTRACT.md`

- Follow contract exactly.
- Respect adaptive intake limits.

**Output required:** Confirmation that contract was executed.

---

### 3) Generate or validate `/ai-onboarding/output/AI_ONBOARDING_SUMMARY.md`

Create or validate summary so that:

- Context is captured accurately
- Critical constraints and boundaries are explicit
- Evidence references are included where available
- Risks/unknowns/assumptions are listed

Rules:

- This is a Phase 1 artifact.
- It must be consistent with `MASTER_CONTEXT.md` (if present) and the source-of-truth hierarchy.
- Do not include secrets.

**Output required:** Generated/validated summary content.

---

### 3.5) Run self-critique drift audit

Generate or update:

- `/ai-onboarding/output/DRIFT_CHECK_REPORT.md`
- Use `/ai-onboarding/templates/DRIFT_CHECK_TEMPLATE.md` as the base format.

Minimum checks:

- Objective and scope alignment
- Constraint and approval alignment
- Assumption risk review
- Evidence freshness review
- Drift classification (`none`, `minor`, `major`)
- Go/No-Go decision
- Threshold check against onboarding scoring policy (`>=90` standard, `>=92` high-impact)

If drift is `major`, pause and request clarification before proceeding.

**Output required:** Drift report content.

---

### 4) Confirm alignment before proceeding

Provide final alignment statement:

- Phase 1 completed
- No implementation work performed
- Ready to enter Phase 2 - Change Planning

**Output required:** One alignment confirmation statement.

---

## Guardrails (Phase 1 Only)

During Phase 1, the agent must:

- Make no implementation changes
- Make no structural/data model changes
- Make no deployment/runtime control changes
- Make no refactors
- Only read, analyze, and produce onboarding artifacts

---

## Acceptance Criteria

Phase 1 is complete only when all are true:

- Mode declared
- Platform profile declared
- Brownfield project brief declared (if applicable)
- Brownfield selected profile declared (if applicable)
- `MASTER_CONTEXT.md` read (or absence explicitly acknowledged)
- Bootstrap contract executed
- `AI_ONBOARDING_SUMMARY.md` generated or validated
- `DRIFT_CHECK_REPORT.md` generated or updated
- Alignment confirmation provided
