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
- Capability profile using numbered selection:
- `1` Auto-detect (recommended)
- `2` Locked-down
- `3` Standard
- `4` High-trust
- `5` All-access (explicit approval required)
- Optional execution role profile (`domain - role`)

If mode is `brownfield`, also declare:

- Target workspace path (absolute)
- Brief project description (1-3 sentences)
- Optional profile override

Then resolve selected profile via:

- `/ai-onboarding/profiles/PROFILE_SELECTION_PROTOCOL.md`

**Output required:** Mode + platform declaration (+ optional execution role profile and brownfield project brief/selected profile when applicable).

Step 0 interaction rule:

- If the user starts with a minimal alignment prompt and Step 0 fields are missing, the assistant must ask for missing fields before proceeding.
- Ask one question at a time; do not paste a multi-field template block.
- Use `/ai-onboarding/commands/STEP0_CANONICAL_OPTIONS.md` for Step 0 option wording.
- Present Step 0 option lists verbatim; do not paraphrase, reorder, add, or remove choices.
- Ask `mode` first with explicit plain-language definitions, then branch to the next appropriate question by mode.
- Required first question text:
- "Which setup matches your situation?
- 1) greenfield - new project or idea with little/no existing implementation.
- 2) brownfield - existing repo/system you want to onboard and improve."
- Accept `1|2|greenfield|brownfield`.
- For capability profile, ask for one numeric choice (`1-5`) instead of free-text capability details.
- The assistant must not assume the user already knows which Step 0 questions to provide.
- Missing required Step 0 fields block progression to Step 1+.
- Required fields: mode, platform, platform version/model, capability profile selection (`1-5`), and for brownfield target workspace path + project brief.
- Optional fields (non-blocking): execution role profile (`domain - role`), profile override.
- Until required fields are complete, do not read/validate onboarding artifacts and do not execute bootstrap.

Post-Step 0 guided intake (required, sequential):

- After Step 0 is complete, ask guided intake questions one at a time before generating artifacts.
- If mode is `greenfield`, ask:
- project brief (2-3 sentences: what is being built, for whom, target platform)
- first milestone outcomes (up to 3 bullets)
- hard constraints (timeline/budget/tech/compliance; `none` allowed)
- If mode is `brownfield`, ask:
- primary onboarding outcome
- do-not-break boundaries (security/data/runtime/deploy)
- onboarding success definition for this run

Core intake defaults (non-blocking, applied after guided intake):

- Auto-fill defaults:
- top do-not-break constraints = no destructive actions, no secrets in outputs, no implementation during onboarding
- required approvals = approved plan before implementation, drift `major` blocks progression
- onboarding success criteria = required artifacts generated, score threshold met, drift not `major`
- Auto-fill default scope boundaries:
- in scope = onboarding artifacts + readiness/drift gates
- out of scope = implementation/deployment/refactors
- Then ask this optional prompt exactly:
- "Optional: keep defaults, or type override to customize constraints/approvals/success criteria/scope/special-focus."
- If user types `override`, ask one area at a time in this order:
- constraints -> approvals -> success criteria -> scope -> special focus.
- `keep defaults` only applies to defaults/override values; it does not skip guided intake questions.
- Before artifact generation, ask this final non-blocking checkpoint exactly:
- "Any final context to include before I generate artifacts? Reply `none` to continue, or add up to 3 bullets."
- If user replies `none`, proceed. If user adds context, capture it in intake and proceed.
- Do not generate or update onboarding artifacts until required Step 0 fields are complete and guided intake is captured.

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
- Platform version/model declared
- Capability profile selection declared (`1-5`)
- Execution role profile captured (if provided) or default role applied
- Brownfield project brief declared (if applicable)
- Brownfield selected profile declared (if applicable)
- Guided intake answers captured (mode-specific)
- Final pre-generation additions checkpoint asked (response captured or `none`)
- Core intake defaults applied (or overridden when provided)
- `MASTER_CONTEXT.md` read (or absence explicitly acknowledged)
- Bootstrap contract executed
- `AI_ONBOARDING_SUMMARY.md` generated or validated
- `DRIFT_CHECK_REPORT.md` generated or updated
- Alignment confirmation provided
