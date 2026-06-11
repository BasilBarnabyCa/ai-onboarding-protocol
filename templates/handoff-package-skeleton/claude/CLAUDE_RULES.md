# Command Rules — merge this block into the new project's CLAUDE.md

These rules prevent permission prompts that allowlists cannot suppress. No exceptions.

```markdown
## Command rules (prevent permission prompts — no exceptions)

- Run git plainly from the repo root. NEVER `cd <dir> && git ...` (flagged: untrusted hooks).
- Reach subpackages with `npm --prefix <app> <cmd>` or root workspace scripts — not `cd`.
- NEVER prefix commands with inline env assignments (`VAR=x cmd`) — bypasses the
  allowlist and leaks credentials into logs. Env values live in gitignored env files
  (`.env`, `.env.test`), mirrored in `.env.example`, loaded via package scripts
  (dotenv-cli), e.g. `"db:migrate:test": "dotenv -e .env.test -- npx prisma migrate deploy"`.
- NEVER use shell loops, variable expansion ($var), heredocs (`cat > file <<EOF`), or
  sed/awk/echo pipelines to create or transform files (flagged: simple_expansion /
  sed write ops). Use Read/Write/Edit tools for ALL file work. Shell is only for
  running programs: npm, npx, node, git, CLIs.
- When intentionally duplicating code across SPAs (trust boundaries stay separate),
  note the duplication in PROGRESS.md.
- Legacy repo access (if granted): READ-ONLY. Never read the legacy .env. Never write there.
```

Setup notes:
- Copy `claude/settings.json` from this package to `.claude/settings.json` in the new repo root.
- The deny list keeps: production env reads, git push, recursive deletes. Local `.env`/`.env.test`
  reads are deliberately ALLOWED in unattended mode — the AI manages those files with values
  the user provides at pre-flight; "never commit env files" is enforced via .gitignore instead.
- Add further stack CLIs to allow as needed (test runners, etc.).
