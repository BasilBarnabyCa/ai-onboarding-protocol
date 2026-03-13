# Software Brownfield Master Context Artifact

## Purpose

Provide a software-specific, high-rigor overlay for brownfield onboarding. This restores deep repository checks for existing codebases while preserving the agnostic workflow, scoring, and drift gates.

## Preconditions

- Mode is `brownfield`
- Existing software workspace is available and readable
- Target workspace path is explicitly declared

## Source-of-Truth Rules

- Treat target workspace contents as primary evidence.
- If unknown, mark `UNKNOWN` and list exact files checked.
- Cite concrete file paths for architectural claims.
- If docs conflict with implementation, report discrepancy and follow executable reality.

## Required Discovery Inputs

1. Full target workspace tree.
2. All markdown docs in target workspace, especially `/docs` and `README.md`.
3. Software config files where present, including:
   - `package.json`, lockfiles, `tsconfig.*`, framework configs
   - `.env.example` or env templates
   - Docker/Kubernetes/infra manifests
   - CI workflow files
4. Git history (at least last 50 commits if available).

## Required MASTER_CONTEXT Software Sections

Use these sections in the output `MASTER_CONTEXT.md` when software profile is active:

1. Project One-Liner
2. Source of Truth Hierarchy
3. What This Repo Does
4. Architecture Overview
5. Tech Stack
6. Repo Map
7. Critical Files Index (High Sensitivity)
8. Modification Impact Map
9. How to Run Locally
10. How to Deploy
11. Data and Domain Model
12. Key Product Flows
13. Coding Conventions
14. Testing
15. Known Risks / Sharp Edges
16. Recent Work and Intent (from Git History)
17. Agent Operating Rules for This Repo
18. Change Workflow Protocol
19. AI Safety Principles
20. Performance Sensitivity Areas
21. Security Boundaries and Secret Handling
22. Open Questions
23. Deterministic Cross-Consistency Verification (with explicit results)

## Mandatory Software Cross-Consistency Checks

The verification section must include explicit results for:

- Route inventory verification
- Frontend API to backend route existence check
- Role and access-wrapper alignment
- Environment variable reality check
- Schema/model coverage check
- Port/base URL/proxy mismatch check
- Required-section completeness check

Result format is mandatory:

- Each check must be reported as `pass|fail`.
- Each result must include concrete evidence file paths.
- Any failed check must include a mismatch note and required corrective action.

Use table format:

- Check
- Status (`pass|fail`)
- Evidence
- Mismatch/Action

## Mandatory Brownfield Evidence Tables

`MASTER_CONTEXT.md` must include:

- Per-doc summary table for markdown docs under `/docs` (or equivalent):
- file path
- summary
- implementation alignment (`aligned|partially stale|stale|unknown`)
- Discrepancy register table for docs-vs-implementation conflicts:
- claim source
- implementation evidence
- impact
- required correction
- Environment variable reality table:
- variable
- required/default
- where used
- status (`USED|INJECTED ONLY|LEGACY/UNUSED|UNKNOWN`)

## Additional Safety Checks for Software Brownfield

- Identify destructive scripts and reset/migration risks.
- Flag auth and permission boundary changes as high-impact.
- Require explicit approval for schema/data model changes.
- Verify secrets are never committed.

## Self-Critique Prompts

- Clarity: Are outputs unambiguous and evidence-backed?
- Completeness: Are all required sections and checks present?
- Hallucination Control: Are unknowns and assumptions explicit?
- Deterministic Rigor: Are cross-check results concrete and reproducible?
- Bias/Overreach: Did the output document reality rather than redesign it?

## Integration with Current Gates

- Keep current onboarding scoring policy (`>=90` standard, `>=92` high-impact).
- Keep drift hard-stop (`major` drift blocks implementation).
- Keep outputs under `/ai-onboarding/output`.
