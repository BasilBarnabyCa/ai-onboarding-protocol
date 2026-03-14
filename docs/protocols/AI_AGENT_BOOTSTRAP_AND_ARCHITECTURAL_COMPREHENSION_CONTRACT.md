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

When asking the user, use plain-language wording:

- "Which setup matches your situation?
- 1) greenfield - new project or idea with little/no existing implementation.
- 2) brownfield - existing repo/system you want to onboard and improve."
- Accept `1|2|greenfield|brownfield`.

---

## Execution Platform Declaration (Required)

Capture platform details before onboarding output:

- Platform (`Codex`, `Claude Code`, `ChatGPT`, or `Other`)
- Platform version/model
- Capability profile selection (`1-5`)
- Optional execution role profile (`domain - role`)

Capability profile selector:

1. `1` Auto-detect (recommended)
2. `2` Locked-down
3. `3` Standard
4. `4` High-trust
5. `5` All-access (explicit approval required)

Rules:

- Auto-detect first where possible.
- Ask platform and platform model/version every run (required capture); auto-detection only pre-fills suggestions.
- Ask for numeric selection only (`1-5`), not free-text capability fields.
- If auto-detection is available, show detected profile and accept `1` to confirm.
- If response is unclear, default to `1` and confirm.
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

- Ask required questions sequentially (one question at a time).
- Use `/ai-onboarding/commands/STEP0_CANONICAL_OPTIONS.md` for Step 0 question wording.
- Present Step 0 option lists verbatim; do not paraphrase, reorder, add, or remove choices.
- Ask at most `8` required questions (including mode-specific composite questions when needed).
- Ask up to `3` targeted follow-up questions only for critical unknowns.
- Prefer evidence-based auto-fill first.
- Maintain an assumptions ledger with confidence (`high`, `medium`, `low`).
- After Step 0 required fields are complete, run guided intake before generating artifacts:
- If mode is `greenfield`, ask:
- project brief (2-3 sentences: what is being built, for whom, target platform)
- first milestone outcomes (up to 3 bullets)
- hard constraints (timeline/budget/tech/compliance; `none` allowed)
- If mode is `brownfield`, ask:
- primary onboarding outcome
- do-not-break boundaries (security/data/runtime/deploy)
- onboarding success definition for this run
- Then auto-fill onboarding defaults unless user asks to override:
- top do-not-break constraints = no destructive actions, no secrets in outputs, no implementation during onboarding
- required approvals = approved plan before implementation, drift `major` blocks progression
- onboarding success criteria = required artifacts generated, score threshold met, drift not `major`
- Auto-fill default scope boundaries:
- in scope = onboarding artifacts + readiness/drift gates
- out of scope = implementation/deployment/refactors
- Ask this optional prompt exactly:
- "Optional: keep defaults, or type override to customize constraints/approvals/success criteria/scope/special-focus."
- If user types `override`, ask one area at a time in this order:
- constraints -> approvals -> success criteria -> scope -> special focus.
- `keep defaults` only applies to defaults/override values; it does not skip guided intake questions.
- Before artifact generation, ask this final non-blocking checkpoint exactly:
- "Any final context to include before I generate artifacts? Reply `none` to continue, or add up to 3 bullets."
- If user replies `none`, proceed. If user adds context, capture it in intake and proceed.
- Do not paste template-like multi-field blocks to the user.
- Do not generate or update onboarding output artifacts until required Step 0 fields are complete and guided intake is captured.

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
