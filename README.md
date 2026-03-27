# AI Onboarding Framework

Domain-agnostic onboarding and execution framework for AI agents, with strict safety gates for alignment, planning, and implementation.

## What This Repo Is

This repository provides a repeatable protocol to:

- onboard an AI agent with evidence-backed context
- keep question count low with adaptive intake
- enforce drift checks before implementation
- gate work with scoring thresholds (`>=90` standard, `>=92` high-impact + drift `none`)

## Who This Is For

- Teams running AI-assisted work in software, security, operations, or mixed domains
- Projects that need deterministic onboarding and change safety

## Where To Start

Create a folder in the root directory of your project called `/ai-onboarding`.

Download and copy contents of this repo to the `/ai-onboarding` folder before starting.

Use command shortcuts for the fastest workflow. To avoid accidental triggering, a shortcut is only treated as a command when your message starts with `cmd:` (for example, `cmd:onboard` or `cmd:plan: <task description>`). If you use words like `onboard` in normal conversation, they are treated as regular text.

Command reference:

- `commands/COMMANDS.md` (copy/paste view)
- `commands/commands.yaml` (source of truth)

In a fresh project/session, start with this first message so the assistant loads your local command spec before shortcuts:

```text
Read /ai-onboarding/commands/commands.yaml and enforce strict command mode only for messages that begin with `cmd:`.
Do not reject or reroute normal-language requests that do not begin with `cmd:`; handle them as normal conversation.
```

Then use this command sequence:

1. `cmd:onboard`
2. `cmd:drift-audit`
3. `cmd:plan: <task description>`
4. `cmd:impl`

If you prefer raw prompts instead of commands, send these prompts in order.

### 1) Alignment (start here)

```text
Follow /ai-onboarding/docs/protocols/ARCHITECTURE_ALIGNMENT.md.
No implementation changes.
```

After this first message, the assistant must ask for missing Step 0 inputs automatically.
You should not need to provide them in advance.
Step 0 required fields are a hard gate: the assistant must not proceed to Step 1+ until all required fields are provided.

Expected assistant behavior:

- Ask one question at a time (sequential), not a large multi-field block.
- Use canonical Step 0 question wording from `/ai-onboarding/commands/STEP0_CANONICAL_OPTIONS.md` verbatim.
- Ask mode first with plain-language definitions:
1) greenfield = new project/idea with little or no implementation yet
2) brownfield = existing repo/system that already has implementation
- Ask platform and platform model/version every run (auto-detection can prefill but must still be confirmed or corrected).
- Ask capability profile as a numeric choice:
1) Auto-detect, 2) Locked-down, 3) Standard, 4) High-trust, 5) All-access.
- If `greenfield`, continue with greenfield-relevant questions.
- If `brownfield`, ask target workspace path and project brief next.
- After Step 0, run guided intake questions before generating output files:
- If `greenfield`, ask (one question at a time):
- project brief (2-3 sentences: what is being built, for whom, target platform)
- first milestone outcomes (up to 3 bullets)
- hard constraints (timeline/budget/tech/compliance; `none` allowed)
- If `brownfield`, ask (one question at a time):
- do-not-break boundaries (security/data/runtime/deploy)
- Then auto-fill onboarding defaults:
constraints = no destructive actions, no secrets in outputs, no implementation during onboarding.
approvals = approved plan before implementation; drift `major` blocks progression.
success criteria = required artifacts generated; score threshold met; drift not `major`.
- Scope boundaries are auto-filled by default:
in scope = onboarding artifacts + readiness/drift gates.
out of scope = implementation/deployment/refactors.
- Optional override prompt:
"Optional: keep defaults, or type override to customize constraints/approvals/success criteria/scope/special-focus."
- If user types `override`, ask one area at a time in this order:
constraints -> approvals -> success criteria -> scope -> special focus.
- `keep defaults` only applies to defaults/override values; it does not skip guided intake questions.
- Before generating artifacts, ask one final non-blocking checkpoint:
"Any final context to include before I generate artifacts? Reply `none` to continue, or add up to 3 bullets."
- Optional fields (`execution role profile`, `profile override`) are non-blocking.

If execution role profile is omitted, the default role from `AGENT_RULES.md` is used.

Strict behavior:

- Missing required Step 0 fields block onboarding progression.
- The assistant asks only missing required fields and pauses until answered.
- The assistant does not infer missing Step 0 values.
- If capability choice is unclear, the assistant defaults to `1` and confirms.
- After Step 0, guided intake answers must be captured before artifact generation begins.

Wait for:

- onboarding output artifacts
- alignment confirmation
- risks/ambiguities

### 2) Drift Audit Gate

```text
Run mandatory self-critique and drift audit.
Generate /ai-onboarding/output/DRIFT_CHECK_REPORT.md.
Use /ai-onboarding/templates/DRIFT_CHECK_TEMPLATE.md as the report format.
If drift is major, pause and ask for clarification.
No implementation changes.
```

Drift audit cadence during active development:

- Run `cmd:drift-audit` every 3-5 working days while work is active.
- Run `cmd:drift-audit` immediately after material scope/architecture/priority changes.
- Run `cmd:reanchor` for quick alignment checks between full drift audits.

### 3) Change Planning

Command shortcut form:

- `cmd:plan: <task description>`

```text
Follow /ai-onboarding/AGENT_RULES.md.

Begin Phase 2 - Change Planning only.
No implementation changes.

Task:
[Clearly describe the task here]
```

Review and explicitly approve the plan before implementation.

### 4) Implementation

```text
Follow /ai-onboarding/AGENT_RULES.md.

Proceed with implementation according to the approved Change Plan.
```

### 5) Mid-Thread Re-Anchor (optional)

```text
Follow /ai-onboarding/AGENT_RULES.md.

Perform a quick re-alignment check against /ai-onboarding/output/MASTER_CONTEXT.md and /ai-onboarding/output/AI_ONBOARDING_SUMMARY.md.
Do NOT regenerate onboarding output in this message.
No implementation changes in this message - alignment only.

Then continue from the already-approved Change Plan.
```

For full details, use `docs/protocols/AI_EXECUTION_PROTOCOL.md`.

## Core Files

- `docs/protocols/AI_EXECUTION_PROTOCOL.md`: exact phase prompts
- `docs/protocols/ARCHITECTURE_ALIGNMENT.md`: Phase 1 alignment rules
- `AGENT_RULES.md`: behavioral constraints and readiness gates
- `docs/protocols/AI_AGENT_BOOTSTRAP_AND_ARCHITECTURAL_COMPREHENSION_CONTRACT.md`: mandatory onboarding contract
- `docs/generators/AI_ONBOARDING_MASTER_CONTEXT_GENERATOR.md`: master context generation rules
- `templates/ONBOARDING_INTAKE_TEMPLATE.md`: low-friction intake template
- `templates/DRIFT_CHECK_TEMPLATE.md`: standard drift audit template
- `commands/COMMANDS.md`: command copy/paste prompts
- `commands/commands.yaml`: command source-of-truth
- `profiles/PROFILE_SELECTION_PROTOCOL.md`: deterministic brownfield profile router
- `profiles/PROFILE_REGISTRY.md`: active/planned profile registry
- `profiles/greenfield/GREENFIELD_MASTER_CONTEXT_ARTIFACT.md`: high-rigor greenfield depth overlay

## Software Brownfield Overlay

When mode is `brownfield` and target workspace is an existing software project, apply:

- `profiles/software-brownfield/SOFTWARE_BROWNFIELD_MASTER_CONTEXT_ARTIFACT.md`

Direct prompt variant:

- `profiles/software-brownfield/SOFTWARE_BROWNFIELD_COPYPASTE_PROMPT.md`

Profile selection behavior:

- For brownfield runs, profile selection is resolved via `profiles/PROFILE_SELECTION_PROTOCOL.md`.
- If ambiguous, one disambiguation question is asked within onboarding budget.

## Greenfield Overlay

When mode is `greenfield`, apply:

- `profiles/greenfield/GREENFIELD_MASTER_CONTEXT_ARTIFACT.md`

## Output Artifacts

All generated artifacts are written to:

- `/ai-onboarding/output`
- This directory is auto-created if missing.
- Generated files in `output/` are gitignored; only `output/.gitkeep` is tracked.

Common files:

- `MASTER_CONTEXT.md`
- `AI_ONBOARDING_SUMMARY.md`
- `ASSUMPTIONS_LEDGER.md`
- `DRIFT_CHECK_REPORT.md`
- `PROJECT_SCOPE.md` (greenfield required)
- `ONBOARDING_INTAKE_FILLED.md`

Archived output snapshots:

- `/ai-onboarding/output/archive/*`

## Role Persistence

- Optional Step 0 field: `Execution role profile` in format `domain - role`.
- If provided, it is persisted in onboarding artifacts (starting with `ONBOARDING_INTAKE_FILLED.md`) and carried forward in alignment context.
- If omitted, the default role from `AGENT_RULES.md` is used.
- Precedence order: current prompt role profile -> persisted onboarding artifacts -> default role in `AGENT_RULES.md`.

## Readiness Gates

- Standard-risk execution: onboarding score `>=90` and drift not `major`
- Score `85-89`: low-risk prep only
- High-impact work: onboarding score `>=92` (target `95`) and drift `none`
- Any `major` drift: implementation blocked

## Recommended First Live Pilot

1. Run one brownfield onboarding against a non-production project folder.
2. Review `MASTER_CONTEXT.md` and `DRIFT_CHECK_REPORT.md`.
3. Approve Phase 2 plan.
4. Re-run pre-implementation drift check before any changes.
