# {{PROJECT_NAME}} — agent rules

<!-- Keep this file ≤60 lines. Commands and conventions only — status lives in loop/PROGRESS.md, never here. -->
<!-- Portability: this AGENTS.md is read natively by Codex, Cursor, Gemini, Copilot. For Claude Code, create a CLAUDE.md whose first line is: @AGENTS.md -->

## Commands
- Install: `{{INSTALL_CMD}}`
- Dev server: `{{DEV_CMD}}`
- Test: `{{TEST_CMD}}`
- Lint: `{{LINT_CMD}}`
- Typecheck: `{{TYPECHECK_CMD}}`

## Conventions
- {{CONVENTION_1 — e.g. Match the existing UI: reuse components/styles already in the codebase before creating new ones}}
- {{CONVENTION_2 — e.g. Mobile-first: every screen must work on a phone}}
- {{CONVENTION_3 — e.g. Simple enough that an 80-year-old could use every screen}}

## Always
- Search the codebase before building — never assume something isn't implemented
- Run test + lint after every change; commit only when green
- Verify from the source of truth (DB row, raw API response, file on disk), not a UI badge
- Redirect long output to a file and `tail` it
- Before retrying anything, re-read `loop/PROGRESS.md`

## Never
- Never delete files to resolve errors, force push, or skip/weaken/edit tests
- Never touch `.env` values, secrets, deploy config, or production
- Never push, deploy, publish, send, or spend from inside a loop
- Never write placeholder/stub implementations and call them done
