# STEP0_CANONICAL_OPTIONS.md

Use these Step 0 questions verbatim. Do not paraphrase, reorder, add, or remove questions/options.

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
Which LLM model should be recorded for this run? (example: GPT-5, Claude Sonnet 4)
If I show a detected model and it is correct, reply: yes
Otherwise, provide the corrected model text.
```

Accept: `yes` or non-empty free text.

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
