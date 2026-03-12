# Codex Master Context Generator Prompt (Copy/Paste)

Use this prompt inside Codex (or any repo-aware agent) **from the root of the repository**.

---

## Prompt

You are an expert Staff Engineer and Technical Writer. Your job is to onboard an AI coding agent (Codex) into this repository with near-zero ambiguity.

## Goal

Produce a single Markdown file named: `MASTER_CONTEXT.md` that explains everything Codex needs to be productive and safe in this repo.

## Non-negotiable rules

* Treat the repository contents as the ONLY source of truth.
* Do not guess. If something is unknown, explicitly mark it as `UNKNOWN` and list the exact files you checked.
* Prefer linking to real files/paths in the repo.
* Be concise but complete; optimize for *agent usefulness* (not marketing).
* Capture conventions and “sharp edges” (things that will break if changed).
* If multiple apps exist (monorepo), document each clearly.

## What you must use as input

1. The full file/folder structure (tree).
2. All Markdown documentation found in:

   * `/docs` (MANDATORY: fully scan this folder recursively and treat it as high-priority context)
   * `/README.md`
   * any `*.md` elsewhere relevant
   * Any architectural decision records (ADR), RFCs, design notes, or planning documents
     If `/docs` exists, you MUST:
   * Summarize each file individually before synthesizing.
   * Extract architectural intent, constraints, and conventions.
   * Note any discrepancies between docs and implementation.
3. Key config files (as applicable):

   * `package.json`, `pnpm-lock.yaml`, `yarn.lock`, `npm-lock.json`
   * `tsconfig.json`, `vite.config.*`, `next.config.*`, `nuxt.config.*`
   * `webpack.*`, `babel.*`
   * `.env.example`, `.env.*` templates
   * `docker-compose.yml`, `Dockerfile`, Kubernetes manifests
   * `terraform/`, `bicep/`, `pulumi/`, CI workflows (`.github/workflows/*`)
4. Git commit history (at least last 50 commits). Use it to infer intent, major milestones, and risky areas.

## Output format

Create exactly one Markdown document: `MASTER_CONTEXT.md`.

### Required sections (in this order)

1. **Project One-Liner**
2. **What This Repo Does**

   * Problem, users, key workflows
3. **Architecture Overview**

   * High-level diagram in Mermaid (keep simple)
   * Major components/services and how they talk
4. **Tech Stack**

   * Frontend, backend, database, auth, hosting, CI/CD, observability
5. **Repo Map**

   * Annotated directory tree (top 3–4 levels)
   * “Where to change X” quick pointers
6. **Critical Files Index (High Sensitivity)**

   * List the most sensitive or high-impact files
   * For each file: explain why it is sensitive and what breaks if modified incorrectly
7. **Modification Impact Map**

   * If modifying X → what else is affected?
   * Map models to routes, routes to frontend calls, env vars to deployment
   * Highlight cascading impact risks
8. **How to Run Locally**

   * Prereqs
   * Install steps
   * Environment variables (table: name | required | default | where used)
   * Common commands (dev/test/lint/build)
9. **How to Deploy**

   * Environments (dev/stage/prod)
   * Deployment pipeline steps
   * Infra-as-code notes (if present)
   * Where secrets are configured
10. **Data & Domain Model**

* Key entities
* Where schemas live
* Migrations strategy
* Optional Mermaid ER diagram

11. **Key Product Flows**

* Step-by-step flows
* Link to code entrypoints

12. **Coding Conventions**

* Patterns used
* Naming conventions
* Error handling
* Logging

13. **Testing**

* Frameworks
* Locations
* How to run

14. **Known Risks / Sharp Edges**

15. **Recent Work & Intent (from Git History)**

16. **Codex Operating Rules for This Repo**

17. **Change Workflow Protocol**

18. **AI Safety Principles (Non-Negotiable Rules)**

19. **Performance Sensitivity Areas**

20. **Security Boundaries & Secret Handling**

21. **Open Questions**

22. **Deterministic Cross-Consistency Verification (Mandatory)**

* Must contain:

  * Route inventory verification
  * Frontend API → Backend route existence check
  * Role & access-wrapper alignment
  * Environment variable reality check
* This section must contain explicit verification results — not just instructions.

---

## Procedure you must follow

1. Generate a repo tree summary.

2. Read and summarize existing docs.

3. Identify app entrypoints.

4. Extract stack from config files.

5. Scan commit history for intent.

6. Synthesize into `MASTER_CONTEXT.md`.

7. **Final Deterministic Cross-Consistency Verification (MANDATORY)**

   You MUST populate Section 22 with the results of the following checks:

   * Re-scan schema file(s) and confirm every model is documented in Section 10.
   * Re-scan all route directories and confirm each route group is represented in Architecture and Product Flows.
   * Re-scan `/docs` recursively and confirm every Markdown file is either:

     * Individually summarized, OR
     * Explicitly marked as irrelevant with justification.
   * Cross-check environment variables found in code (`process.env.*`) against the Environment Variables table; ensure none are undocumented.
   * Cross-check port numbers, base URLs, and proxy settings for mismatches.
   * Confirm all required sections (1–22) are present and non-empty.
   * If any inconsistency is found, resolve it before finalizing the document.

Now do the work and output the complete contents of `MASTER_CONTEXT.md`.

---

# Self-Critique (Preset)

## Clarity

* The prompt is explicit about the role (Staff Engineer + Technical Writer), the deliverable (`MASTER_CONTEXT.md`), and the exact required section order.
* It defines strict source-of-truth rules to prevent guessing.
* It clearly separates instructions, output requirements, and verification steps.

## Completeness

* Covers purpose, architecture, stack, repo map, local run, deployment, data model, flows, conventions, testing, risks, and Git intent.
* Includes a dedicated “Codex Operating Rules” section to reduce unsafe edits.
* Explicitly requires Deterministic Cross-Consistency Verification as a structural output section (Section 22).

## Hallucination / Assumption Control

* Strong guardrail: mark unknowns as `UNKNOWN` and list exact files checked.
* Forces the agent to cite real file paths.
* Requires cross-checking environment variables against actual `process.env.*` usage.
* Requires reconciliation between routes, schema, docs, and product flows.

## Deterministic Rigor Validation

* Section 22 is structurally required and must contain verification **results**, not instructions.
* Cross-consistency checks must be visible in output (no silent validation steps).
* Route groups, schema models, environment variables, and documentation must be reconciled before finalization.
* All required sections (1–22) must be present and non-empty before completion.

## Bias / Overreach Check

* Avoids opinionated redesign; documents what exists.
* Optimizes for operational usefulness rather than marketing language.
* Treats the repository as the single source of truth.

## Next-Step Improvements

* If the repo is very large, optionally limit deep dives to the top N high-impact paths while linking to detailed sections.
* For monorepos, require per-app segmentation with clearly separated entrypoints and environment variables.
* If security is critical, expand auth flow mapping and permission boundary documentation.
* Optionally add a “High-Risk Change Checklist” subsection for production-heavy systems.
