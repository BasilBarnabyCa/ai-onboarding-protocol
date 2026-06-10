# [PROJECT NAME] — Handoff Package

Everything the new project needs, in one folder. Copy the contents into the new repo as mapped below, then use the kickoff prompt.

## What goes where

| This package | New repo destination | Purpose |
|---|---|---|
| `docs/HANDOFF.md` | `docs/HANDOFF.md` | The charter: decisions, architecture, security bar, build order, unattended mode (§14) |
| `docs/LEGACY_DETAIL_APPENDIX.md` | `docs/LEGACY_DETAIL_APPENDIX.md` | Implementation spec: endpoints, consolidated schema, hook inventory, file-format contracts, dependency intent map, nav/pages |
| `docs/UX_BRAND_SPEC.md` | `docs/UX_BRAND_SPEC.md` | Visual contract: logos, color tokens, fonts, shell, nav trees, page archetypes, table columns per view |
| `claude/settings.json` | `.claude/settings.json` | Permission allowlist + denies — kills routine approval prompts |
| `claude/CLAUDE_RULES.md` | merge into `CLAUDE.md` | Command-shape rules that defeat prompts allowlists can't |
| `assets/*` | per UX spec §1/§3 | brand images and fonts |
| (your own) `COMMIT_CONVENTIONS.md` | new repo root | Required by HANDOFF.md §0 — the AI reads it before its first commit |

## Kickoff prompts

Attended (milestone-by-milestone):

> Ingest docs/HANDOFF.md, docs/LEGACY_DETAIL_APPENDIX.md, and docs/UX_BRAND_SPEC.md fully, then start.

Unattended:

> Ingest docs/HANDOFF.md, docs/LEGACY_DETAIL_APPENDIX.md, and docs/UX_BRAND_SPEC.md fully, then run unattended per HANDOFF §14.

## Notes

- The appendix and UX spec exist so the AI rarely needs the legacy repo. If it still asks, granting READ-ONLY access to the legacy repo at [LEGACY_REPO_PATH] is safe (it's frozen); tell it: never read the legacy `.env`, never write there.
- Hard stops survive even unattended mode: schema review after milestone 2, new credentials, anything touching real data, deployment/cutover, deviations from locked decisions.
- Process for repeating this on other projects: `ai-onboarding/docs/protocols/POST_ONBOARDING_MIGRATION_PLAYBOOK.md` in the legacy repo.
