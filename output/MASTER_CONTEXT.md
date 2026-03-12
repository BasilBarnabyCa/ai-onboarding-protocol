# MASTER_CONTEXT.md

Mode: greenfield
Execution platform: Codex
Platform version/model: GPT-5
Capability profile: local shell tools, workspace-write filesystem, network-restricted runtime, approval-based escalation for protected operations.
Simulation status: true

## 1. Project One-Liner
Create a domain-agnostic onboarding framework configured for cybersecurity use, with deterministic drift control and high-impact readiness gates.

## 2. Mode and Scope Boundaries
- Mode: greenfield.
- In scope: onboarding intake, context synthesis, scoring, drift gates, planning handoff.
- Out of scope: direct production control changes, destructive actions, sensitive-data operations.

## 3. Problem, Outcomes, and Success Criteria
Problem: onboarding drift creates unsafe execution risk.
Desired outcomes: consistent context quality with low user burden and explicit risk controls.
Success criteria: score >=92 for high-impact scope, drift `none`, and approval-gated execution.

## 4. Stakeholders and Roles
- Security lead: governance owner and high-impact approver.
- Client owner: business and risk approver.
- SOC analyst: primary operator persona.
- AI agent: protocol-constrained execution assistant.

## 5. Operating Model / System Overview
Process flow:
1. Alignment
2. Drift audit
3. Change planning
4. Pre-implementation drift recheck
5. Implementation
This sequence is defined by `/ai-onboarding/AI_EXECUTION_PROTOCOL.md` and constrained by `/ai-onboarding/AGENT_RULES.md`.

## 6. Components, Assets, or Process Areas
- Governance rules: `/ai-onboarding/AGENT_RULES.md`
- Alignment protocol: `/ai-onboarding/ARCHITECTURE_ALIGNMENT.md`
- Bootstrap contract: `/ai-onboarding/AI_AGENT_BOOTSTRAP_AND_ARCHITECTURAL_COMPREHENSION_CONTRACT.md`
- Generator: `/ai-onboarding/AI_ONBOARDING_MASTER_CONTEXT_GENERATOR.md`
- Intake template: `/ai-onboarding/ONBOARDING_INTAKE_TEMPLATE.md`
- Drift template: `/ai-onboarding/DRIFT_CHECK_TEMPLATE.md`

## 7. Tooling and Platform Stack (if applicable)
- Execution platform: Codex (GPT-5)
- Artifact format: markdown files in `/ai-onboarding/output`
- Versioning: git workflow with commit conventions and review gates

## 8. Repository / Workspace Map (if applicable)
- `/ai-onboarding/*.md`: source protocol documents
- `/ai-onboarding/output/*.md`: generated onboarding artifacts
- `/ai-onboarding/output/archive/*`: historical snapshots

## 9. Data and Information Handling Model
- No secrets or sensitive client data in onboarding artifacts.
- Unknowns and assumptions must be explicit and tracked with confidence.
- Evidence references should point to current docs or explicit user inputs.

## 10. Security, Compliance, and Access Controls
- Dual approval required for high-impact actions.
- Major drift is a hard block.
- High-impact readiness requires score >=92 and drift `none`.
- Platform capability constraints must remain explicit and consistent.

## 11. Delivery / Release / Execution Workflow
- Generate onboarding artifacts in `/ai-onboarding/output`.
- Verify deterministic consistency and scoring.
- Run drift audit and capture Go/No-Go.
- Enter planning phase only after onboarding pass.
- Enter implementation only after plan approval and drift recheck pass.

## 12. Change Impact Map
- Scoring policy changes alter execution eligibility.
- Drift policy changes alter safety thresholds.
- Platform profile changes alter available tool pathways and risk controls.

## 13. Validation and Verification Strategy
- Required-section completeness checks.
- Cross-file consistency checks for scope, constraints, and platform profile.
- Drift audits at alignment and pre-implementation gates.

## 14. Known Risks / Sharp Edges
- Stakeholder scope drift.
- Compliance interpretation mismatch.
- Treating simulation outputs as production-ready without revalidation.

## 15. Recent Intent Signals (from history/docs)
- Framework generalized beyond coding-specific workflows.
- Drift gating and stronger readiness thresholds were added.
- Platform declaration now required in intake and alignment.

## 16. Operating Rules for Agents in This Repo
- Keep phases separate.
- Follow bounded question budget.
- Use output contracts and templates.
- Block implementation on major drift or insufficient readiness.

## 17. Open Questions
- Which control framework (if any) must be mapped before production rollout?
- Who is final signatory for moving from simulation to production use?

## 18. Deterministic Cross-Consistency Verification (with results)
- Required outputs present and non-empty: pass.
- Scope and constraints consistent across outputs: pass.
- Platform profile consistent across intake, summary, context, and drift report: pass.
- Assumptions ledger referenced in drift and summary outputs: pass.
- High-impact threshold check (>=92 + drift none): pass.

## 19. Self-Critique and Drift Control Status
- Onboarding score: 94
- Scope impact level: high
- Drift status: none
- Decision: Go for high-impact readiness under current simulation constraints.
