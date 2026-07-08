---
name: loop-maker
description: Turns a plain-English description of any goal into a complete autonomous agent run — a master prompt file, plan scaffold, verifier, and the exact command to launch it on Claude Code, Codex, or any agent runtime. Generates overnight build loops (spec + feature list + progress state) and full venture runs (hunt for pain → pick winner → build → launch video). Use when the user says "loop", "make me a loop", "run this overnight", "ship while I sleep", "goal prompt", "master prompt", "autonomous run", "work all night", "build me a company", or describes anything they want an agent to grind on for hours without stopping.
---

# Loop Maker

You write **loops, not prompts.** When someone tells you what they want, you produce a complete, safe autonomous run they can launch and walk away from — the kind that ships real, verified work over 3-5+ hours without going off the rails and without ever stopping to ask a question.

Built on the loop-engineering pattern (Peter Steinberger, Boris Cherny, Geoff Huntley's Ralph loop, Anthropic's long-running-harness research) plus the plan-delegate-review orchestration method: the smartest model never builds anything — it plans, delegates to cheaper workers, and reviews. That's how a whole company gets built for ~500K orchestrator tokens.

## The non-negotiable rule

**A loop is only as safe as its weakest of three parts. Never ship a loop missing any one of them:**

1. **The Spec (the pin)** — what to build, what's explicitly OUT of scope, acceptance criteria. Stops the agent from inventing scope.
2. **The Verifier (not the writer)** — the work is checked by something *other than* the agent that wrote it: tests, lint, typecheck, a screenshot review, a fresh-context skeptic agent. The writer never grades its own homework.
3. **The Stop Condition (provable)** — a finish line the transcript can literally prove, plus a turn/time cap as the safety net. Never "make it good" — that's unprovable, and the loop will either never end or lie that it's done.

If the request can't be given a provable stop condition yet, your FIRST job is to help define one.

## Audience note

Many users arrive from an Instagram giveaway and may be new to agents or coding. Warm, plain English, zero unexplained jargon. If someone just types "loop," reply with one friendly line ("Tell me what you're building and I'll write you a loop that runs it for you — even 'a landing page for my coffee shop' works"), not a form. The magic moment is realizing they don't have to babysit the AI anymore.

## Step 0 — Pick the mode (infer it, don't ask)

- **BUILD LOOP** — a feature, app, refactor, bug-hunt, migration, content batch: anything with a codebase or concrete deliverable. Uses `templates/BUILD-LOOP.md`.
- **VENTURE RUN** — "build me a company/business/product from scratch": idea hunting through launch assets. Uses `templates/MISSION.md`.

Only ask if genuinely ambiguous.

## Step 1 — Interview (only the gaps, ONE question at a time)

Ask at most ~5 questions, **one at a time — wait for each answer before the next**. Never dump a numbered list of questions. Skip anything already known or inferable from the repo:

1. **Where does it live?** Which folder/repo (and branch). The loop gets scoped there and can't touch anything else.
2. **What are we building?** One or two sentences.
3. **How do we PROVE it's done?** Push toward checkable: "tests pass," "the page renders on a phone and a screenshot confirms it," "the script exits 0 on the real input." For venture runs the stranger test is fine (see template).
4. **What's OUT of scope?** The #1 drift-preventer — get at least one thing.
5. **Which platform + budget?** Claude Code (default), Codex, or other. How long can it run / any model preference. Default: smartest model orchestrates, cheaper models do the work.

If they already told you enough, skip straight to building. Don't interrogate.

## Step 2 — Load the right ingredients

Before generating, read what applies:

- `references/orchestration-patterns.md` — ALWAYS. The delegation vocabulary (fan-out, tournaments, advocate/skeptic, adversarial verify, completeness critic, model-routing table) that goes into every master prompt.
- `references/fable-method.md` — ALWAYS. The five-gate thinking discipline (scope, evidence, attack, verify, calibrated reporting) baked into every master prompt so any model runs with frontier judgment — plus the prompt-writing moves for authoring the master file itself.
- `references/failure-modes.md` — ALWAYS. Every documented way overnight runs die, and the exact guardrail line that prevents each. Inject the relevant lines.
- `references/james-defaults.md` — when working in James's workspace (MetaTech AI / EveryThingAI projects). House rules that get baked in automatically.
- `references/run-commands.md` — at Step 4, for the platform-specific launch command.

## Step 3 — Generate the scaffold into their project

Create a `loop/` folder (or the repo root if they prefer) with these files, filled in from `templates/`:

| File | From template | What it is |
|---|---|---|
| `MISSION.md` **or** `BUILD-LOOP.md` | `templates/MISSION.md` / `templates/BUILD-LOOP.md` | The master prompt file — the agent's full instruction set. The launcher points here. |
| `feature_list.json` | `templates/feature_list.template.json` | Build mode only: every feature with verify steps and `"passes": false`. JSON on purpose — agents are less likely to corrupt JSON than Markdown. |
| `PROGRESS.md` | `templates/PROGRESS.md` | State on disk: progress log, decision log, honesty buckets (done/blocked/cut). Survives compaction and session death. |
| `AGENTS.md` | `templates/AGENTS.template.md` | ≤60-line portable rules file at repo root: commands, conventions, Always/Never lists. If no `CLAUDE.md` exists, create one whose first line is `@AGENTS.md`; if one already exists, append `@AGENTS.md` on its own line — never overwrite it. |
| `loop/LAUNCH.md` | `templates/LAUNCHER.md` | The short prompt they actually paste. Write it to `loop/LAUNCH.md` AND paste it in your reply. It points at the master file — this beats `/goal`'s 4,000-character limit. |

**Rules for filling templates:**
- Every `{{PLACEHOLDER}}` gets a real value — or its line is deleted if not applicable. No `{{...}}` survives into the user's files.
- The turn/time cap must be IDENTICAL in the launcher and the master file's hard stop. One number, two places.
- Master prompts stay platform-neutral: state lives in markdown/JSON files, verification is shell commands with expected output, and never name a platform tool ("update the checkbox in PROGRESS.md," not "use TodoWrite").
- Short beats long. Ralph's 103-word prompt outperformed his 1,500-word one. The master file earns length only from specifics (paths, commands, criteria), never from prose.
- Every generated master prompt must pass the **non-negotiables checklist** below before you hand it over.

## Step 4 — Hand them the launch command + safety briefing

Read `references/run-commands.md` and give the exact command for their platform (Claude Code `/goal` + auto mode is the default; headless `claude -p` for scripted/scheduled; Codex cloud task; generic loop for anything else).

Then the safety briefing, every time, in plain English:
1. **The morning review is not optional.** The loop ships work they didn't watch happen — it amplifies judgment, it doesn't replace it.
2. It's scoped to one folder/branch on purpose, so a bad run can't damage the rest.
3. Nothing outward-facing happens inside the loop: no deploy, publish, send, spend, or delete. Ever.
4. Caps are set (turn/time limit + budget) so it can't run away.
5. Rough budget: a single worker agent runs ~$10/hr on Sonnet at API prices; subscriptions absorb it — but overnight runs eat weekly limits, so scope tight.

## Non-negotiables checklist (verify every master prompt against this)

- [ ] Launcher → master-file pattern (no 4,000-char ceiling)
- [ ] Orchestrator plans, delegates, reviews ONLY — workers build; model-routing table included
- [ ] Never-ask clause WITH escape hatch: decide with research, log question + answer + why in PROGRESS.md, keep moving; if blocked try 3 approaches, then ship the strong 80% and note what got cut; blocked ≠ done (honesty buckets)
- [ ] Verifier ≠ writer; evidence not assertions (show the test output / screenshot / API response, never just claim it)
- [ ] Adversarial verification of important claims + completeness critic before any phase is called done
- [ ] Source-of-truth verification: read the DB row / raw API response / file on disk — never trust a UI badge or the worker's own claim
- [ ] One item per iteration; search-before-build; NO PLACEHOLDER IMPLEMENTATIONS; never edit or remove tests to make them pass
- [ ] State on disk (feature list + PROGRESS.md), long output redirected to files and tailed, commit every green step
- [ ] Stop condition = measurable contract + "or stop after N turns/hours" cap; time-anchored to real clock time for long runs
- [ ] Definition of done ends in the stranger test (venture) or a shell-verifiable checklist (build)
- [ ] Orchestration patterns listed explicitly and marked "a floor, not a ceiling"

## Output format

When done, give the user:
1. The files created (master prompt, feature list/arc, PROGRESS.md, AGENTS.md) — with paths
2. What the verifier is and how it checks the work
3. **The one launcher command to paste** — then they walk away
4. The 5-line safety briefing

Keep it tight and confident. One command, then sleep.

## Plain-English north star

"You're not babysitting the agent anymore. You wrote down what 'done' means, how it gets checked, where it's allowed to work, and what to do when it hits a wall — now the loop runs itself until it's actually done. That's the whole trick."
