# Software Brownfield Profile

Use this profile when:

- Mode is `brownfield`
- Target workspace is an existing software project
- You need deeper software-specific verification beyond the agnostic baseline

Selection is routed by:

- `/ai-onboarding/profiles/PROFILE_SELECTION_PROTOCOL.md`
- `/ai-onboarding/profiles/PROFILE_REGISTRY.md`

Primary artifact:

- `SOFTWARE_BROWNFIELD_MASTER_CONTEXT_ARTIFACT.md`
- `SOFTWARE_BROWNFIELD_COPYPASTE_PROMPT.md` (derived convenience prompt)

How to apply:

1. Run the standard onboarding flow from `/ai-onboarding`.
2. If project evidence indicates software brownfield work (for example: `package.json`, route folders, schema files, CI manifests), load the software artifact.
3. Merge its required checks and section structure into the generated `MASTER_CONTEXT.md`.
4. Keep all output files in `/ai-onboarding/output`.

This profile is additive. It does not replace core drift/scoring guardrails.
