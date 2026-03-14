# Domain-Agnostic Master Context Generator Prompt (Copy/Paste)

Use this prompt inside Codex (or any repo-aware agent) from `/ai-onboarding`.

All generated artifacts must be written to `/ai-onboarding/output`.

---

## Prompt

You are an expert systems operator and technical writer. Your job is to onboard an AI agent into this project with near-zero ambiguity while keeping user effort low.

## Goal

Generate these onboarding artifacts:

- `/ai-onboarding/output/MASTER_CONTEXT.md` (required)
- `/ai-onboarding/output/AI_ONBOARDING_SUMMARY.md` (required)
- `/ai-onboarding/output/PROJECT_SCOPE.md` (required for greenfield, optional for brownfield)
- `/ai-onboarding/output/ASSUMPTIONS_LEDGER.md` (required)
- `/ai-onboarding/output/DRIFT_CHECK_REPORT.md` (required)
- `/ai-onboarding/output/ONBOARDING_INTAKE_FILLED.md` (required)

## Quality Bar (Non-Negotiable)

Outputs must be implementation-grade, not high-level narrative.

Minimum quality characteristics:

- Evidence traceability: major claims cite concrete file paths.
- Discrepancy clarity: docs vs implementation mismatches are listed explicitly.
- Unknown control: unknowns are marked as `UNKNOWN` with exact files checked.
- Risk operability: risk items include impact and verification action.
- Verification determinism: cross-consistency checks output explicit `pass|fail` results with evidence.

## Mode (required)

Choose one:

- `brownfield`: existing implementation/process exists.
- `greenfield`: new project or minimal implementation exists.

Record selected mode at top of each output file.

## Execution Platform (required)

Capture execution platform details at onboarding start:

- Platform: `Codex`, `Claude Code`, `ChatGPT`, or `Other`
- Platform version/model
- Capability profile selection (`1-5`)
- Optional execution role profile (`domain - role`)

Capability profile selector:

1. `1` Auto-detect (recommended)
2. `2` Locked-down
3. `3` Standard
4. `4` High-trust
5. `5` All-access (explicit approval required)

Rule:

- Auto-detect platform/capabilities where possible.
- Ask for numeric profile selection only (`1-5`), not free-text capability fields.
- If auto-detection is available, present detected profile and ask user to accept with `1` or override with another option.
- If response is unclear, default to `1` and confirm.
- Optional execution role profile must not block progression.

## Overlay Rules

### Brownfield overlay (required in brownfield mode)

Resolve profile first:

- `/ai-onboarding/profiles/PROFILE_SELECTION_PROTOCOL.md`
- `/ai-onboarding/profiles/PROFILE_REGISTRY.md`

If selected profile is `software-brownfield`, load:

- `/ai-onboarding/profiles/software-brownfield/SOFTWARE_BROWNFIELD_MASTER_CONTEXT_ARTIFACT.md`

### Greenfield depth overlay (required in greenfield mode)

Load:

- `/ai-onboarding/profiles/greenfield/GREENFIELD_MASTER_CONTEXT_ARTIFACT.md`

And enforce:

- Product vision + non-goals + success metrics.
- MVP slices + milestone plan.
- System/tech decisions with rationale (and rejected options when known).
- Domain model + core workflow/loop + acceptance criteria.
- Test strategy + release definition (exit criteria).

## Non-negotiable rules

- Treat available artifacts as source of truth.
- Do not guess silently; mark unknowns as `UNKNOWN`.
- Label assumptions as `ASSUMPTION:` with confidence (`high|medium|low`).
- Prefer evidence-backed file-path citations.
- Be concise but complete.
- Keep onboarding user effort low.

## Adaptive Intake Rules

1. Run auto-discovery first and pre-fill everything possible.
2. Ask required questions sequentially (one question at a time); do not paste a template block.
3. Ask at most `8` required questions (including mode-specific composite questions when needed).
4. Ask up to `3` follow-up questions only for critical uncertainty.
5. Do not generate or update onboarding output files until required Step 0 fields are complete and guided intake is captured.
6. Save filled intake to `/ai-onboarding/output/ONBOARDING_INTAKE_FILLED.md`.
7. Fill drift template and save to `/ai-onboarding/output/DRIFT_CHECK_REPORT.md`.

## Suggested required questions

1. Ask mode first with explicit plain-language definitions:
- "Which setup matches your situation?
- 1) greenfield - new project or idea with little/no existing implementation.
- 2) brownfield - existing repo/system you want to onboard and improve."
- Accept `1|2|greenfield|brownfield`.
2. Ask platform only if not auto-detected.
3. Ask platform version/model only if not auto-detected.
4. Ask capability profile selector (`1-5`).
5. If brownfield: ask target workspace path + project brief (1-3 sentences).
6. Run guided intake (required, one question at a time):
- If greenfield: ask project brief, first milestone outcomes, and hard constraints.
- If brownfield: ask primary onboarding outcome, do-not-break boundaries, and onboarding success definition.
7. Auto-fill onboarding defaults (constraints, approvals, success criteria, scope boundaries).
8. Ask this optional prompt exactly:
- "Optional: keep defaults, or type override to customize constraints/approvals/success criteria/scope/special-focus."
- If user types `override`, ask one area at a time in this order:
- constraints -> approvals -> success criteria -> scope -> special focus.
9. `keep defaults` only applies to defaults/override values; it does not skip guided intake questions.
10. Before artifact generation, ask this final non-blocking checkpoint exactly:
- "Any final context to include before I generate artifacts? Reply `none` to continue, or add up to 3 bullets."
11. If greenfield and missing: ask one composite greenfield-depth question (vision, non-goals, metrics, MVP/milestones, decisions, domain loop, acceptance/release).

Optional question (non-blocking):

- Execution role profile in format `domain - role`.

## What to use as input

1. File/folder structure from `/ai-onboarding`.
2. For brownfield: file/folder structure from target workspace path.
3. Markdown docs under `/ai-onboarding` and (for brownfield) under target workspace.
4. Relevant config/workflow files (if present) from target workspace.
5. Git history (if present) for intent/risk clues.
6. User-provided intake answers.

## Required `MASTER_CONTEXT.md` sections (in order)

1. Project One-Liner
2. Source of Truth Hierarchy
3. What This Project/Repo Does
4. Architecture Overview
5. Tech Stack / Platform Stack
6. Repo/Workspace Map
7. Critical Files Index (High Sensitivity)
8. Modification Impact Map
9. How to Run/Operate Locally
10. Deployment/Release Model
11. Data & Domain Model
12. Key Product/Operational Flows
13. Conventions (Coding or Operating)
14. Testing & Validation Strategy
15. Known Risks / Sharp Edges (Risk Register)
16. Recent Work & Intent Signals
17. Agent Operating Rules for This Repo
18. Change Workflow Protocol
19. AI Safety Principles (Non-Negotiable)
20. Performance Sensitivity Areas
21. Security Boundaries & Secret Handling
22. Open Questions
23. Deterministic Cross-Consistency Verification (Explicit Results)

## Brownfield mandatory depth requirements

When mode is `brownfield`, `MASTER_CONTEXT.md` must include:

- Per-file summary table for markdown docs under `/docs` (or equivalent doc root):
- file path
- summary
- implementation alignment (`aligned|partially stale|stale|unknown`)
- Discrepancy register for docs vs implementation with impact notes.
- Environment variable reality table (`USED|INJECTED ONLY|LEGACY/UNUSED|UNKNOWN`).
- Route/API alignment results where applicable.

## Greenfield mandatory depth requirements

When mode is `greenfield`, `MASTER_CONTEXT.md` must include:

- Product vision + non-goals + measurable success criteria.
- MVP slices with milestone plan.
- Architecture/technology decisions with rationale.
- Domain model and primary workflow/loop.
- Acceptance criteria and release definition.

## Required `AI_ONBOARDING_SUMMARY.md` structure

1. Project Understanding (with evidence)
2. Safe Change Rules (binding list with evidence)
3. How Work Will Be Executed Safely
4. Risks and Ambiguities (`UNKNOWN` and `ASSUMPTION` items)
5. Sharp-Edge Acknowledgment Checklist (`Understood|Needs clarification`)
6. Readiness Snapshot (score, drift, go/no-go)
7. Alignment Confirmation statement

## Deterministic verification output format (required)

Section 23 must contain result tables, not procedures.

### Table A: Required section completeness

- Check
- Status (`pass|fail`)
- Evidence
- Notes

### Table B: Cross-consistency checks

- Check
- Status (`pass|fail`)
- Evidence
- Mismatch/Action

Minimum checks:

- Required section non-empty check
- Constraint consistency across artifacts
- Scope consistency across artifacts
- High-risk control consistency (access/secrets/destructive/deploy)
- Assumptions ledger cross-reference check
- Drift report fields present and complete
- Platform version/model and capability profile selection consistency between intake and outputs
- Mode-specific checks:
- Brownfield: profile selection consistency + route/API/env checks where applicable
- Greenfield: vision/MVP/acceptance/release checks present and coherent

## Onboarding score

Compute and include onboarding score:

- Coverage completeness: 25%
- Evidence quality: 25%
- Cross-consistency pass rate: 25%
- Risk and constraint clarity: 15%
- Mode-depth completeness (greenfield or brownfield requirements): 10%
- Drift penalty: subtract 0-20 for unresolved contradictions

Decision gate:

- `>=90`: onboarding complete for standard-risk execution
- `85-89`: low-risk preparation only (no high-impact implementation)
- `<85`: onboarding incomplete
- Any `major` drift: onboarding incomplete regardless of score

High-impact override:

- If scope includes production-critical controls, sensitive data paths, compliance boundaries, or irreversible operations:
- Require `>=92` (target `95`) and drift `none`.

## Procedure

1. Select mode (`greenfield` or `brownfield`).
2. Capture platform profile selection (+ optional execution role profile).
3. If brownfield: capture workspace path + project brief, then resolve profile.
4. Run guided intake (mode-specific) after Step 0 and before defaults/overrides.
5. Auto-fill onboarding defaults (constraints, approvals, success criteria, scope boundaries).
6. Ask optional overrides using the standard `keep defaults` / `override` prompt.
7. Ask a final non-blocking "anything else to add" checkpoint before generation.
8. Do not generate outputs until required Step 0 fields are complete and guided intake is captured.
9. Auto-discover and summarize evidence.
10. Fill intake template and ask only missing high-impact questions.
11. Generate required output files in `/ai-onboarding/output`.
12. Run deterministic verification and record explicit results.
13. Generate/update drift report with classification and go/no-go.
14. Output onboarding score and completion decision.

Now do the work and output complete contents for all required artifacts.
