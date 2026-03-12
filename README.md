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

## Quick Start

Run from `/ai-onboarding`.

1. Choose mode and platform:
- Mode: `greenfield` or `brownfield`
- Platform: `Codex`, `Claude Code`, `ChatGPT`, or `Other`
- For brownfield, also declare target workspace path

2. Start alignment:

```text
Follow /ai-onboarding/ARCHITECTURE_ALIGNMENT.md.
Mode: [brownfield|greenfield]
Platform: [Codex|Claude Code|ChatGPT|Other]
Platform profile: [model + capability summary]
Target workspace: [absolute path]
No implementation changes.
Write onboarding artifacts to /ai-onboarding/output.
```

3. After alignment, run drift audit gate:

```text
Run mandatory self-critique and drift audit.
Generate /ai-onboarding/output/DRIFT_CHECK_REPORT.md.
Use /ai-onboarding/DRIFT_CHECK_TEMPLATE.md as the report format.
If drift is major, pause and ask for clarification.
No implementation changes.
```

4. Move to planning, then implementation only after approvals and gate checks.

## Core Files

- `AI_EXECUTION_PROTOCOL.md`: exact phase prompts
- `ARCHITECTURE_ALIGNMENT.md`: Phase 1 alignment rules
- `AGENT_RULES.md`: behavioral constraints and readiness gates
- `AI_AGENT_BOOTSTRAP_AND_ARCHITECTURAL_COMPREHENSION_CONTRACT.md`: mandatory onboarding contract
- `AI_ONBOARDING_MASTER_CONTEXT_GENERATOR.md`: master context generation rules
- `ONBOARDING_INTAKE_TEMPLATE.md`: low-friction intake template
- `DRIFT_CHECK_TEMPLATE.md`: standard drift audit template

## Software Brownfield Overlay

When mode is `brownfield` and target workspace is an existing software project, apply:

- `profiles/software-brownfield/SOFTWARE_BROWNFIELD_MASTER_CONTEXT_ARTIFACT.md`

Direct prompt variant:

- `profiles/software-brownfield/SOFTWARE_BROWNFIELD_COPYPASTE_PROMPT.md`

## Output Artifacts

All generated artifacts are written to:

- `/ai-onboarding/output`

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
