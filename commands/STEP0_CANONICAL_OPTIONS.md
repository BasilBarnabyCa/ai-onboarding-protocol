# STEP0_CANONICAL_OPTIONS.md

Use these Step 0 prompts/options verbatim. Do not paraphrase, reorder, add, or remove options.

## Mode Question (ask first)

```text
Which setup matches your situation?
1) greenfield - new project or idea with little/no existing implementation.
2) brownfield - existing repo/system you want to onboard and improve.
```

Accept: `1|2|greenfield|brownfield`.

## Platform Question (ask every run)

```text
Which execution platform are you using for this onboarding run?
1) Codex
2) Claude Code
3) ChatGPT
4) Other
```

Accept: `1|2|3|4|Codex|Claude Code|ChatGPT|Other`.

If a platform is auto-detected, show it as a suggested default but still ask this question explicitly.

## Platform Model/Version Question (ask every run)

```text
Which platform model/version should be recorded for this run?
If the detected value is correct, reply: same
Otherwise, provide the model/version text.
```

Accept: `same` or non-empty free text.

## Capability Profile Question

```text
Select capability profile:
1) Auto-detect (recommended)
2) Locked-down
3) Standard
4) High-trust
5) All-access (explicit approval required)
```

Accept only one number: `1|2|3|4|5`.
