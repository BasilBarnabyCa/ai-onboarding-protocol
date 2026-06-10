# Post-Onboarding Migration Playbook

**What this is:** A repeatable protocol for what happens AFTER `cmd:onboard` (Phase 1 alignment) completes on a legacy repository, when the decision is to migrate/rebuild it as a new project on a modern stack. Designed to be reused across all legacy projects.

**Prerequisite:** Phase 1 onboarding complete in the legacy repo — `MASTER_CONTEXT.md`, `AI_ONBOARDING_SUMMARY.md`, `DRIFT_CHECK_REPORT.md` (Go decision) all exist under `/ai-onboarding/output/`.

**Read first:** `/ai-onboarding/docs/LESSONS_LEARNED.md` — friction→fix log from the first full run; it prevents every known stall. Everything this playbook needs ships inside `/ai-onboarding/`: this playbook, `templates/HANDOFF_TEMPLATE.md`, `templates/handoff-package-skeleton/` (incl. claude runner config + command rules), and the lessons log — copying `ai-onboarding/` into a legacy repo is sufficient to run the whole workflow.

**End state:** A frozen legacy repo with committed audit artifacts, plus a single self-contained handoff document the new project's AI ingests to start the rebuild.

---

## Phase A — Disposition Decision

Normally entered via the non-blocking next-step question at the end of brownfield alignment (`ARCHITECTURE_ALIGNMENT.md` step 4.1: keep working here vs. migrate). If the user answered `migrate`, disposition is already decided — skip to Phase B. Otherwise, review the onboarding outputs with the user and decide what happens to this system:

| Disposition | Choose when |
|---|---|
| Maintain | Stack supported, risks acceptable, change volume low |
| Upgrade in place | Stack upgradable with reasonable effort, architecture worth keeping |
| **Rebuild (this playbook)** | Stack EOL, zero/low test coverage, architecture diverges from your standard stack, or strategic standardization |
| Retire | System no longer needed |

Inputs to the decision (all already in `MASTER_CONTEXT.md`): framework/runtime EOL status, test coverage, security posture, known sharp edges, deploy story, business criticality.

**Output:** explicit user statement of disposition. If "rebuild" → continue.

---

## Phase B — Target Definition

1. **Capture the target stack** from the user FIRST — before any handoff drafting begins. The user provides/pastes their standard stack (they mirror it across projects): backend runtime/framework, language policy (e.g. JS only / no TS), ORM, database, validation, auth (day-one vs planned), frontend framework/tooling, testing tools, repo shape (monorepo? deployment boundaries?), architecture pattern + layering, cloud/hosting, security bar. The stack answers — not template examples — drive all stack-dependent handoff content.
2. **Record permitted deviations** explicitly (e.g. "keep MySQL instead of PostgreSQL") so the new AI doesn't "correct" them later.
3. **Map old → new, component by component:** for each legacy subsystem (auth, RBAC, ORM, scheduled tasks, queues, mail, file import/export, PDF, storage, telemetry), name its replacement in the target stack.
4. **Identify port hazards** — legacy framework magic with no equivalent in the target stack. These are the silent-failure risks of any rewrite. Common ones:
   - ORM lifecycle events/observers/hooks → must become explicit service-layer logic
   - Implicit validation (framework form requests) → explicit JSON schemas
   - Framework schedulers/queues → explicit timer jobs with per-item failure isolation
   - File format contracts with external parties (import/export sheets, APIs) → must be preserved byte-for-byte and tested heavily
   - Soft deletes, global scopes, cascade behaviors, middleware side effects
5. **Identify trust boundaries** in the legacy app (route groups, role-gated areas) — these become the independent frontend apps / deployment boundaries in the new project.

**Output:** stack spec + component map + named port hazards (these all go into the handoff document).

---

## Phase C — Decision Lock-In

Ask the user and record answers (one batch of questions; recommend defaults). Minimum set:

1. New repo location/name — who creates it?
2. Hosting target (full cloud mirror vs current host vs hosting-agnostic)
3. Auth on day one (in-app JWT vs identity provider from the start)
4. Number of frontend apps at launch (from trust boundaries) + future ones
5. Build order (recommend: scaffold → full DB schema → auth/RBAC/middleware spine → services in dependency order → frontends per module)
6. Cutover style: big-bang with rehearsals vs per-module strangler
7. Data migration expectations (same DB engine = reshaping; different engine = full ETL; reconciliation gates either way)

**Rule:** once answered, these are *decisions* — they go in a "do not re-litigate" table in the handoff.

---

## Phase D — Generate the Handoff Document

Create one **fully self-contained** markdown file (the new AI must need nothing from the legacy repo to start). **Use `/ai-onboarding/templates/HANDOFF_TEMPLATE.md`** — it mirrors this structure with per-section fill guidance and the `ASK:` questions. Required sections, in order:

| # | Section | Content |
|---|---|---|
| — | Purpose + ingestion instruction | What the doc is; "treat as authoritative; ask on UNKNOWN/ASSUMPTION, never invent" |
| 0 | **First-Session Kickoff** | Ordered steps for the new AI: ingest fully → play back understanding → ask only milestone-1-blocking questions → create project memory file (CLAUDE.md) distilled from this doc → keep this doc in repo (`docs/HANDOFF.md`) → scaffold milestone 1 → STOP and show user → standing per-session rules |
| 1 | What the system is | Domain in plain language; glossary of core nouns (legacy term → meaning) |
| 2 | Target stack | From Phase B, including permitted deviations |
| 3 | Repo layout | Concrete tree with deployment boundaries |
| 4 | Domain model | Every entity with key fields and relationships; mark dead/legacy models NOT to port |
| 5 | Product flows | Each workflow as a behavioral spec, including fixes to known legacy flaws |
| 6 | API surface | Route groups/trust split to mirror; server-side enforcement rules |
| 7 | Port hazards | From Phase B §4 — loud and specific, with required actions |
| 8 | Security requirements | Concrete controls per layer (identity, authz, input/output, data, audit, secrets, infra, process); name the benchmark (e.g. OWASP ASVS level) |
| 9 | Build order | From Phase C, as approved milestones; testing expectations |
| 10 | Data migration & cutover | Approach + **reconciliation gates** (row counts, financial sums to the cent, etc.) |
| 11 | Decisions already made | Table — "do not re-litigate" |
| 12 | Open questions | What to ask the user, and *when* (defer non-blocking ones to their module) |
| 13 | Legacy reference pointers | Exact legacy paths to consult when deeper detail is needed |

**Hard rules:** no secrets, no credentials, no real personal data, no internal IPs. Mark every inference `ASSUMPTION` and every gap `UNKNOWN`.

**Companion documents (same phase — see template how-to-use step 7):** generate `LEGACY_DETAIL_APPENDIX.md` (endpoints, consolidated schema, hook inventory, file-format contracts, dependency intent map, nav/pages) and `UX_BRAND_SPEC.md` (logo/font asset names, color tokens, typography, shell, nav trees, page archetypes, exact table columns per view). These make unattended runs self-sufficient — without them the new AI stops to request legacy repo access at the schema, import, and UI milestones.

---

## Phase E — Freeze the Legacy Repo & Assemble the Package

0. **Assemble `handoff-package/` at the legacy repo root** from `/ai-onboarding/templates/handoff-package-skeleton/` — PROJECT-SPECIFIC contents only (the framework stays in `ai-onboarding/`): `docs/` (the three generated documents), `claude/` (adapted settings.json + CLAUDE_RULES.md), `assets/` (brand images + fonts copied from the legacy tree), and a filled README (from `PACKAGE_README_TEMPLATE.md`) with destinations and kickoff prompts. One folder is everything the user carries to the new project.
1. Commit the `ai-onboarding/` framework + all generated artifacts + the handoff package. Note: the framework `.gitignore` excludes `output/*` — **force-add** (`git add -f`) the artifacts, since preserving the audit is the point. Do not push unless the user says to.
2. Declare the repo frozen: reference-only, no further feature work.
3. Record the freeze + migration decision in the assistant's persistent project memory (old repo = reference only; pointer to new project).
4. Optional: banner at the top of the legacy `README.md` stating the repo is frozen and superseded (requires user approval since the repo is now frozen).

---

## Phase F — In the New Project

1. Copy the handoff document into the new repo as `docs/HANDOFF.md` (plus any detail appendix and the user's `COMMIT_CONVENTIONS.md` at root).
2. Tell the AI: *"Ingest docs/HANDOFF.md and start."* Section 0 of the handoff drives everything from there.
3. **For unattended runs, configure the harness before the long run** — otherwise it stalls on tool-approval prompts no matter what the handoff says: create the runner's project permission config (`.claude/settings.json` — example in `HANDOFF_TEMPLATE.md` §14) allowing routine dev commands and denying `.env` reads, `git push`, and recursive deletes; and add the command-shape rules to the project memory file (no `cd <dir> && git ...`; use `npm --prefix` for subpackages).
4. Optionally copy the `ai-onboarding/` framework and run `cmd:onboard` as **greenfield**, using the handoff as the project brief input.
5. Work milestone-by-milestone with a user checkpoint between milestones (encoded in §0/§9 of the handoff).
6. Validation principle: **the running legacy app is the only behavioral spec** (legacy repos typically have no tests) — verify side-by-side per module.
7. Cutover only after migration rehearsal passes all reconciliation gates.

---

## Phase G — Retrospective (keeps the framework improving)

`/ai-onboarding/docs/LESSONS_LEARNED.md` is a living log, not a static doc. Update it at two moments:

1. **During the run, as friction occurs** — whenever the user has to correct the process (a stall, a prompt that shouldn't have happened, a missing artifact, a wrong assumption), append a lesson immediately in the friction→fix format: what stalled, why, and what rule/template change prevents it. If the fix is a template or playbook change, make that change in the same commit.
2. **At the end of the migration** (post-cutover or when the user closes the project) — a short retrospective pass: anything learned that wasn't captured live.

Then **sync upstream**: copy the updated `LESSONS_LEARNED.md` (and any changed templates/playbook) to the canonical framework repo (`ai-onboarding-protocol`), so the next legacy project starts with everything every prior run learned. A lesson that only lives in one project's copy is a lesson lost.

- [ ] Phase 1 onboarding complete, drift not `major`, Go decision
- [ ] A. Disposition decided by user (rebuild)
- [ ] B. Target stack captured + deviations recorded
- [ ] B. Old→new component map done
- [ ] B. Port hazards named (ORM events, schedulers, external file contracts, …)
- [ ] B. Trust boundaries identified → frontend app list
- [ ] C. Lock-in questions answered (repo, hosting, auth, apps, build order, cutover, data migration)
- [ ] D. Handoff document generated — self-contained, all 14 sections, no secrets/PII
- [ ] D. Companion docs generated: LEGACY_DETAIL_APPENDIX + UX_BRAND_SPEC (incl. table columns per view)
- [ ] E. handoff-package/ assembled at repo root (docs + claude config + brand assets + filled README; framework stays in ai-onboarding/)
- [ ] E. Legacy repo committed (artifacts force-added) and frozen; memory updated
- [ ] F. Handoff copied to new repo as `docs/HANDOFF.md`; new AI ingests and scaffolds milestone 1
- [ ] F. Per-module side-by-side validation against the running legacy app
- [ ] F. Migration rehearsal passes reconciliation gates → cutover
- [ ] G. LESSONS_LEARNED.md updated (live friction entries + end-of-run retrospective) and synced to the canonical framework repo

---

**Reference implementation of this playbook:** the SDMC BMS migration (this repo) — see `/ai-onboarding/output/NEW_PROJECT_HANDOFF.md` for a completed handoff example.
