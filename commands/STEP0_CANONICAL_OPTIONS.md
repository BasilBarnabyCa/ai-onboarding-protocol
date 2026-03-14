# STEP0_CANONICAL_OPTIONS.md

Use these Step 0 prompts/options verbatim. Do not paraphrase, reorder, add, or remove options.

## Mode Question (ask first)

```text
Which setup matches your situation?
1) greenfield - new project or idea with little/no existing implementation.
2) brownfield - existing repo/system you want to onboard and improve.
```

Accept: `1|2|greenfield|brownfield`.

## Platform Question (ask only if not auto-detected)

```text
Which execution platform are you using for this onboarding run?
1) Codex
2) Claude Code
3) ChatGPT
4) Other
```

Accept: `1|2|3|4|Codex|Claude Code|ChatGPT|Other`.

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
