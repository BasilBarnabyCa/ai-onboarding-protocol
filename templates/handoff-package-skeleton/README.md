# Handoff Package Skeleton (AGNOSTIC — do not put project-specific content here)

This skeleton defines the standard handoff-package layout for ANY legacy-project migration (Playbook Phase E). To assemble a project's package:

1. Copy this skeleton to the legacy repo root as `handoff-package/`.
2. Fill `docs/` from `/ai-onboarding/output/` (the project-specific generated artifacts).
3. Fill `assets/` with the brand files named in the project's UX_BRAND_SPEC §1/§3 (logos, favicons, fonts).
4. Replace `PACKAGE_README_TEMPLATE.md` placeholders and save as the package's `README.md`.
5. Adapt `claude/settings.json` allow-list to the target stack's CLIs (deny list stays).

```
handoff-package/                   ← PROJECT-SPECIFIC ONLY; the framework stays in ai-onboarding/
├── README.md                      ← from PACKAGE_README_TEMPLATE.md (filled)
├── docs/
│   ├── HANDOFF.md                 ← output/NEW_PROJECT_HANDOFF.md
│   ├── LEGACY_DETAIL_APPENDIX.md  ← output/LEGACY_DETAIL_APPENDIX.md
│   └── UX_BRAND_SPEC.md           ← output/UX_BRAND_SPEC.md
├── claude/
│   ├── settings.json              ← agnostic base (adapt allow-list per stack)
│   └── CLAUDE_RULES.md            ← agnostic command rules (copy as-is)
└── assets/                        ← project brand files (img/, fonts/)
```

The `claude/` files in this skeleton are agnostic and travel unchanged except for stack-CLI allow entries. Everything under `docs/` and `assets/` is project-specific OUTPUT — it is generated per project and never lives in this skeleton. Do NOT copy framework templates into the package; everything needed to RUN the workflow on the next legacy project ships inside `ai-onboarding/` itself.
