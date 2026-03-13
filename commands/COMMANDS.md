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
Ask for any missing required Step 0 fields before any alignment work.
Do not proceed to Step 1+ until all required Step 0 fields are complete.
Do not assume missing Step 0 values.
If Step 0 fields are provided inline, use them directly and ask only for remaining required fields.
No implementation changes.
```

Optional one-message kickoff pattern with `cmd:onboard`:

```text
cmd:onboard
Mode: [brownfield|greenfield]
Platform: [Codex|Claude Code|ChatGPT|Other]
Platform profile: [model + capability summary]
Execution role profile: [domain - role, optional]
Target workspace: [absolute path, brownfield only]
Project brief: [1-3 sentences, brownfield only]
Profile override: [optional]
```

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
