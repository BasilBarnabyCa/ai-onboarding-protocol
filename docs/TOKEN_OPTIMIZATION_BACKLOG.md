# Plan: Token-Optimization Improvements for ai-onboarding-protocol

## Context

A separate multi-day token-optimization audit produced 5 proposed improvements for this
repo. Each was evaluated against actual repo state (not assumed) via a full read of
`AGENT_RULES.md`, `docs/protocols/ARCHITECTURE_ALIGNMENT.md`,
`docs/protocols/POST_ONBOARDING_MIGRATION_PLAYBOOK.md`, `docs/LESSONS_LEARNED.md`,
`docs/generators/AI_ONBOARDING_MASTER_CONTEXT_GENERATOR.md`, `profiles/PROFILE_REGISTRY.md`,
and the hook/skill/`cmd:` implementation. Findings: 2 of 5 are confirmed real gaps with
clean fits into existing structure, 1 is a scope-down from what was proposed, 1 is doc-only,
and 1 needs no action yet. This plan implements them in the order that clears real gaps
first, cheapest first.

Nothing has been implemented yet. This plan produces markdown-only edits — no code, no
hooks, no automation — consistent with this repo's nature as a protocol/documentation
framework.

## Order and Rationale

1. **Model-tier routing (Phase D)** — clean gap, zero existing content to conflict with, cheapest.
2. **Context-budget check (Gate A/B)** — clean gap, moderate edit, reuses existing enforcement clause.
3. **Runner-permission fixes** — real value, but scoped down to editing the existing
   settings.json template rather than inventing a new PreToolUse hook mechanism (no hooks
   exist anywhere in this repo today; adding one would be a bigger, novel lift).
4. **Blast-radius open question** — doc-only, lowest risk, no urgency.
5. **Skill-description budget** — no action; confirmed not applicable (no skill packaging
   exists). Document the decision so it isn't re-litigated.

## Step 1: Model-tier routing for Phase D subagents

**Files:**
- `AGENT_RULES.md` — add a short subsection near the existing rules (no current
  haiku/sonnet/opus mention anywhere in repo) codifying tier-by-task-type, matching the
  tiering already settled in the user's global `RTK.md`/`CLAUDE.md` convention:
  - haiku: file-extraction / legacy-code-reading subagents
  - sonnet: cross-consistency checks, evidence-quality scoring
  - opus: Phase A disposition-table decisions (Maintain/Upgrade/Rebuild/Retire), Phase B
    target-stack architecture mapping
  - State explicitly: pass `model` on every subagent call, never omit (omitted defaults
    upward, not to haiku).
- `docs/protocols/POST_ONBOARDING_MIGRATION_PLAYBOOK.md` — in the Phase D section
  (lines 63-87, the 14-section handoff + companion-docs description), add a one-line
  pointer to the new `AGENT_RULES.md` tiering subsection so Phase D itself specifies tiers
  at the point of use, not just cross-referenced.
- `templates/HANDOFF_TEMPLATE.md` (line ~16, "Extract both via parallel read-only
  subagents...") — add tier annotation inline where the parallel-subagent instruction
  actually lives, since the playbook body itself doesn't contain the subagent instruction
  (it lives here and in `LESSONS_LEARNED.md`).

## Step 2: Context-budget check as part of Gate A/B

**Files:**
- `AGENT_RULES.md` (lines ~176-194, "Self-Critique and Drift Control (Mandatory)") — add
  a fifth check item alongside the existing scope/constraint/evidence/assumption checks:
  a context-budget check (e.g., threshold ~40% of window used → require compact/handoff
  artifact before continuing to next phase). Reuse the existing "no-collapsing-phases"
  enforcement language already governing scope drift — do not invent new enforcement
  mechanics.
- `docs/protocols/ARCHITECTURE_ALIGNMENT.md` (Phase 1, step "3.5) Run self-critique drift
  audit", lines ~170-189) — mirror the same addition here since this is where the
  step is actually defined in detail (AGENT_RULES.md's Gate A/B section references this
  check set but doesn't fully define it).
- `templates/DRIFT_CHECK_TEMPLATE.md` — add a context-budget row/field to the report
  template so Gate A/B output actually surfaces this check, matching how the other four
  checks are already represented.
- Call out relevance to the Legacy Migration Workflow (Phases A-G) explicitly, since long
  single-thread sessions are where this matters most — a short note in
  `docs/protocols/POST_ONBOARDING_MIGRATION_PLAYBOOK.md` is enough; no phase restructuring.

## Step 3: Bake permission-gotcha fixes into the shipped settings.json template

**Scope-down from the original proposal:** the original proposal asked for a "runner-permission
hook template" in the spirit of a `PreToolUse` rewrite hook. This repo has zero hooks
anywhere — introducing one would be a new mechanism, not a documentation fix, and is out of
proportion to a docs-focused framework. Instead: the three concrete, already-settled fixes
from `docs/LESSONS_LEARNED.md` (items #3 and #4) get baked directly into the existing
plain allow/deny permissions template that already ships to new projects.

**Files:**
- `templates/handoff-package-skeleton/claude/settings.json` — the template already copied
  into new projects at Phase F (`POST_ONBOARDING_MIGRATION_PLAYBOOK.md` line ~105). Extend
  its allow/deny lists to reflect the three settled fixes:
  - No bare `cd <dir> && git ...` pattern encouraged — template already allows plain git
    subcommands from repo root; add a short comment noting why (avoids "untrusted hooks" prompt).
  - Confirm no inline `VAR=x cmd` patterns are implied; note the dotenv-cli / env-file
    convention instead.
  - Confirm `Read(**/.env.production)` deny is present (it is) and stays mode-dependent per
    lesson #4 — add a comment cross-referencing `docs/LESSONS_LEARNED.md` items #3/#4 so the
    template doesn't drift from the documented rationale.
- `docs/protocols/POST_ONBOARDING_MIGRATION_PLAYBOOK.md` (Phase F, ~line 101-113) — add a
  one-line note that the shipped `settings.json` already encodes these fixes, so new
  migrations don't rediscover them.
- No new file, no hooks key, no PreToolUse mechanism.

## Step 4: Flag blast-radius tension as an open question

**Files:**
- `docs/protocols/ARCHITECTURE_ALIGNMENT.md` — this file currently has no "Open Question"
  heading anywhere; add a new short section (e.g., near the end, or wherever Phase-agnostic
  meta-notes belong) documenting the tension: blast-radius/dependency-graph tooling
  (e.g., code-review-graph) could reduce tokens for day-to-day doc drafting, but
  `docs/LESSONS_LEARNED.md` item #6 shows exhaustive reading caught two real data-corrupting
  bugs and correctly downgraded a feared risk ("26 observers"). Recommendation: do not
  blanket-adopt; consider scoped-only for Phase D doc drafting; keep Phase B's
  read-everything approach for port-hazard identification unchanged.
- Cross-reference from `docs/protocols/POST_ONBOARDING_MIGRATION_PLAYBOOK.md` Phase D
  section with a single line pointing to the new open-question note, so it's visible where
  Phase D is actually defined.

## Step 5: Document the skill-description-budget decision (no action)

**Files:**
- `docs/LESSONS_LEARNED.md` or a short note in `AGENT_RULES.md` — record: repo's `cmd:`
  triggers (`commands/commands.yaml` + regex match) are not Claude Code skills; no skill
  packaging exists; if `cmd:onboard`/`cmd:drift-audit`/etc. are ever packaged as installable
  skills, keep each description under ~200 chars (settled threshold from the audit — skill
  descriptions load into every message's menu, so cost scales with however many skills a
  given user/environment has installed, not a fixed number this repo controls). Not urgent
  today — this is a forward note, not a change to any current file's behavior.

## Step 0 (on approval): Save this plan into the repo

Copy this plan file into `docs/TOKEN_OPTIMIZATION_BACKLOG.md` in the repo so it's
referenceable alongside the other protocol docs, not just in the local plans directory.
Keep the Context/Order/Steps structure as-is; this becomes the durable backlog record for
future sessions to check off against.

## Verification

This is a documentation-only change set — no runtime to execute. Verification is by
review:
- Diff each edited file and confirm added content matches the existing section's tone,
  heading level, and cross-reference style (this repo is heavily cross-referenced between
  `AGENT_RULES.md`, the protocol docs, and templates — new content must link both ways
  where an existing analogous check already does, e.g. Gate A/B's existing four checks).
- Grep the repo after edits for "haiku", "sonnet", "opus", "context budget", "Open
  Question" to confirm each addition landed exactly once in its intended file (no
  duplication across files that cross-reference each other).
- Manually trace Phase D and Gate A/B sections end-to-end after edits to confirm an agent
  following the protocol linearly would encounter the new instructions at the right point
  (not just in a far-away file it may not read in sequence).
