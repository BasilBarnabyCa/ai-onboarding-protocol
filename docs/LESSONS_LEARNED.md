# Lessons Learned — Legacy Migration Exercise (Laravel 7/Vue 2 → Node 20/Express/Prisma/Vue 3, 2026-06-10)

Friction encountered during the first full run of the migration workflow, and the fix now baked into the framework. Read this before running the playbook on the next legacy project.

## 1. The handoff alone is not enough for unattended runs
**Friction:** the new AI stopped at the schema, import, and UI milestones to request legacy repo access — the handoff was a charter, not an implementation spec.
**Fix (baked in):** always generate the two companion docs with the handoff (template how-to-use step 7): `LEGACY_DETAIL_APPENDIX.md` (endpoints, consolidated schema, hook inventory, file contracts, dependency intent map, nav) and `UX_BRAND_SPEC.md` (brand tokens, fonts, shell, nav trees, page archetypes, **table columns per view**). Extract via parallel read-only subagents.

## 2. "Unattended" requires harness config, not just document rules
**Friction:** the run stalled every few minutes on tool-approval prompts (git, npm, cd) despite §14 unattended rules — those govern the AI, not the harness.
**Fix (baked in):** `.claude/settings.json` allowlist + deny list ships in the package (skeleton `claude/settings.json`); §14 pre-flight includes confirming it with the user.

## 3. Some permission prompts CANNOT be allowlisted — only avoided by command shape
Hardcoded security heuristics fire regardless of settings. Each was hit live:
- `cd <dir> && git ...` → "untrusted hooks" prompt. Rule: git runs plainly from repo root; `npm --prefix` for subpackages.
- `VAR=x cmd` inline env prefix → allowlist matches the command START, so it never matches; also leaks credentials into logs. Rule: env files (+ dotenv-cli package scripts).
- Shell loops / `$var` expansion / heredocs / `sed -i` → `simple_expansion` & sed-write prompts. Rule: ALL file creation/transformation via Read/Write/Edit tools; shell only runs programs.
**Fix (baked in):** the command rules block (`CLAUDE_RULES.md` in the package skeleton) is merged into the new project's CLAUDE.md at kickoff.

## 4. Deny rules can force the AI into worse behavior
**Friction:** denying `Read(.env)` made Edit impossible (Edit requires Read), so the AI fell back to flagged blind `sed` on `.env`.
**Fix (baked in):** env read-deny is mode-dependent — attended keeps it; unattended removes it for local env files (the user hands over local creds at pre-flight anyway) and keeps only `Read(**/.env.production)`. The real invariant — env files never committed — is enforced via .gitignore + gate checks.

## 5. Decisions drift; record supersessions explicitly
**Friction:** the database decision flipped (keep MySQL → full-mirror PostgreSQL) mid-process.
**Fix (baked in):** §11 decisions table records superseded decisions with dates so the new AI never resurrects an old one.

## 6. Deep extraction pays for itself — and surprises are usually pleasant
The feared "26 observers" port hazard turned out to be one trivial pattern (creator-stamping). The import parsers contained two real data-corrupting bugs (zipcode→city overwrite; wrong address-line mapping) that the rebuild must fix and the migration script must compensate for. Neither would have surfaced without reading every file. **Rule: inventory hazards by reading the actual code, not by labeling them risky.**

## 7. Dependencies transfer as INTENT, not as packages
**Fix (baked in):** the appendix's dependency map is three-column: legacy package → intent → suggested modern alternative; obsolete intents are dropped, not replaced.

## 8. Centralize the deliverables
**Friction:** take-along files accumulated piecemeal (handoff, then prompts, then appendix, then UX spec, then assets...).
**Fix (baked in):** Playbook Phase E assembles a `handoff-package/` at the legacy repo root: agnostic `templates/` (this framework's reusable pieces) + `output/` (the project-specific docs, runner config, brand assets, filled README with kickoff prompts). One folder to carry.

## 9. Misc operational
- The framework `.gitignore` excludes `output/*` — force-add (`git add -f`) generated artifacts when the user wants them in history.
- Legacy repo read access for the new AI is safe post-freeze (read-only, never the legacy `.env`); a standing grant beats per-command prompts.
- Intentional code duplication across trust-boundary SPAs is fine — but logged in PROGRESS.md so divergence is a known cost.
- Brand/font asset files go IN the package (`output/assets/`) — don't make the user hunt for them in the legacy tree.
