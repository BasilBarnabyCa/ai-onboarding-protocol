# MASTER_CONTEXT.md

Mode: greenfield
Simulation status: true

## 1. Project One-Liner
Create a cybersecurity-ready onboarding and execution framework that is domain-agnostic, drift-resistant, and safe for high-impact work.

## 2. Mode and Scope Boundaries
- Mode: greenfield.
- In scope: onboarding intake, context generation, risk controls, change planning gates, drift checks.
- Out of scope: direct production changes, sensitive-data operations, irreversible actions without approvals.

## 3. Problem, Outcomes, and Success Criteria
Problem: onboarding quality drifts over time and can lead to unsafe execution.
Desired outcomes: high-fidelity context, minimal user burden, deterministic safety checks.
Success criteria: score >=92 for high-impact scope, drift status `none`, explicit approvals for high-impact changes.

## 4. Stakeholders and Roles
- Security lead: governance owner and high-impact approver.
- Client owner: business/risk approver.
- SOC analyst: primary operator of documented workflows.
- AI agent: guided executor under protocol constraints.

## 5. Operating Model / System Overview
The process follows phased gates:
1. Alignment
2. Drift audit
3. Change planning
4. Drift recheck
5. Implementation
This sequence is defined in `/ai-onboarding/AI_EXECUTION_PROTOCOL.md` and constrained by `/ai-onboarding/AGENT_RULES.md`.

## 6. Components, Assets, or Process Areas
- Governance rules: `/ai-onboarding/AGENT_RULES.md`
- Alignment protocol: `/ai-onboarding/ARCHITECTURE_ALIGNMENT.md`
- Bootstrap contract: `/ai-onboarding/AI_AGENT_BOOTSTRAP_AND_ARCHITECTURAL_COMPREHENSION_CONTRACT.md`
- Execution protocol: `/ai-onboarding/AI_EXECUTION_PROTOCOL.md`
- Intake template: `/ai-onboarding/ONBOARDING_INTAKE_TEMPLATE.md`
- Drift template: `/ai-onboarding/DRIFT_CHECK_TEMPLATE.md`

## 7. Tooling and Platform Stack (if applicable)
- Markdown-based process artifacts
- Git-based version control and review
- Local execution from `/ai-onboarding`

## 8. Repository / Workspace Map (if applicable)
- `/ai-onboarding/*.md`: protocol source files
- `/ai-onboarding/output/*.md`: generated onboarding artifacts

## 9. Data and Information Handling Model
- Onboarding artifacts may contain operational context but must not include secrets or sensitive identifiers.
- Assumptions and unknowns must be explicit and tracked.
- Evidence references should point to local files or user statements.

## 10. Security, Compliance, and Access Controls
- No secret material in outputs.
- High-impact actions require explicit approvals.
- Major drift blocks implementation.
- Sensitive-data paths require highest readiness gate.

## 11. Delivery / Release / Execution Workflow
- Produce onboarding artifacts in `/ai-onboarding/output`.
- Verify consistency and score.
- Run drift audit and obtain Go/No-Go.
- Enter change planning only after alignment pass.
- Enter implementation only after plan approval and drift recheck pass.

## 12. Change Impact Map
- Changes to scoring or drift policy affect readiness decisions and execution eligibility.
- Changes to intake template impact completeness and confidence quality.
- Changes to guardrails impact risk posture across all future runs.

## 13. Validation and Verification Strategy
- Deterministic checks across files for scope and constraints.
- Drift audit at alignment and pre-implementation gates.
- Score-based readiness with high-impact override.

## 14. Known Risks / Sharp Edges
- Ambiguous stakeholder scope can create drift.
- Hidden compliance requirements can invalidate readiness assumptions.
- Reusing simulation outputs as production-ready docs without revalidation is unsafe.

## 15. Recent Intent Signals (from history/docs)
- Repository evolved from coding-specific onboarding to domain-agnostic execution.
- Drift controls and stricter readiness thresholds were added to prevent process drift.
- Output path was standardized to `/ai-onboarding/output`.

## 16. Operating Rules for Agents in This Repo
- Respect phase separation.
- Do not collapse alignment, planning, and implementation.
- Keep onboarding question count bounded.
- Use templates and output contract paths.

## 17. Open Questions
- Which compliance control set is required for the first real deployment?
- Which stakeholder owns final sign-off for promotion from simulation to production?

## 18. Deterministic Cross-Consistency Verification (with results)
- Required artifacts present: pass (`MASTER_CONTEXT`, `AI_ONBOARDING_SUMMARY`, `PROJECT_SCOPE`, `ASSUMPTIONS_LEDGER`, `ONBOARDING_INTAKE_FILLED`, `DRIFT_CHECK_REPORT`).
- Scope consistency across artifacts: pass.
- Constraint consistency across artifacts: pass.
- Assumptions ledger references present in summary/drift report: pass.
- High-impact threshold check (>=92 + drift none): pass.

## 19. Self-Critique and Drift Control Status
- Onboarding score: 94
- Scope impact level: high
- Drift status: none
- Decision: Go for high-impact readiness threshold under current simulation assumptions.
