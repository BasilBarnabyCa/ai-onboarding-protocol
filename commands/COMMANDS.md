# COMMANDS.md

Derived from:
- `/ai-onboarding/commands/commands.yaml`

Last synced:
- 2026-03-13

Note:
- `commands.yaml` is the source of truth.
- This file is a human-friendly copy/paste view.

## How To Use

Use strict command mode:
- Only treat input as a command when it starts with `cmd:`.
- Commands must match: `^(cmd:(onboard|drift-audit|impl|reanchor|brownfield:select)|cmd:plan: \S.*)$`
- Anything else is normal conversation text.
- For planning, use `cmd:plan: <task description>`.

Example flow:
1. `cmd:onboard`
2. `cmd:drift-audit`
3. `cmd:plan: add OAuth login`
4. `cmd:impl`

## Commands

### cmd:onboard

```text
Follow /ai-onboarding/docs/protocols/ARCHITECTURE_ALIGNMENT.md.
Strict Step 0 mode:
Use /ai-onboarding/commands/STEP0_CANONICAL_OPTIONS.md as canonical Step 0 wording.
Present those options verbatim; do not paraphrase, reorder, add, or remove options.
Ask for missing required Step 0 fields one question at a time.
Start with this exact mode question:
"Which setup matches your situation?
1) greenfield - new project or idea with little/no existing implementation.
2) brownfield - existing repo/system you want to onboard and improve."
Accept `1|2|greenfield|brownfield`.
Branch questions by mode:
- If greenfield: ask only greenfield-relevant required questions next.
- If brownfield: ask target workspace + project brief next, then brownfield profile resolution.
For capability profile, present numbered choices and accept a single number:
1) Auto-detect (recommended)
2) Locked-down
3) Standard
4) High-trust
5) All-access (explicit approval required)
If response is unclear, default to 1 and confirm.
Do not proceed to Step 1+ until all required Step 0 fields are complete.
Do not assume missing Step 0 values.
If Step 0 fields are provided inline, use them directly and ask only for remaining required fields.
Do not paste template-style multi-field blocks to the user.
After Step 0, run guided intake (required) one question at a time before generating artifacts.
If greenfield, ask:
1) project brief (2-3 sentences: what is being built, for whom, and target platform)
2) first milestone outcomes (up to 3 bullets)
3) hard constraints (timeline/budget/tech/compliance; `none` allowed)
If brownfield, ask:
1) primary onboarding outcome
2) do-not-break boundaries (security/data/runtime/deploy)
3) onboarding success definition for this run
Then auto-fill onboarding defaults under the hood:
constraints = no destructive actions, no secrets in outputs, no implementation during onboarding.
approvals = approved plan before implementation; drift `major` blocks progression.
success criteria = required artifacts generated; score threshold met; drift not `major`.
Auto-fill default scope boundaries:
in scope = onboarding artifacts + readiness/drift gates.
out of scope = implementation/deployment/refactors.
Then ask this optional prompt exactly:
"Optional: keep defaults, or type override to customize constraints/approvals/success criteria/scope/special-focus."
If user types `override`, ask one area at a time in this order:
constraints -> approvals -> success criteria -> scope -> special focus.
`keep defaults` applies only to defaults/override values; it does not skip guided intake questions.
Before artifact generation, ask this final non-blocking checkpoint exactly:
"Any final context to include before I generate artifacts? Reply `none` to continue, or add up to 3 bullets."
If user replies `none`, proceed. If user adds context, capture it and proceed.
Do not generate or update onboarding output files until required Step 0 fields are complete and guided intake is captured.
No implementation changes.
```

Inline answers are supported, but onboarding still proceeds one question at a time.

### cmd:drift-audit

```text
Run mandatory self-critique and drift audit.
Generate /ai-onboarding/output/DRIFT_CHECK_REPORT.md.
Use /ai-onboarding/templates/DRIFT_CHECK_TEMPLATE.md as the report format.
If drift is major, pause and ask for clarification.
No implementation changes.
```

### cmd:plan: <task description>

```text
Follow /ai-onboarding/AGENT_RULES.md.

Begin Phase 2 - Change Planning only.
No implementation changes.

Task:
[TASK_DESCRIPTION]
```

### cmd:impl

```text
Follow /ai-onboarding/AGENT_RULES.md.

Proceed with implementation according to the approved Change Plan.
```

### cmd:reanchor

```text
Follow /ai-onboarding/AGENT_RULES.md.

Perform a quick re-alignment check against /ai-onboarding/output/MASTER_CONTEXT.md and /ai-onboarding/output/AI_ONBOARDING_SUMMARY.md.
Do NOT regenerate onboarding output in this message.
No implementation changes in this message - alignment only.

Then continue from the already-approved Change Plan.
```

### cmd:brownfield:select

```text
Follow /ai-onboarding/profiles/PROFILE_SELECTION_PROTOCOL.md.
Resolve selected profile id/method/confidence and persist it in onboarding outputs.
No implementation changes.
```
