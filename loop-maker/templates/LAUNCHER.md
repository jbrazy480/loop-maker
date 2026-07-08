# Launcher prompts

The short prompt the user actually pastes. It points at the master file — `/goal` has a ~4,000-character limit, so the real instructions live in the file and this launcher has no ceiling.

## Claude Code (default)

```
/goal Read {{MASTER_FILE_PATH}} and execute everything below the divider line as your goal. That file is your full instruction set — mission, guardrails, phases, deliverables, and definition of done. Follow it exactly, including the never-ask rule. Do not report back until the Definition of Done in that file is met, or stop after {{N_TURNS}} turns. Start now.
```

Run it with auto mode on (`/permissions` → pre-allow the safe commands, or start the session with `claude --permission-mode auto`) so no tool prompt stalls the run at 2 AM.

## Codex / Cursor / any other agent

```
Read {{MASTER_FILE_PATH}} and execute everything below the divider line as your task. That file is your full instruction set — follow it exactly, including the never-ask rule. Do not stop or ask questions until the Definition of Done in that file is met. Start now.
```

## Headless / scheduled (Claude Code)

```bash
caffeinate -i claude -p "/goal Read {{MASTER_FILE_PATH}} and execute everything below the divider line as your goal. Follow it exactly including the never-ask rule. Do not report back until the Definition of Done is met, or stop after {{N_TURNS}} turns." --permission-mode auto --output-format json < /dev/null
```

(`caffeinate -i` keeps a Mac awake; `< /dev/null` stops headless runs hanging on stdin; the JSON output includes total cost.)
