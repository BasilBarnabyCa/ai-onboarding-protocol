# Greenfield Master Context Artifact

## Purpose

Provide a high-rigor greenfield overlay so new projects produce implementation-grade onboarding artifacts, not lightweight summaries.

## Preconditions

- Mode is `greenfield`
- No authoritative brownfield runtime implementation exists yet, or implementation is minimal

## Required Greenfield Depth

`MASTER_CONTEXT.md` must include these greenfield-specific elements:

1. Product vision and explicit non-goals
2. Success metrics (measurable)
3. MVP slices with milestone plan
4. System/tech decisions with rationale
5. Domain model and primary workflow/loop
6. Acceptance criteria and release definition

## Required Decision Tables

### Architecture / Technology Decision Log

- Decision
- Chosen option
- Alternatives considered
- Rationale
- Risk / tradeoff

### MVP Slice Plan

- Slice
- Outcome
- Acceptance criteria
- Dependencies
- Target milestone

## Greenfield Verification Additions

Deterministic verification must include explicit results for:

- Vision/non-goal/success-metric coherence check
- MVP-to-milestone consistency check
- Decision-log completeness check
- Domain-model to workflow alignment check
- Acceptance/release criteria completeness check

Result format:

- Check
- Status (`pass|fail`)
- Evidence
- Mismatch/Action

## Integration with Global Gates

- Keep onboarding scoring policy (`>=90` standard, `>=92` high-impact)
- Keep drift hard-stop (`major` drift blocks implementation)
- Keep outputs in `/ai-onboarding/output`
