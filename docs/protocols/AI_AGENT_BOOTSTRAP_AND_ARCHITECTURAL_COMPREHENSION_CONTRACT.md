# AI Agent Bootstrap & Context Comprehension Contract

## Purpose

This document is the mandatory onboarding instruction for any AI agent working in this repository.

Before modifying implementation artifacts, the agent must demonstrate understanding of the operating context, constraints, and safe modification patterns defined in `/ai-onboarding/output/MASTER_CONTEXT.md` (when present).

This is a comprehension and alignment step only.

**No implementation changes are allowed during this phase.**

---

# Instructions to the AI Agent

Run from `/ai-onboarding`.

Ground all claims in available evidence (repository files, documentation, or explicit user input).

For every major statement, cite supporting file paths when available.

If something is unclear or missing, explicitly mark it as:

> UNKNOWN

If an assumption is required, explicitly label it as:

> ASSUMPTION:

---

## Mode Declaration (Required)

Declare one mode before onboarding output:

- `brownfield`: existing implementation/process exists.
- `greenfield`: project is net-new or mostly undefined.

---

## Execution Platform Declaration (Required)

Capture platform details before onboarding output:

- Platform (`Codex`, `Claude Code`, `ChatGPT`, or `Other`)
- Platform version/model
- Capability profile (tools, filesystem access, network policy, approval mode)
- Optional execution role profile (`domain - role`)

Rules:

- Auto-detect first where possible.
- Ask the user only when unknown.
- Platform clarification must stay within the required-question budget.
- Execution role profile is optional and must not block progression.

---

## Brownfield Profile Selection (Required when mode is `brownfield`)

Capture:

- Target workspace path (absolute)
- Brief project description (1-3 sentences)
- Optional profile override

Resolve profile using:

- `/ai-onboarding/profiles/PROFILE_SELECTION_PROTOCOL.md`

Persist selection details:

- Selected profile id
- Selection method (`override`, `auto`, `question`)
- Selection confidence score
- Evidence summary

If ambiguous, ask one disambiguation question within question budget.

---

## Greenfield Depth Overlay (Required when mode is `greenfield`)

Apply:

- `/ai-onboarding/profiles/greenfield/GREENFIELD_MASTER_CONTEXT_ARTIFACT.md`

Persist greenfield depth outputs in onboarding artifacts (vision, non-goals, success metrics, MVP slices, milestone plan, decision rationale, acceptance/release criteria).

---

## Adaptive Intake Rule (Required)

- Ask at most `5` required questions.
- Ask up to `3` targeted follow-up questions only for critical unknowns.
- Prefer evidence-based auto-fill first.
- Maintain an assumptions ledger with confidence (`high`, `medium`, `low`).

---

## 1. Context Understanding

Provide a concise summary of:

- What the system/program/process is (1-2 sentences)
- Primary users/stakeholders and roles
- Core workflows
- Major components/process areas (if applicable)
- Access/control model (if applicable)
- Data or information handling model (if applicable)
- Delivery/operations model and environment assumptions
- Security/compliance constraints
- Multi-environment or multi-tenant considerations (if applicable)

Each section should cite evidence when possible.

---

## 2. Safe Change Rules

Extract and list 10-20 key conventions and modification constraints, including:

- Where new work should be added
- Where structural/data model changes belong
- Change and release restrictions
- Configuration and variable handling rules
- Secrets and sensitive-data handling
- Monitoring/observability expectations
- Validation/testing requirements
- Performance/scaling constraints (if applicable)
- Rules designed to prevent production or operational breakage

Each rule must cite the file(s) or user instruction it is derived from.

These rules are binding constraints.

---

## 3. How I Will Work in This Repository

Provide a practical checklist for safe execution of:

- Adding a new capability
- Modifying existing behavior
- Introducing structural/data model changes
- Changing access/control behavior
- Introducing new dependencies/tools
- Performing refactors
- Deploying or releasing changes safely

The checklist must reflect actual constraints from available evidence.

---

## 4. Risks and Ambiguities

Identify:

- Unclear areas in the context
- Missing assumptions
- Potential high-risk areas
- Cross-environment inconsistencies

If documentation conflicts with implementation, list the discrepancy and cite the files involved.

---

## 5. Sharp-Edge Acknowledgment Checklist

Explicitly acknowledge awareness of high-risk areas, including but not limited to:

- Destructive operations and irreversible actions
- Identity/access and permission controls
- Sensitive-data and secrets handling
- Environment/configuration drift risks
- Integration and endpoint mismatch risks
- Compliance/regulatory boundaries

Mark each item with one of:

- Understood
- Needs clarification

---

## Required `AI_ONBOARDING_SUMMARY.md` Structure

The summary must be a decision artifact, not a generic recap.

Required sections:

1. Project Understanding
2. Safe Change Rules (binding constraints)
3. How Work Will Be Executed Safely
4. Risks and Ambiguities (`UNKNOWN` + `ASSUMPTION` items with evidence)
5. Sharp-Edge Acknowledgment Checklist
6. Readiness Snapshot (score, drift status, go/no-go)
7. Alignment Confirmation statement

Rules:

- Every major statement must cite evidence file paths where available.
- Risks should include impact and verification/mitigation action.
- If docs conflict with implementation, include explicit discrepancy notes.

---

## Mandatory Onboarding Persistence Rule

Persist onboarding alignment artifacts in `/ai-onboarding/output`.

1. If `/ai-onboarding/output/AI_ONBOARDING_SUMMARY.md` does not exist:

   - Generate it from onboarding output.
   - Save to `/ai-onboarding/output/AI_ONBOARDING_SUMMARY.md`.
   - Do not include secrets, tokens, passwords, or personally identifiable information.

2. If `/ai-onboarding/output/AI_ONBOARDING_SUMMARY.md` exists:

   - Validate understanding against it.
   - Report discrepancies.
   - Do not overwrite without explicit approval.

No implementation work may begin until onboarding alignment is confirmed.

---

## Mandatory Self-Critique and Drift Audit

After onboarding artifacts are generated or validated, produce:

- `/ai-onboarding/output/DRIFT_CHECK_REPORT.md`
- Use `/ai-onboarding/templates/DRIFT_CHECK_TEMPLATE.md` as the default report structure.

The report must include:

- Objective alignment (current outputs vs stated user outcome)
- Scope alignment (in-scope vs out-of-scope consistency)
- Constraint alignment (do-not-break rules and approval requirements)
- Assumption risk review (all `low` confidence assumptions that can affect outcomes)
- Evidence quality review (missing, conflicting, or stale evidence)
- Drift classification: `none`, `minor`, or `major`
- Go/No-Go decision with rationale

Rules:

- `major` drift blocks progression to implementation.
- `low` confidence critical assumptions require follow-up clarification before implementation.
- Follow-up clarification still follows adaptive intake limits.

Scoring and readiness thresholds:

- `>=90`: ready for standard-risk implementation.
- `85-89`: only low-risk preparation work; no high-impact implementation.
- `<85`: onboarding incomplete.
- High-impact scope requires `>=92` (target `95`) and drift `none`.

---

## Pre-Implementation Change Planning Rule

After onboarding alignment is confirmed, but before implementation changes, produce a Change Plan including:

- Files/artifacts to be modified
- Commands/actions to be run
- Risk assessment
- Rollback strategy
- Validation and testing steps

No implementation changes may begin until the Change Plan is acknowledged.

---

## Completion Confirmation

End onboarding with the statement:

"I understand the project context, constraints, and safe modification patterns. I am ready to implement changes responsibly."
