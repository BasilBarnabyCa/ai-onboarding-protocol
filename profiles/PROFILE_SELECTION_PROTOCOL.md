# PROFILE_SELECTION_PROTOCOL.md

Use this protocol when mode is `brownfield`.

## Required Inputs

1. Target workspace path (absolute path).
2. Brief project description (1-3 sentences from user).
3. Optional profile override (if user already knows the domain profile).

## Selection Procedure

1. Validate override first:
- If override matches an `active` profile, select it.

2. Auto-score active profiles from evidence:
- Use indicators in `/ai-onboarding/profiles/PROFILE_REGISTRY.md`.
- Score each profile from `0.00` to `1.00` based on evidence density and consistency.

3. Confidence rule:
- Auto-select if top score `>=0.70` and margin over second score `>=0.15`.

4. Ambiguity rule:
- If confidence rule fails, ask one disambiguation question.
- Keep this within onboarding question budget.

5. Persist result:
- Record selected profile, score, and selection method (`override`, `auto`, `question`) in onboarding outputs.

## Output Fields (must be persisted)

- Selected profile id
- Selection method
- Selection confidence score
- Evidence summary
- Any disambiguation question used

## Failure Handling

- If no active profile is appropriate, use agnostic baseline and mark profile as `none`.
- Mark unresolved profile fit as `ASSUMPTION` with validation plan.
