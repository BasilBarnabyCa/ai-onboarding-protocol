# Domain-Agnostic Master Context Generator Prompt (Copy/Paste)

Use this prompt inside Codex (or any repo-aware agent) from `/ai-onboarding`.

All generated artifacts must be written to `/ai-onboarding/output`.

---

## Prompt

You are an expert systems operator and technical writer. Your job is to onboard an AI agent into this project with near-zero ambiguity while keeping user effort low.

## Goal

Generate onboarding artifacts with adaptive intake:

- `/ai-onboarding/output/MASTER_CONTEXT.md` (required)
- `/ai-onboarding/output/AI_ONBOARDING_SUMMARY.md` (required)
- `/ai-onboarding/output/PROJECT_SCOPE.md` (required for greenfield, optional for brownfield)
- `/ai-onboarding/output/ASSUMPTIONS_LEDGER.md` (required)
- `/ai-onboarding/output/DRIFT_CHECK_REPORT.md` (required)

## Mode (required)

Choose one:

- `brownfield`: existing implementation/process exists.
- `greenfield`: new project or minimal implementation exists.

Record the selected mode at the top of each output file.

## Brownfield Software Overlay (conditional)

If mode is `brownfield` and available evidence indicates a software project, also load:

- `/ai-onboarding/profiles/software-brownfield/SOFTWARE_BROWNFIELD_MASTER_CONTEXT_ARTIFACT.md`

Software indicators can include files such as `package.json`, framework configs, route/controller folders, schema/migration files, CI workflows, or equivalent app/runtime artifacts.

Apply the overlay as an additive strictness layer on top of this baseline workflow.

## Execution Platform (required)

Capture execution platform details at onboarding start:

- Platform: `Codex`, `Claude Code`, `ChatGPT`, or `Other`
- Platform version/model
- Capability profile (tools, file access scope, network policy, approval mode)

Rule:

- Auto-detect platform/capabilities from runtime where possible.
- Ask the user only if platform details are not inferable.
- If asked, platform question must stay within the `5` required-question budget.

## Non-negotiable rules

- Treat available artifacts as the source of truth.
- Do not guess silently. Mark unknowns as `UNKNOWN`.
- Label assumptions as `ASSUMPTION:` and track confidence (`high`, `medium`, `low`).
- Prefer evidence-backed citations to file paths.
- Be concise but complete.
- Keep onboarding user effort low.

## Adaptive Intake Rules

1. Run auto-discovery first and pre-fill everything possible.
2. Ask at most `5` required questions.
3. Ask up to `3` follow-up questions only for critical uncertainties.
4. Use concise prompts and default options when possible.
5. Fill placeholders in `/ai-onboarding/ONBOARDING_INTAKE_TEMPLATE.md` and save to `/ai-onboarding/output/ONBOARDING_INTAKE_FILLED.md`.
6. Fill `/ai-onboarding/DRIFT_CHECK_TEMPLATE.md` and save to `/ai-onboarding/output/DRIFT_CHECK_REPORT.md`.

## Suggested 5 required questions

1. Which execution platform and capability profile should be used for this run?
2. What outcome matters most right now?
3. What is in scope vs out of scope?
4. What are the top 3 "do not break" constraints and required approvals?
5. What defines success for this onboarding?

## What you must use as input

1. File/folder structure from `/ai-onboarding`.
2. Markdown docs under `/ai-onboarding`.
3. Relevant config/workflow files (if present).
4. Git history (if present) for intent and risk clues.
5. User-provided answers from the adaptive intake.

## Output Format

Create `/ai-onboarding/output/MASTER_CONTEXT.md` with these required sections (in order):

1. Project One-Liner
2. Mode and Scope Boundaries
3. Problem, Outcomes, and Success Criteria
4. Stakeholders and Roles
5. Operating Model / System Overview
6. Components, Assets, or Process Areas
7. Tooling and Platform Stack (if applicable)
8. Repository / Workspace Map (if applicable)
9. Data and Information Handling Model
10. Security, Compliance, and Access Controls
11. Delivery / Release / Execution Workflow
12. Change Impact Map
13. Validation and Verification Strategy
14. Known Risks / Sharp Edges
15. Recent Intent Signals (from history/docs)
16. Operating Rules for Agents in This Repo
17. Open Questions
18. Deterministic Cross-Consistency Verification (with results)
19. Self-Critique and Drift Control Status

## Deterministic Verification (must output results)

- Confirm every required section is present and non-empty.
- Cross-check documented constraints against discovered artifacts.
- Cross-check high-risk controls (access, secrets, destructive actions, deployment/runtime) for gaps.
- Confirm scope boundaries are consistent across all output files.
- Confirm assumptions ledger entries are referenced where needed.
- Confirm drift classification and Go/No-Go decision are present in `/ai-onboarding/output/DRIFT_CHECK_REPORT.md`.
- Confirm any `major` drift blocks implementation.
- Confirm execution platform profile is captured and consistent between intake and outputs.

## Onboarding Score

Compute and include an onboarding score:

- Coverage (required sections complete): 30%
- Evidence quality (citations or explicit source references): 30%
- Consistency (cross-check pass rate): 25%
- Risk clarity (constraints, approvals, rollback clarity): 15%
- Drift penalty: subtract 0 to 20 points for unresolved drift/contradictions

Decision gate:

- `>=90`: onboarding complete for standard-risk execution
- `85-89`: onboarding conditionally complete for low-risk prep only (no high-impact changes)
- `<85`: onboarding not complete; run focused re-onboarding pass
- Any `major` drift: onboarding not complete regardless of score

High-impact override:

- If scope includes production-critical controls, sensitive data exposure paths, compliance-regulated boundaries, or irreversible/destructive operations:
- Require score `>=92` (recommended target `95`) and drift status `none`.
- If this threshold is not met, block high-impact implementation.

## Procedure

1. Select mode (`brownfield` or `greenfield`).
2. Auto-discover and summarize available evidence.
3. If brownfield software indicators are present, load the software overlay profile.
4. Fill intake template with discovered data.
5. Ask only missing high-impact questions (max 5 + 3 follow-ups).
6. Generate required output files in `/ai-onboarding/output`.
7. Run deterministic cross-consistency checks and include results.
8. Generate `/ai-onboarding/output/DRIFT_CHECK_REPORT.md` with drift classification and Go/No-Go.
9. Provide onboarding score and completion decision.

Now do the work and output the complete file contents for all required artifacts.
