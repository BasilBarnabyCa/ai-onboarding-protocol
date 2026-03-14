# Changelog

All notable changes to this repository are documented in this file.

This project currently tracks changes by date and merged pull requests (no tagged releases yet).

## 2026-03-14

### Changed
- Standardized and hardened Step 0 onboarding behavior across docs and command specs.
- Enforced canonical Step 0 wording/questions for consistent first-run behavior.
- Enforced asking platform and model every run (auto-detect may prefill, but no skip).
- Simplified the model question wording to be user-friendly (`LLM model` + `yes/correction` pattern).

### Added
- Final non-blocking pre-generation checkpoint:
  - "Any final context to include before I generate artifacts? Reply `none` to continue, or add up to 3 bullets."

### Related PRs
- [#7](https://github.com/BasilBarnabyCa/ai-onboarding-protocol/pull/7)
- [#8](https://github.com/BasilBarnabyCa/ai-onboarding-protocol/pull/8)
- [#9](https://github.com/BasilBarnabyCa/ai-onboarding-protocol/pull/9)
- [#10](https://github.com/BasilBarnabyCa/ai-onboarding-protocol/pull/10)
- [#11](https://github.com/BasilBarnabyCa/ai-onboarding-protocol/pull/11)

## 2026-03-13

### Changed
- Enforced sequential Step 0 + intake gating and reduced ambiguity in onboarding prompts.
- Simplified command flow and strengthened greenfield onboarding depth requirements.
- Improved README guidance and strict command-mode behavior.
- Added/clarified periodic drift-audit cadence and phase transition expectations.

### Related PRs
- [#3](https://github.com/BasilBarnabyCa/ai-onboarding-protocol/pull/3)
- [#4](https://github.com/BasilBarnabyCa/ai-onboarding-protocol/pull/4)
- [#5](https://github.com/BasilBarnabyCa/ai-onboarding-protocol/pull/5)
- [#6](https://github.com/BasilBarnabyCa/ai-onboarding-protocol/pull/6)

## 2026-03-12

### Added
- Initial repository protocol foundation:
  - `AGENT_RULES.md`
  - protocol docs under `docs/protocols/`
  - generator/template structure
  - command conventions and onboarding scaffolding
- Brownfield profile selection layer and Step 0 intake prompts.
- Profile overlays and output artifact conventions.

### Changed
- Reorganized documentation/templates into structured folders.
- Clarified README "where to start" flow and strict command guidance.
- Added `.gitignore` and commit convention docs.
- Ignored generated output artifacts and clarified drift workflow.

### Related PRs
- [#1](https://github.com/BasilBarnabyCa/ai-onboarding-protocol/pull/1)
- [#2](https://github.com/BasilBarnabyCa/ai-onboarding-protocol/pull/2)

## Merged Pull Requests (Index)

| PR | Merged (UTC) | Title | Base <- Head |
|---|---|---|---|
| [#11](https://github.com/BasilBarnabyCa/ai-onboarding-protocol/pull/11) | 2026-03-14T02:18:20Z | fix(onboarding): simplify canonical LLM model question wording | `main <- wip` |
| [#10](https://github.com/BasilBarnabyCa/ai-onboarding-protocol/pull/10) | 2026-03-14T01:56:41Z | fix(onboarding): always ask platform and model in Step 0 | `main <- wip` |
| [#9](https://github.com/BasilBarnabyCa/ai-onboarding-protocol/pull/9) | 2026-03-14T01:48:22Z | chore(onboarding): lock Step 0 options to canonical wording | `main <- wip` |
| [#8](https://github.com/BasilBarnabyCa/ai-onboarding-protocol/pull/8) | 2026-03-14T01:36:47Z | feat(onboarding): add final pre-generation context checkpoint | `main <- wip` |
| [#7](https://github.com/BasilBarnabyCa/ai-onboarding-protocol/pull/7) | 2026-03-14T01:32:06Z | feat(onboarding): enforce post-Step-0 guided intake before generation | `main <- wip` |
| [#6](https://github.com/BasilBarnabyCa/ai-onboarding-protocol/pull/6) | 2026-03-14T01:08:14Z | chore: simplify step0 onboarding defaults and overrides | `main <- wip` |
| [#5](https://github.com/BasilBarnabyCa/ai-onboarding-protocol/pull/5) | 2026-03-13T18:57:53Z | Wip | `main <- wip` |
| [#4](https://github.com/BasilBarnabyCa/ai-onboarding-protocol/pull/4) | 2026-03-13T16:52:57Z | feat: enforce sequential step0 and intake gating | `main <- wip` |
| [#3](https://github.com/BasilBarnabyCa/ai-onboarding-protocol/pull/3) | 2026-03-13T14:48:59Z | Codex/readme flow fix | `main <- codex/readme-flow-fix` |
| [#2](https://github.com/BasilBarnabyCa/ai-onboarding-protocol/pull/2) | 2026-03-13T01:43:04Z | Codex/readme flow fix | `main <- codex/readme-flow-fix` |
| [#1](https://github.com/BasilBarnabyCa/ai-onboarding-protocol/pull/1) | 2026-03-12T22:28:31Z | Update README.md | `main <- BasilBarnabyCa-patch-1` |

## Commit History (Index, Non-Merge)

| Commit | Date | Subject |
|---|---|---|
| `6fa923b` | 2026-03-12 | chore(repo): add gitignore and commit conventions |
| `b253ebc` | 2026-03-12 | docs(repo): add onboarding and execution protocol documents |
| `56e6ba5` | 2026-03-12 | docs(onboarding): add agnostic flow with drift audits and stricter scoring gates |
| `e0b7b05` | 2026-03-12 | docs(onboarding): add profile overlays, README, and platform-aware output artifacts |
| `843fe67` | 2026-03-12 | docs(protocol): add brownfield profile selection layer and step-0 intake prompts |
| `ec522ec` | 2026-03-12 | chore(repo): ignore generated output artifacts and clarify drift workflow |
| `9a4bc15` | 2026-03-12 | docs(repo): reorganize protocol and template docs into folders |
| `ba37b9f` | 2026-03-12 | Update README.md |
| `acb4a26` | 2026-03-12 | docs(readme): streamline where-to-start flow for new users |
| `d678366` | 2026-03-12 | docs(commands): enforce strict cmd-prefixed shortcuts and plan input validation |
| `bd04d8b` | 2026-03-12 | docs(readme): simplify strict command shortcut guidance wording |
| `a7c37f8` | 2026-03-12 | docs(protocol): add periodic drift-audit cadence guidance |
| `eff35ac` | 2026-03-13 | feat: strengthen greenfield onboarding and simplify command flow |
| `f2b01e2` | 2026-03-13 | feat: enforce sequential step0 and intake gating |
| `83a0d14` | 2026-03-13 | (docs): updated readme by removing redundant line in where to start |
| `95a747e` | 2026-03-13 | feat: streamline onboarding questions and step0 guidance |
| `d3c314e` | 2026-03-13 | chore: simplify step0 onboarding defaults and overrides |
| `a231bea` | 2026-03-13 | feat(onboarding): enforce post-step0 guided intake before generation |
| `dea7b0e` | 2026-03-13 | feat(onboarding): add final pre-generation context checkpoint |
| `c1688ef` | 2026-03-13 | chore(onboarding): lock Step 0 options to canonical wording |
| `bf8eb23` | 2026-03-13 | fix(onboarding): always ask platform and model in Step 0 |
| `0311c8f` | 2026-03-13 | fix(onboarding): simplify canonical LLM model question wording |
