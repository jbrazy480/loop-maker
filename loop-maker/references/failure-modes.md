# Failure modes → the guardrail line that prevents each

Every one of these is documented from real overnight runs. When generating a master prompt, inject the guardrail lines that apply.

| # | How the run dies | The guardrail line to inject |
|---|---|---|
| 1 | **Declares victory too early** — marks the whole job done after partial work | Feature list on disk with `"passes": false` per item; "Read the feature list at session start and pick ONE item"; definition of done = every item verified or honestly bucketed |
| 2 | **Fake done / lying** — says it passed without running anything | "Evidence, not assertions: show the test output, the command and what it returned, or the screenshot." Verifier ≠ writer. Stop condition checked by a separate evaluator (`/goal`), not the worker |
| 3 | **Gaming the verifier** — weakens or deletes tests to make them pass | "It is unacceptable to remove or edit tests." Keep the feature list in JSON (agents corrupt JSON less than Markdown) |
| 4 | **Placeholder implementations** — stubs dressed up as features | "NO PLACEHOLDER OR SIMPLIFIED IMPLEMENTATIONS. Full implementations only." Completeness critic per phase |
| 5 | **Rebuilds what already exists** | "Before building anything, search the codebase — never assume something isn't implemented" |
| 6 | **Context exhaustion / silent stall** — logs flood the window; compaction at hour 3-4 eats 20-40% of in-flight state | "Redirect long output to files and `tail` the last 20 lines." All state on disk (PROGRESS.md + feature list + git). "Before retrying anything, re-read PROGRESS.md" |
| 7 | **Stops early, human-style** — "finishes" at a human workday pace, or asks a question and waits forever | Never-ask rule with escape hatch (decide, log, move on). Time anchor: "Check the real clock (`date`); if before {{END_TIME}}, define more work and keep going. There are no breaks." |
| 8 | **Loops forever on an impossible item** | "Try 3 genuinely different approaches, then ship the strong 80%, log what got cut, take the next item." Hard cap: "or stop after N turns/hours" |
| 9 | **Blocked ≠ done confusion** — half-baked stub shipped as a win | Honesty buckets: every item ends as done (with evidence) / blocked (what stopped it) / cut (why). "Blocked is not done." |
| 10 | **Scope creep / drift** — forgets constraints over hours | Explicit Out-of-Scope list; scoped to one folder/branch; Never list in AGENTS.md; constraints restated in the master file the agent re-reads |
| 11 | **Environment damage** — deleted DBs, force pushes, burned prod | "Never push, deploy, publish, send, spend, or delete outside scope." No prod credentials in reach. Sandbox/branch/worktree. Commit every green step so anything can be reverted |
| 12 | **Runaway cost** — parallel agents eat a week's quota in minutes | Model-routing table (cheap workers); cap parallel agents; turn/time caps; run on subscription, not raw API, when possible |
| 13 | **Credulous results** — takes a suspiciously good result at face value | "Good-looking results are suspicious. If something passes too easily, hunt for the bug before trusting it" |
| 14 | **Surface patches** — an if-statement for one failing input | "Fix root causes, not symptoms. No special-case patches" |
| 15 | **Trusting the reporter** — believes a UI badge or a worker's claim | "Verify from the source of truth: the DB row, the raw API response, the file on disk — never the thing reporting on itself" |
| 16 | **Parallel collisions** — two loops interleave commits in one repo | One repo/worktree per loop, 3 parallel max; merge verified branches in the morning |
| 17 | **Documentation theater** — most of the output is markdown about work instead of work | Deliverables defined as artifacts (working product, passing tests, rendered video), not reports. Completeness critic checks artifacts, not write-ups |

## The morning-review rule (non-negotiable, tell the user every time)

Treat every output as a draft. The loop does the building; the human stays the boss. Require the run to end with a **morning report**: what shipped, what's blocked/cut, riskiest assumptions ranked by cost of being wrong, and the evidence index.
