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

Copy the `/ai-onboarding` folder into your project root before starting.

Use command shortcuts for the fastest workflow. To avoid accidental triggering, a shortcut is only treated as a command when your message starts with `cmd:` (for example, `cmd:onboard` or `cmd:plan: <task description>`). If you use words like `onboard` in normal conversation, they are treated as regular text.

Command reference:

- `commands/COMMANDS.md` (copy/paste view)
- `commands/commands.yaml` (source of truth)

Recommended command sequence:

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

Expected assistant questions (as needed):

- Mode: `greenfield` or `brownfield`
- Platform: `Codex`, `Claude Code`, `ChatGPT`, or `Other`
- Platform profile (model + capability summary)
- Brownfield only: target workspace absolute path
- Brownfield only: brief project description (1-3 sentences)
- Brownfield only: optional profile override

Strict behavior:

- Missing required Step 0 fields block onboarding progression.
- The assistant asks only missing required fields and pauses until answered.
- The assistant does not infer missing Step 0 values.

Alternative if you prefer to provide everything up front in one message:

```text
Follow /ai-onboarding/docs/protocols/ARCHITECTURE_ALIGNMENT.md.
Mode: [brownfield|greenfield]
Platform: [Codex|Claude Code|ChatGPT|Other]
Platform profile: [model + capability summary]
Target workspace: [absolute path, brownfield only]
Project brief: [1-3 sentences, brownfield only]
Profile override: [optional]
No implementation changes.
Write onboarding artifacts to /ai-onboarding/output.
```

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

## Software Brownfield Overlay

When mode is `brownfield` and target workspace is an existing software project, apply:

- `profiles/software-brownfield/SOFTWARE_BROWNFIELD_MASTER_CONTEXT_ARTIFACT.md`

Direct prompt variant:

- `profiles/software-brownfield/SOFTWARE_BROWNFIELD_COPYPASTE_PROMPT.md`

Profile selection behavior:

- For brownfield runs, profile selection is resolved via `profiles/PROFILE_SELECTION_PROTOCOL.md`.
- If ambiguous, one disambiguation question is asked within onboarding budget.

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
