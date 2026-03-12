# AI Agent Bootstrap & Architectural Comprehension Contract

## Purpose

This document is the mandatory onboarding instruction for any AI coding agent working in this repository.

Before modifying any code, the agent must demonstrate understanding of the architecture, constraints, and safe modification patterns defined in `/MASTER_CONTEXT.md`.

This is a comprehension and alignment step only.

**No code changes are allowed during this phase.**

---

# Instructions to the AI Agent

Read `/MASTER_CONTEXT.md` end-to-end and treat it as the architectural source of truth.

All claims must be grounded in repository evidence.

For every major architectural statement, cite supporting file paths (for example: `backend/src/server.js`, `docs/PRISMA_AZURE_DEPLOYMENT.md`).

If something is unclear or missing, explicitly mark it as:

> UNKNOWN

If an assumption is required, explicitly label it as:

> ASSUMPTION:

---

## 1. Project Understanding

Provide a clear and concise summary of:

* What the product/system is (1–2 sentences)
* Primary users and roles
* Core workflows
* Frontend or client architecture (if applicable)
* Backend or service architecture (if applicable)
* Authentication model (describe mechanism and flow)
* Data layer (ORM/queries, schema strategy, dev vs prod differences)
* Deployment model and infrastructure assumptions
* Security model and constraints
* Any multi-environment or multi-tenant considerations

Each section must cite supporting file paths.

---

## 2. Safe Change Rules

Extract and list the 10–20 most important conventions and modification constraints.

These must include:

* Where new code should be added
* Where schema changes belong
* Migration strategy and restrictions
* How configuration and environment variables are handled
* Secrets management approach
* Logging/monitoring expectations
* Testing requirements (if any)
* Performance or scaling constraints
* Any rules designed to prevent production breakage

Each rule must cite the file(s) it is derived from.

These rules are binding constraints.

---

## 3. How I Will Work in This Repository

Provide a practical checklist for safe implementation of:

* Adding a new feature
* Modifying existing logic
* Adding or modifying database schema
* Changing authentication behavior
* Introducing new dependencies
* Performing refactors
* Deploying changes safely

The checklist must reflect the actual architecture and constraints defined in `/MASTER_CONTEXT.md`.

---

## 4. Risks and Ambiguities

Identify:

* Any unclear areas in the architecture
* Any missing assumptions
* Any potential high-risk areas
* Any cross-environment inconsistencies

If assumptions are required, clearly label them as:

> ASSUMPTION:

If documentation conflicts with implementation, explicitly list the discrepancy and cite the files involved.

---

## 5. Sharp-Edge Acknowledgment Checklist

Explicitly acknowledge awareness of critical high-risk areas defined in `/MASTER_CONTEXT.md`, including but not limited to:

* Prisma centralized instance requirement
* Destructive scripts (import/truncate/migrate reset)
* Authentication and role synchronization constraints
* Environment variable handling rules
* Port and base URL mismatches
* Secrets handling and non-commit rules
* Azure deployment constraints

Mark each item with one of the following:

* Understood
* Needs clarification

---

## Mandatory Onboarding Persistence Rule

The agent must ensure architectural alignment is persisted.

1. If `/AI_ONBOARDING_SUMMARY.md` does not exist:

   * Generate it using the structured onboarding output.
   * Save it to the repository root.
   * Do not include secrets, connection strings, tokens, passwords, or personally identifiable information.
   * Keep it concise; reference `/MASTER_CONTEXT.md` instead of duplicating large sections.

2. If `/AI_ONBOARDING_SUMMARY.md` exists:

   * Validate your understanding against it.
   * Report discrepancies.
   * Do not overwrite without explicit approval.

No implementation work may begin until onboarding alignment is confirmed.

---

## Pre-Implementation Change Planning Rule

After onboarding alignment is confirmed, but before modifying code, the agent must produce a Change Plan including:

* Files to be modified
* Commands to be run (for example: migrations, builds)
* Risk assessment
* Rollback strategy
* Validation and testing steps

No code modifications may begin until the Change Plan is acknowledged.

---

## Completion Confirmation

End onboarding with the statement:

"I understand the project architecture, constraints, and safe modification patterns. I am ready to implement changes responsibly."
