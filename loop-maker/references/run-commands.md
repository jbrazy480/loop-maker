# Launch commands per platform

Fill in and hand over exactly ONE of these (see `templates/LAUNCHER.md` for the launcher prompt text itself).

## Claude Code — interactive `/goal` (the default)

```
/goal Read loop/MISSION.md and execute everything below the divider line as your goal. Follow it exactly, including the never-ask rule. Do not report back until the Definition of Done in that file is met, or stop after {{N_TURNS}} turns. Start now.
```

- `/goal` keeps Claude working turn after turn; a separate small model evaluates the condition after each turn — that separation is a built-in verifier.
- Always include the turn cap **inside the goal text** ("or stop after N turns") — it's the real safety net.
- Pair with auto mode so tool prompts don't stall the run: pre-allow safe commands via `/permissions`, or launch with `claude --permission-mode auto`.
- The evaluator only judges what's in the transcript — that's why the master prompt demands evidence (test output, screenshots) be shown, not summarized.

## Claude Code — headless / scheduled

```bash
caffeinate -i claude -p "/goal Read loop/MISSION.md and execute everything below the divider line as your goal. Follow it exactly including the never-ask rule. Do not report back until the Definition of Done is met, or stop after {{N_TURNS}} turns." \
  --permission-mode auto --output-format json < /dev/null
```

- `caffeinate -i` (Mac) keeps the machine awake; the lid must stay open on Apple Silicon.
- `< /dev/null` — headless runs hang waiting on stdin without it.
- `--output-format json` reports total cost per invocation.
- For scheduled nightly runs: cron this ONCE per night. Waking up to one small verified increment every morning beats waking up to 50 unreviewed ones.

## Codex (cloud task or CLI)

Paste the generic launcher into a Codex cloud task (or the CLI):

```
Read loop/MISSION.md and execute everything below the divider line as your task. That file is your full instruction set — follow it exactly, including the never-ask rule. Do not stop or ask questions until the Definition of Done in that file is met. Start now.
```

- Codex reads `AGENTS.md` natively (repo root, nested files win) — the scaffold's AGENTS.md carries the commands and Never list.
- Codex cloud tasks return results as PRs — remind the user the morning review IS the PR review.

## Cursor / any other agent runtime

Same generic launcher prompt. The scaffold is deliberately portable: all state is markdown/JSON files, all verification is shell commands, and the master prompt never names a platform tool. If the runtime has no goal/loop feature, the fallback is the classic outer loop — re-send the same launcher whenever the agent stops, until the Definition of Done holds; the files on disk carry the state between iterations.

## Parallel runs (advanced)

2-3 things at once → one git worktree per loop, one `/goal` per worktree, merge verified branches in the morning. 3 max — the human morning review is the bottleneck, and same-repo parallel loops interleave commits.
