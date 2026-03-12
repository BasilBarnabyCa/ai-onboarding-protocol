# Phase 1 — Architectural Alignment (Required)

This document defines the **mandatory onboarding/alignment protocol** for any AI coding agent before it is allowed to plan or modify code.

> **Goal:** Establish a shared, evidence-based understanding of the repository architecture and safe-change constraints.
>
> **Scope:** Alignment only — **no implementation work**.

---

## When to Run Phase 1

Run Phase 1:

* On first entry to the repository (new thread, new agent, or new model).
* After any **material change** to `MASTER_CONTEXT.md`.
* After significant repo refactors that may invalidate prior understanding.

Do **not** re-run Phase 1 for normal feature work if `MASTER_CONTEXT.md` has not materially changed.

---

## Inputs and Source of Truth

* **Primary architectural source of truth:** `/MASTER_CONTEXT.md`
* **Rules of engagement:** `/AGENT_RULES.md`

### Source of Truth Hierarchy (Project-Agnostic Template)

If documentation conflicts with implementation, follow this generalized precedence order:

1. Database migration files (or equivalent schema definitions) define database schema truth.
2. Application entry points (e.g., `server/index.js`, `app.ts`, `main.py`) define mounted route/module truth.
3. Route/controller modules (e.g., `routes/**`, `controllers/**`) define active endpoint truth.
4. Client API/service layers (e.g., `frontend/src/services/**`) define client contract expectations.
5. Documentation (`/docs`, READMEs, design specs) is descriptive and may lag behind code.

> For this specific repository, the concrete file paths are documented inside `MASTER_CONTEXT.md`.

---

## Phase 1 Steps (Do Not Skip)

### 1) Read `/MASTER_CONTEXT.md` completely

* Read end-to-end.
* Treat it as the architectural constitution for the repo.

**Output required:** A short confirmation that it was read fully.

---

### 2) Execute `/AI Agent Bootstrap & Architectural Comprehension Contract`

* Follow the contract instructions exactly.
* Perform comprehension checks required by the contract.

**Output required:** Confirmation that the contract was executed.

---

### 3) Generate or validate `/AI_ONBOARDING_SUMMARY.md`

Create or validate the repo summary so that:

* Architecture is captured accurately.
* Critical constraints and boundaries are explicitly stated.
* Evidence references are included (file paths).
* Known risks/unknowns are listed.

**Rules:**

* This is a **Phase 1 artifact**.
* The summary must be consistent with `/MASTER_CONTEXT.md` and with the Source of Truth Hierarchy.
* Do **not** include secrets.

**Output required:** The generated/validated `AI_ONBOARDING_SUMMARY.md` content.

---

### 4) Confirm alignment before proceeding

Provide a final alignment statement:

* Phase 1 completed.
* No implementation work performed.
* Ready to enter **Phase 2 — Change Planning**.

**Output required:** A single “Alignment Confirmation” statement.

---

## Guardrails (Phase 1 Only)

During Phase 1, the agent must:

* Make **no code changes**.
* Make **no schema changes**.
* Make **no deployment/workflow changes**.
* Make **no refactors**.
* Only read, analyze, and produce Phase 1 artifacts.

---

## Acceptance Criteria

Phase 1 is considered complete only when all are true:

* `/MASTER_CONTEXT.md` read fully.
* Bootstrap contract executed.
* `/AI_ONBOARDING_SUMMARY.md` generated or validated.
* Alignment confirmation provided.
