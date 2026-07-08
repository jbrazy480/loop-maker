# BUILD LOOP: {{FEATURE_NAME}}

> Everything below this line is your full instruction set. Follow it exactly, including the never-ask rule. Do not report back until the Definition of Done is met or the hard cap is hit.

---

## Goal

{{GOAL — one paragraph: the outcome, not the tasks}}

## Context

- Work lives in: `{{PROJECT_FOLDER}}` on branch `{{BRANCH}}`
- Key files/docs: {{KEY_PATHS}}
- The feature list is `loop/feature_list.json` — every item has verify steps and starts `"passes": false`
- State lives in `loop/PROGRESS.md` — progress log, decision log, honesty buckets
- Project commands (build/test/lint) are in `AGENTS.md` at the repo root

## Constraints

- Only edit files under `{{PROJECT_FOLDER}}`. Never touch secrets, `.env` values, deploy config, or production anything.
- **It is unacceptable to remove or edit tests** — or to weaken a verify step — to make something pass.
- **No placeholder or simplified implementations. Full implementations only.** If you catch yourself writing a stub, stop and build the real thing or move the item to the blocked bucket honestly.
- Before building anything, **search the codebase first** — never assume something isn't already implemented.
- Fix root causes, not symptoms. No special-case patches for one input.
- Nothing outward-facing: no push to shared branches, no deploy, no publish, no send, no delete outside scope, no spending.
{{EXTRA_CONSTRAINTS — or delete this line}}

## Out of scope (do NOT touch — defer to later)

{{OUT_OF_SCOPE — at least one explicit exclusion from the interview}}

## Every session / iteration, in order

1. Run `pwd` and confirm you're in `{{PROJECT_FOLDER}}`.
2. Read `loop/PROGRESS.md` and the last ~10 git log entries to get up to speed.
3. Run the baseline check ({{BASELINE_CHECK — e.g. "start the dev server and complete one end-to-end smoke action"}}) BEFORE new work. If the project is broken, fixing it is your first item.
4. Open `loop/feature_list.json` and pick the **single highest-priority item** with `"passes": false`. One item at a time — never batch.
5. Implement it completely.
6. **Verify it like a skeptic.** Run the item's verify steps end-to-end as a real user would. Evidence, not assertions: capture the test output, the command and what it returned, or the screenshot. Good-looking results are suspicious — if something passes too easily, hunt for the bug before trusting it. Go to the source of truth (the DB row, the raw API response, the file on disk), never a UI badge or your own memory of "I did that."
7. For {{HIGH_STAKES_AREAS — e.g. "anything touching auth, payments, or client-facing UI"}}: spawn a fresh-context reviewer agent to try to REFUTE that the item is done against its acceptance criteria. If it finds real gaps, fix them before moving on.
8. Only after verification: set `"passes": true`, update `loop/PROGRESS.md` (what shipped, decisions made, surprises), and commit with a descriptive message.
9. Redirect long command output to files and `tail` the last ~20 lines — never paste walls of logs into your own context.

## Autonomy — the never-ask rule

I will not answer questions mid-run. Make every call yourself with research and reasoning, log the question + your answer + why in the Decision Log, and keep moving. Blocking is not an option: if an approach fails, try another route; after 3 genuinely different attempts, ship the strong 80% version, log what got cut, and take the next item. Blocked ≠ done — every item ends in exactly one honesty bucket: **done** (verified, with evidence), **blocked** (what stopped it), or **cut** (descoped, why).

There are no breaks and no "that's enough for tonight." Check the real clock (`date`); if it's before {{END_TIME}} and items remain, keep working.

## Delegation & orchestration

For anything bigger than a couple of items, act as an orchestrator: plan and review in this context; delegate implementation, research, and verification to worker agents on cheaper models. Workers return tight summaries, never transcripts. Never let a worker mark its own item as passing — you (or a fresh verifier) confirm it first. Fan out parallel researchers when investigating; adversarially verify big claims with skeptic agents. **These patterns are a floor, not a ceiling.** If the runtime has no subagents, do reviews yourself in a separate pass with fresh eyes, re-reading the item's acceptance criteria first — never from memory.

Model routing — match the model to the task:

| Model | Cost | Intelligence | Taste | Use for |
|---|---|---|---|---|
{{MODEL_TABLE — fill with the models actually available on the chosen platform, e.g. for Claude Code:
| (orchestrator — you) | low volume | highest | highest | plan, delegate, review, judge |
| Sonnet | cheap | high | good | building, research, verification |
| Haiku | cheapest | fine | basic | scouting, bulk checks |}}

## Completeness gate (before declaring done)

Before claiming the Definition of Done, run a **completeness critic**: a fresh-context agent (or a fresh-eyes pass) that walks `loop/feature_list.json` and the full diff asking "what's missing, unverified, or half-real?" Anything it finds becomes new feature-list items. The run isn't done until the critic comes back dry.

## Definition of Done

The run is complete when **every item in `loop/feature_list.json` has `"passes": true`**, {{FINAL_CHECKS — e.g. "`npm test` exits 0, `npm run lint` is clean"}}, the completeness gate came back dry, and `loop/PROGRESS.md` ends with a morning report: what shipped, what's blocked or cut, the riskiest assumptions ranked by cost of being wrong, and the evidence for each verified item.

Items may end bucketed blocked/cut ONLY as the exception: every priority-1 item must be **done**, and if more than a third of all items end blocked or cut, the run is NOT done — write why in the morning report and keep working until the hard cap.

Hard stop: {{TURN_OR_TIME_CAP — e.g. "or stop after 100 turns / at 6:30 AM, whichever comes first"}}.
