# 🔁 loop-maker — write loops, not prompts

**Stop babysitting your AI. Tell it what you want, walk away, come back to finished work.**

This is a free skill for Claude Code (and it works with Codex, Cursor, and other AI agents too). You describe what you want in plain English, and it writes you a complete, *safe* autonomous run — a master prompt, a plan, a checker, and one command to launch it. The same pattern people are using to ship apps overnight and even have an AI build an entire company in one 4-hour run.

Built on the loop-engineering playbook: Anthropic's own long-running-agent research, the Ralph Wiggum loop, and the plan-delegate-review method (the smart model manages, cheaper models build — that's how a whole company costs ~500K orchestrator tokens instead of millions).

Made by James (@ EveryThingAI). If you got this from my Instagram — enjoy. 🙏

---

## 📦 Install — 3 steps, ~60 seconds (no tech skills needed)

You need **Claude Code** installed first (the AI coding tool from Anthropic — free to start at https://claude.com/claude-code). Once you have it:

**1. Find your skills folder.** Open this location (copy-paste it):
```
~/.claude/skills/
```
- On Mac: open Finder → press `Cmd+Shift+G` → paste `~/.claude/skills/` → Enter. (If the `skills` folder doesn't exist, create a folder named `skills` inside the `.claude` folder.)
- On Windows: it's at `C:\Users\YOUR-NAME\.claude\skills\`

**2. Drop the whole `loop-maker` folder into it.** So you end up with:
```
~/.claude/skills/loop-maker/
```

**3. Restart Claude Code** (close it and open it again). Done. ✅

---

## ▶️ How to use it

Open Claude Code and type the word **loop**, then say what you want. Examples:

> **loop** — build me a landing page for my coffee shop, make it look good on a phone

> **loop** — add a login screen to my app and don't stop until the tests pass

> **loop** — run all night: build me a complete company from scratch, launch video and all

It will then:
1. Ask a couple quick questions, one at a time (only if it needs to)
2. Write your **master prompt file** — mission, guardrails, phases, and a real definition of done
3. Write the **plan files** — a feature list the AI checks off, and a progress file so nothing gets lost
4. Set up the **checker** — the AI has to prove its work with evidence, never just say "done"
5. Hand you **one command to paste** — then you walk away

That's it. You're not prompting anymore. You're running a loop.

---

## ✅ Why it won't make garbage while you sleep

Every run it writes has the three things that keep an overnight run from going off the rails:

| Part | What it does for you |
|---|---|
| **The Spec (the pin)** | Stops the AI from inventing stuff you didn't ask for |
| **The Checker (not the writer)** | The AI can't just *say* it's done — it has to prove it with evidence |
| **The Stop Condition** | A real finish line plus a hard cap, so it actually stops |

Plus the rules the pros converged on: never ask the human (decide, log it, keep moving) · no placeholder work · never touch the tests to make them pass · one item at a time · everything saved to files so a crash loses nothing · nothing gets published, deployed, or spent from inside a loop.

**One honest rule it always tells you:** review the work in the morning. The loop does the building; you stay the boss.

---

## ❓ Stuck?

- "I don't have Claude Code" → get it free: https://claude.com/claude-code
- "I can't find the .claude folder" → it's hidden; on Mac use `Cmd+Shift+G` in Finder and paste `~/.claude`
- "It's not working" → make sure the folder is exactly `~/.claude/skills/loop-maker/` and you restarted Claude Code
- Anything else → ask in the free community: **https://www.skool.com/evolving-ai-hub**

🎓 **Join Evolving AI Hub on Skool** for every skill and prompt system we drop: **https://www.skool.com/evolving-ai-hub**

Want the system that runs your whole business this way (not just code)? → **evrythingai.com**
