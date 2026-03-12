# PROFILE_REGISTRY.md

This registry defines selectable brownfield overlays.

## Selection Fields

- `id`: stable profile identifier
- `type`: domain and lifecycle scope
- `status`: `active` or `planned`
- `indicators`: evidence patterns used for auto-detection
- `artifact`: overlay file to apply when selected

## Profiles

| id | type | status | indicators (examples) | artifact |
|---|---|---|---|---|
| `software-brownfield` | existing software systems | active | `package.json`, lockfiles, route/controller folders, schema/migration files, CI workflows | `/ai-onboarding/profiles/software-brownfield/SOFTWARE_BROWNFIELD_MASTER_CONTEXT_ARTIFACT.md` |
| `cybersecurity-brownfield` | existing security programs/systems | planned | security runbooks, control matrices, policy docs, SIEM/SOAR configs, threat model docs | `TBD` |
| `data-brownfield` | existing data/analytics systems | planned | dbt/sql model folders, warehouse configs, pipeline DAGs, data contracts | `TBD` |
| `ops-brownfield` | existing operations/process systems | planned | runbooks, SLO/SLI docs, incident workflows, change calendars | `TBD` |

## Notes

- Planned profiles are not auto-selectable until an artifact is created.
- If no active profile meets selection thresholds, use agnostic baseline and ask one disambiguation question.
