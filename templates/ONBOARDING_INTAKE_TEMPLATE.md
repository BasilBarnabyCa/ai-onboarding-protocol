# ONBOARDING_INTAKE_TEMPLATE.md

Use this template during Phase 1.
This template is an internal recording artifact; do not paste the full template to the user.

Process:
1. Auto-fill from available evidence first.
2. Ask required questions sequentially (one question at a time), starting with mode.
3. Ask up to 6 required questions only where needed.
4. Ask up to 3 follow-up questions only for critical unknowns.
5. Do not generate output artifacts until required Step 0 fields are complete.
6. Save final filled version to `/ai-onboarding/output/ONBOARDING_INTAKE_FILLED.md`.

---

## Mode

- Selected mode: [text goes here]
- Execution platform: [Codex|Claude Code|ChatGPT|Other]
- Platform version/model: [text goes here]
- Capability profile selection: [1|2|3|4|5]
- Capability profile resolved (tools/file access/network/approval mode): [text goes here]
- Execution role profile (optional, `domain - role`): [text goes here or default role]
- Target workspace path (brownfield): [absolute path or n/a]
- Brownfield project brief (1-3 sentences): [text goes here or n/a]
- Profile override requested: [text goes here or none]
- Selected profile id: [text goes here]
- Profile selection method (override|auto|question): [text goes here]
- Profile selection confidence (0.00-1.00): [text goes here]
- Profile selection evidence summary: [text goes here]
- Scope impact level: [low|standard|high]
- Confidence: [high|medium|low]
- Evidence: [text goes here]

## Guided Intake Answers (Post-Step 0, Required)

- Guided intake completed before generation: [yes|no]
- Greenfield project brief (2-3 sentences): [text goes here or n/a]
- Greenfield first milestone outcomes (up to 3 bullets): [text goes here or n/a]
- Greenfield hard constraints (timeline/budget/tech/compliance): [text goes here or none]
- Brownfield do-not-break boundaries: [text goes here or n/a]

## Core Intake Defaults (Applied After Guided Intake)

- Do-not-break constraints default: no destructive actions, no secrets in outputs, no implementation during onboarding.
- Required approvals default: approved plan before implementation; drift `major` blocks progression.
- Success criteria default: required artifacts generated; score threshold met; drift not `major`.
- Optional override prompt used: "Optional: keep defaults, or type override to customize constraints/approvals/success criteria/scope/special-focus."
- Core intake override (optional): [text goes here]
- Keep-defaults acknowledged (if used): [yes|no]

## Scope Boundaries

- Scope boundaries default (auto-fill after guided intake): in scope = onboarding artifacts + readiness/drift gates; out of scope = implementation/deployment/refactors
- Scope boundaries override (optional): [text goes here]

## Optional Focus

- Special focus area for this onboarding (optional): [text goes here]
- Final pre-generation additions prompt asked: [yes|no]
- Final pre-generation additions (or `none`): [text goes here]

## Context Snapshot

- Stakeholders and roles: [text goes here]
- Core workflows: [text goes here]
- High-risk controls (access/data/destructive actions): [text goes here]
- Environment/runtime notes (if applicable): [text goes here]

## Greenfield Depth Inputs (Required when mode is `greenfield`)

- Product vision (1-2 sentences): [text goes here]
- Explicit non-goals: [text goes here]
- Success metrics: [text goes here]
- MVP slices (phase list): [text goes here]
- Milestone plan: [text goes here]
- System/tech decisions and rationale: [text goes here]
- Domain model and primary workflow/loop: [text goes here]
- Acceptance criteria + release definition: [text goes here]

## Evidence Sources

- Files reviewed: [text goes here]
- Docs reviewed: [text goes here]
- History reviewed: [text goes here]

## Assumptions Ledger

- ASSUMPTION: [text goes here] | Confidence: [high|medium|low] | Validation plan: [text goes here]
- ASSUMPTION: [text goes here] | Confidence: [high|medium|low] | Validation plan: [text goes here]

## Follow-up Questions Asked (Only if Required)

- Q1: [text goes here]
- Q2: [text goes here]
- Q3: [text goes here]

## Completion Check

- Onboarding score: [0-100]
- Required questions count used: [0-6]
- Follow-up questions count used: [0-3]
- Drift status after self-critique: [none|minor|major]
- Go/No-Go decision: [go|no-go]
- Ready to generate onboarding artifacts: [yes|no]
