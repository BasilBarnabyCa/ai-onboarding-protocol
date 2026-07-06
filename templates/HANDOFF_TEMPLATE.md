# HANDOFF_TEMPLATE.md

Use this template to generate a rebuild handoff document after brownfield onboarding (see `/ai-onboarding/docs/protocols/POST_ONBOARDING_MIGRATION_PLAYBOOK.md`, Phase D).

How to use:
0. **Stack first.** Before filling ANY section, get the user's target stack: ask them to paste/describe their standard stack and any per-project deviations (the §2 ASK questions). Do not start generating the handoff from assumptions about the stack — the stack answers drive §2, §3, §9, §10, and §14 content.
1. Auto-fill every section you can from `/ai-onboarding/output/MASTER_CONTEXT.md` and the legacy repo first.
2. Ask the user ONLY the questions marked `ASK:` whose answers you cannot derive from evidence. Batch them sensibly; recommend defaults.
3. Replace all `[placeholders]`; delete the `ASK:`/`FILL:` guidance lines from the final document.
4. The finished file must be fully self-contained — the new project's AI must need nothing from the legacy repo to start.
5. Hard rules: no secrets, no credentials, no real personal data, no internal IPs. Mark inferences `ASSUMPTION:` and gaps `UNKNOWN`.
6. Save to `/ai-onboarding/output/NEW_PROJECT_HANDOFF.md`; the user carries it to the new repo as `docs/HANDOFF.md`.
7. **Companion documents (generate alongside the handoff — strongly recommended for unattended runs).** The handoff is the charter; these carry the implementation-level detail so the new AI almost never needs the legacy repo:
   - `LEGACY_DETAIL_APPENDIX.md` → new repo `docs/`. Contents: full endpoint inventory (every route: method, path, purpose, grouped by trust boundary); consolidated final DB schema (ALL migrations applied in order — every column, type, nullability, default, renames flagged) + FK list + data-quirk hazards for the migration script; ORM lifecycle-hook/observer inventory (what each actually does — often less scary than feared); external file-format contracts byte-level (import/export column mappings, transformations, skip rules, KNOWN BUGS flagged fix-vs-preserve); dependency intent map (legacy package → intent → modern alternative; drop obsolete intents); SPA navigation trees per role + page inventory.
   - `UX_BRAND_SPEC.md` → new repo `docs/`. Contents: logo/favicon/font asset filenames (user copies the files; AI references by name, placeholder if missing); full color palette as design tokens (semantic + grayscale + status badges + special-purpose) mapped to the new styling system; typography (family, weights actually used, scale); application shell diagram (topbar/sidenav/footer specifics); full sidebar nav trees per app/role; page archetypes (dashboard/list/detail/form/hub/auth — standard anatomy of each); **exact table columns per view page, in order** (so the new UI shows the same data); email/PDF/report branding.
   Extract both via parallel read-only subagents over the legacy repo (routes, migrations, hooks, importers, sass/css variables, layout partials, every list component's thead).

**This template is PROJECT-AGNOSTIC.** Where it shows concrete technologies, folder layouts, or layering chains (Express, Prisma, Vue SPAs, `routes → controllers → services → repositories`), these are ILLUSTRATIVE EXAMPLES from the reference implementation — not mandates. The user's target-stack answers (§2 ASK) are the source of truth: derive layout, layering, naming, and testing tools from THEIR stack, and adapt or drop any section content that doesn't apply (e.g. no SPAs, a different architecture style, no relational DB). Keep the SECTION STRUCTURE (0–14) intact for every project; vary the content freely.

Completed example: a filled handoff is produced at `/ai-onboarding/output/NEW_PROJECT_HANDOFF.md` when the migration playbook runs (generated per project; not tracked in this repo).

---

# [PROJECT NAME] — Rebuild Handoff & Ingestion Document

**Purpose:** This document is the complete project charter and domain-knowledge transfer for rebuilding [system name] on a new stack. It was produced from an evidence-based audit of the legacy codebase (`[legacy repo name]`, [legacy stack]) on [date]. The legacy repo is now **frozen** — reference only, no further work.

**Instruction to the ingesting AI:** Treat this document as the authoritative domain specification and project charter. The build is greenfield; the legacy system is the behavioral reference. Where this document marks something `UNKNOWN` or `ASSUMPTION`, ask the user rather than inventing an answer.

---

## 0. First-Session Kickoff (do this in order when the user says to start)

1. **Ingest fully before acting.** Read this entire document. Do not scaffold, install, or generate anything until you have.
2. **Play back your understanding.** Give the user a short summary (5–10 lines) of what you're building, the stack, and the first milestone — so misreadings surface before any code exists.
3. **Confirm only what's needed now.** From §12 (Open Questions), ask at most the [N] that block milestone 1: [list them]. Defer the rest until their module comes up. Do NOT re-ask anything in §11 (Decisions Already Made).
4. **Create the project memory file** (`CLAUDE.md` or equivalent) at the repo root, distilled from this document: stack rules, security bar (§8), build order (§9), and the §11 decisions table. Keep it short — link back to this file for detail.
5. **Keep this file in the repo** at `docs/HANDOFF.md` as the durable charter; reference it, don't duplicate it.
6. **Scaffold milestone 1** (§9 step 1): [one-line scaffold scope].
7. **Stop and show the user the scaffold** before starting milestone 2. From then on, work milestone by milestone per §9, getting a nod between milestones. (If the user activates Unattended Mode, §14 replaces these gates.)
8. **Standing rules for every session:** [language policy]; never skip a layer; every endpoint gets [validation] and RBAC checks; every mutation of [sensitive entities] writes to the audit log; PII never in logs or seed data; before implementing each service, request the legacy [hooks/observers] inventory for its models (§7).

---

## 1. What This System Is

FILL: from MASTER_CONTEXT "What This Repo Does" + the user's project brief. Plain language, 1 short paragraph.

**Core nouns (legacy → meaning):**
- **[LegacyTerm]** = [what it actually means in the domain]
- ...

ASK (only if unclear from evidence): "In one or two sentences each, what do [ambiguous legacy terms] actually mean to the business?"

## 2. Target Stack (decided — mirror the user's standard stack)

ASK: "Paste or describe your standard target stack (backend runtime/framework, language policy, ORM, database, validation, auth day-one vs planned, frontend framework/tooling, repo shape, cloud/hosting, security bar)."
ASK: "Any deviations from that standard for THIS project (e.g. keep the legacy database engine)? Deviations get recorded so the new AI never 'corrects' them."

- **Backend:** [runtime + framework + language policy]
- **Database:** [engine + ORM; local dev setup; role of the legacy DB as migration source]
- **Validation:** [library + policy, e.g. reject unknown properties]
- **Testing:** [backend framework — unit + integration via real HTTP against a test DB] / [frontend framework]; both wired into root scripts and CI
- **Auth (day one):** [mechanism]; [planned future identity provider] — design for swap-in without rework
- **Frontends:** [framework/tooling; one app per trust boundary]
- **Architecture:** [monorepo/polyrepo; orchestration; deployment boundaries; trust boundaries never merged]
- **Backend architecture & layering:** FILL from the user's standard stack — name the pattern (MVC + service layer, hexagonal, etc.), the exact layer chain, and the no-layer-skipping rule. Example (Express + ORM): `routes → controllers → services → repositories (ORM) → [DB]`, with middleware for [auth, RBAC, rate limit, versioning, errors]
- **Architecture naming/layout mapping (binding once filled):** FILL — spell out how the chosen pattern maps to actual folders so the new AI cannot drift into mixed conventions. Use the idioms of the TARGET framework, not the legacy one. Example (Express MVC): Model = [ORM schema] + `src/repositories/` (repository pattern; no `models/` class folder unless the ORM genuinely has model classes); View = the frontend apps, API returns JSON only; Controller = `src/controllers/` (thin — business logic in `src/services/`); layer folders flat under `server/src/` with no wrapper folders borrowed from other ecosystems
- **Cloud (decided):** [hosting target + key services: WAF/CDN, secrets manager, blob storage, telemetry with PII scrubbing]

## 3. Repo Layout

FILL: concrete tree showing every deployment boundary and the layer folders, derived from the user's stack (§2) and the legacy trust boundaries (§6). The tree below is an EXAMPLE shape (monorepo, one API + SPAs) — replace wholesale if the target architecture differs.

```
[new-repo]/
├── package.json
├── server/
│   ├── [orm-schema-dir]/
│   └── src/
│       ├── routes/ ├── controllers/ ├── services/ ├── repositories/
│       ├── middleware/ ├── validation/ └── jobs/
├── [frontend-app-1]/
└── [frontend-app-2]/
```

Note likely FUTURE boundaries (e.g. external-party portal) so versioning/auth are designed for them.

## 4. Domain Model (port to the new schema)

FILL: from MASTER_CONTEXT "Data and Domain Model" + legacy migrations. Group entities by area. For each: key fields, relationships, sensitivity flags (e.g. fields needing field-level encryption).
FILL: explicitly mark dead/legacy models NOT to port, and which surviving design replaces them.

ASK (if legacy had ambiguous/duplicate subsystems): "Legacy has both [X] and [Y] — which is the surviving design?"

## 5. Key Product Flows (behavioral spec)

FILL: from MASTER_CONTEXT "Key Product Flows". Number each flow; write as behavior, not implementation. For each flow note:
- external contracts that must be preserved exactly (file formats, API shapes)
- known legacy flaws the rebuild must FIX (state them as requirements, e.g. per-item failure isolation in batch jobs)
- scheduled/background behavior with times and timezones

## 6. API Surface (shape to mirror)

FILL: from legacy route files — route groups, trust split, approximate endpoint count per group. State: authorization enforced server-side, deny-by-default; any client-side role checks are cosmetic only.

## 7. Critical Port Hazards

FILL: legacy framework magic with no equivalent in the target stack. Always check for:
- ORM lifecycle events/observers/hooks → must become explicit service-layer logic (count them; name the legacy registration point)
- Implicit framework validation → explicit schemas
- Framework schedulers/queues → explicit timer jobs with per-item failure isolation
- External file/API format contracts → preserve byte-for-byte, test heavily
- Soft deletes, global scopes, cascades, middleware side effects

State the required action: inventory before implementing each service; the user can provide the legacy repo when needed.

## 8. Security Requirements ([bar, e.g. government-grade / OWASP ASVS L2+])

ASK: "What security bar does this system need (regulated data? government-grade? standard)?"
FILL: protected assets first (what PII/financial/regulated data exists). Then concrete controls per layer:

- **Identity:** [token design, hashing, lockout, forced reset, MFA-readiness, IdP swap-in path]
- **Authorization:** deny-by-default RBAC middleware; service-level checks for high-impact operations
- **Input/output:** [validation policy], parameterized queries, security headers, strict CORS per app, rate limiting
- **Data:** TLS; encryption at rest; field-level encryption for [most-sensitive fields]; PII never in logs/errors/telemetry; soft deletes + retention policy
- **Audit:** append-only audit log (actor, action, entity, before/after, timestamp, IP) for every mutation of [sensitive entities]
- **Secrets:** [secrets manager] in deployed envs; `.env` local only, never committed; no secrets/PII in seeds
- **Infra:** [WAF/CDN], dependency scanning in CI, least-privilege DB credentials
- **Process:** no destructive scripts touching real data; schema changes only via reviewed migrations with rollback notes

## 9. Build Order (approved by user)

ASK: "Approve or adjust the proposed build order." (Recommend: scaffold → full DB schema → auth/RBAC/middleware spine → services in dependency order → frontends per module → data migration + cutover.)

1. [milestone 1: scaffold — root orchestration, server skeleton + middleware spine, frontend apps, lint/format, CI]
2. [milestone 2: full schema + reference-data seeds]
3. [milestone 3: auth/RBAC/middleware spine]
4. [milestone 4..N: services in dependency order]
5. [frontends per module]
6. [data migration + cutover — see §10]

Testing expectation: [state legacy coverage honestly]. Per module, three layers:
- **Unit ([framework]):** service logic in isolation — [the domain math that matters most]
- **Integration ([framework + HTTP client] + test [DB]):** every route through the full middleware spine down to the database; test DB provisioned/reset via migrations; never points at a real database; [highest-risk pipeline] gets fixture-based coverage
- **Component ([frontend framework]):** stores, role-gated rendering, critical forms

A milestone is not complete until its unit AND integration suites pass.

## 10. Data Migration & Cutover

- Legacy DB is [engine/host] → target is [engine]: [same-engine reshaping | cross-engine ETL]
- **The migration script lives in THE NEW project** (e.g. `server/scripts/migration/` or the target stack's equivalent), never in the frozen legacy repo — it depends on the target schema, is rehearsed repeatedly, and needs its own tests. It needs the legacy *database*, not the legacy *code*
- Script design: **read-only** connection to the legacy DB; extract → transform ([known data quirks to handle]) → load; **idempotent and repeatable**; produces a migration report per run
- `.env`: `DATABASE_URL` (target) + `LEGACY_DATABASE_URL` (read-only source)
- **Reconciliation gates (script asserts automatically, fails loudly):** row counts per entity; [domain-critical sums to the cent]; [schedules/relationships preserved]
- Validation reference: the running legacy app is the only behavioral spec — side-by-side verification per module
- [Big-bang | per-module] cutover after at least one full rehearsal on a production snapshot

## 11. Decisions Already Made (do not re-litigate)

ASK (lock-in batch, one time): new repo location/name & who creates it; hosting; auth day one; frontend apps at launch; build order approval; cutover style; database & migration approach.

| Decision | Value |
|---|---|
| Legacy repo | Frozen; reference only |
| Migration style | [value] |
| Database | [value — note any superseded earlier decision with date] |
| Migration script home | The NEW repo |
| Language | [value] |
| Hosting | [value] |
| Auth day one | [value] |
| SPAs at launch | [value] |
| Build order | As §9 |
| Testing | [backend fw] (unit+integration) / [frontend fw] |
| Security bar | [value] |

## 12. Open Questions (ask the user when relevant)

FILL: everything genuinely unresolved, each tagged with WHEN to ask (milestone-1-blocking vs defer-to-module). Typical: which roles survive; jurisdiction/compliance regime; mail/notification provider; external file format specs; schedule times/timezones; production data snapshot access.

## 13. Legacy Reference Pointers

FILL: exact legacy paths to consult for deeper detail — onboarding MASTER_CONTEXT, route files, ORM hooks/observers registration, external-contract parsers (imports/exports), scheduled commands, migrations.

## 14. Unattended Mode (activate when the user says "run unattended")

When activated, this section **overrides the milestone-by-milestone approval gates** in §0 step 7.

### Pre-flight (one batch, before any code)
1. The §12 questions that block any milestone
2. Initial `.env` values the AI cannot self-generate: [DB connection strings incl. legacy read-only], [provider credentials] (or permission to stub behind the same interface)
3. How far to run unattended (default: through milestone [N-1] — everything except data migration/cutover)
4. **Harness permissions:** unattended mode also requires the AI runner's tool-approval prompts to be configured, or the run stalls on yes/no prompts for git/npm/cd regardless of these rules. As part of milestone-1 scaffold, create the runner's project permission config (e.g. `.claude/settings.json` for Claude Code) allowing routine dev commands (package manager, git add/commit/status/diff, file ops, ORM CLI) while DENYING: reading `.env`, `git push`, and recursive deletes. Confirm the user is comfortable with the allowlist before the long run.
5. **Command-shape rules (add to the project memory file — these defeat prompts that allowlists cannot):**
   - Never run `cd <dir> && git ...` compound commands (flagged as untrusted-hook risk every time) — run git plainly from the repo root; reach monorepo subpackages with `npm --prefix <app>` or root workspace scripts instead of `cd`
   - Never prefix commands with inline env assignments (`VAR=x cmd`) — permission rules match the command's start, so the allowlist never matches, AND credentials leak into prompts/transcripts/logs. Load env from files instead: per-environment env files (`.env`, `.env.test` — both gitignored, variables mirrored in `.env.example`) wired through package scripts (e.g. dotenv-cli: `"db:migrate:test": "dotenv -e .env.test -- npx prisma migrate deploy"`), then run the script
   - Never use shell loops, variable expansion (`$var`), or `sed`/`awk`/`echo` pipelines to create or transform files — variable-expanded commands are flagged (`simple_expansion`) and cannot be allowlisted. Use the runner's file tools (Read/Write/Edit) for all file creation and transformation; reserve shell for running programs (package manager, git, node, CLIs)

### Harness permission config — reference example (Claude Code: `.claude/settings.json` at new repo root)

Create this during milestone 1 (adapt commands to the target stack; keep the deny list intact):

```json
{
  "permissions": {
    "allow": [
      "Read", "Edit", "Write", "Glob", "Grep",
      "Bash(npm:*)", "Bash(npx:*)", "Bash(node:*)",
      "Bash(git add:*)", "Bash(git commit:*)", "Bash(git status:*)",
      "Bash(git diff:*)", "Bash(git log:*)", "Bash(git branch:*)", "Bash(git checkout:*)",
      "Bash(mkdir:*)", "Bash(ls:*)", "Bash(cd:*)", "Bash(cat:*)",
      "Bash(cp:*)", "Bash(mv:*)", "Bash(touch:*)"
    ],
    "deny": [
      "Read(./.env)", "Read(.env)",
      "Bash(git push:*)",
      "Bash(rm -rf:*)"
    ]
  }
}
```

Add the target stack's CLI tools to `allow` as needed (e.g. `Bash(npx prisma:*)`, test runners). `git push` and `rm -rf` denies are non-negotiable.

**The `.env` read-deny depends on mode.** In attended mode (human owns secrets), keep it. In unattended mode, REMOVE it: the §14 env protocol has the user hand local credentials to the AI at pre-flight and expects the AI to maintain env files — but Edit requires Read, so a read-deny forces the AI into flagged `sed`/heredoc workarounds it cannot use. The actual non-negotiable is **env files are never committed**: enforce via `.gitignore` (AI verifies with `git check-ignore` at milestone gates) and the no-secrets-in-commits standing rule. Production credentials must never be on the dev machine in any case.

### Autonomy rules
- Complete entire milestones without pausing; **automated gates replace human nods**: lint clean, unit + integration suites passing, frontend suites passing, apps build, dependency audit reviewed
- Write tests as you build — they are the only spec-verification while unattended
- Maintain `PROGRESS.md` at the repo root (work done, decisions, gate status, deferred items)
- If blocked: record in `PROGRESS.md`, move to unblocked work, else stop with a clear ask. Never improvise around a blocker

### Environment variable protocol (.env stop points)
- `.env.example` is the contract — every variable appears there, commented, the moment it's introduced; `.env` never committed
- New variable needed → **self-generate if safe** (local keys/salts; mark LOCAL-ONLY in PROGRESS.md) → **stub if continuable** (same service interface, TODO logged) → **STOP and ask** for real credentials, third-party accounts, or anything with security consequences. Never invent, hard-code, or commit placeholder secrets

### Hard stops (always require the human, regardless of mode)
1. Schema review after milestone 2 — everything downstream compounds on it
2. Any new credential/secret per the protocol above
3. Anything touching real/legacy data: migration runs, rehearsals, reconciliation
4. Any deployment, cloud resource creation, or cutover action
5. Any deviation from a §11 decision that seems necessary — stop and explain, never silently deviate

---

— End of handoff. Ingest fully before scaffolding. —
