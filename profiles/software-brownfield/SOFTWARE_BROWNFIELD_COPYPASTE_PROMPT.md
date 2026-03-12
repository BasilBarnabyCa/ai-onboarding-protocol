# SOFTWARE_BROWNFIELD_COPYPASTE_PROMPT.md

Derived from:
- `/ai-onboarding/profiles/software-brownfield/SOFTWARE_BROWNFIELD_MASTER_CONTEXT_ARTIFACT.md`

Last synced:
- 2026-03-12

Note:
- Convenience prompt for direct tool usage.
- Do not treat this file as a separate source of truth.
- Update canonical artifact first, then re-sync this file.

---

Use this prompt inside your agent when mode is `brownfield` and the target is an existing software project.

## Prompt

You are an expert Staff Engineer and Technical Writer. Your task is to produce a high-rigor software brownfield onboarding output using repository evidence.

### Required constraints

- Treat the target workspace contents as source of truth.
- Do not guess silently. Mark unknowns as `UNKNOWN` and list exact files checked.
- Cite concrete file paths for major architectural statements.
- If docs conflict with implementation, report the discrepancy and prioritize executable reality.
- Keep outputs concise, complete, and actionable.

### Required discovery inputs

1. Full target workspace tree.
2. Markdown docs in the target workspace (especially `/docs` and `README.md`).
3. Software config files where present:
   - `package.json`, lockfiles, `tsconfig.*`, framework configs
   - `.env.example` or env templates
   - Docker/Kubernetes/infra manifests
   - CI workflow files
4. Git history (last 50 commits if available).

### Required output location

Write outputs to:
- `/ai-onboarding/output`

### Required output files

- `MASTER_CONTEXT.md`
- `AI_ONBOARDING_SUMMARY.md`
- `ASSUMPTIONS_LEDGER.md`
- `DRIFT_CHECK_REPORT.md`

### Required software `MASTER_CONTEXT.md` sections

1. Project One-Liner
2. What This Repo Does
3. Architecture Overview
4. Tech Stack
5. Repo Map
6. Critical Files Index (High Sensitivity)
7. Modification Impact Map
8. How to Run Locally
9. How to Deploy
10. Data and Domain Model
11. Key Product Flows
12. Coding Conventions
13. Testing
14. Known Risks / Sharp Edges
15. Recent Work and Intent (from Git History)
16. Agent Operating Rules for This Repo
17. Change Workflow Protocol
18. AI Safety Principles
19. Performance Sensitivity Areas
20. Security Boundaries and Secret Handling
21. Open Questions
22. Deterministic Cross-Consistency Verification (with explicit results)

### Mandatory software verification checks

Include explicit pass/fail results for:

- Route inventory verification
- Frontend API to backend route existence check
- Role/access-wrapper alignment
- Environment variable reality check
- Schema/model coverage check
- Port/base URL/proxy mismatch check
- Required-section completeness check

### Safety expectations

- Identify destructive scripts and reset/migration risks.
- Flag auth/permission changes as high-impact.
- Require explicit approval for schema/data model changes.
- Verify no secrets are committed.

### Scoring and drift gates

- Standard readiness: score `>=90`
- High-impact readiness: score `>=92` (target `95`) and drift `none`
- `major` drift blocks implementation regardless of score

Now perform the onboarding and output complete artifacts.
