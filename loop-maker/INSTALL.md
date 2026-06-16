# 🔁 loop-maker — write loops, not prompts

**Stop babysitting your AI. Tell it what you're building, walk away, come back to finished work.**

This is a free Claude Code skill. You describe what you want to build in plain English, and it writes you a complete, *safe* "loop" — an autonomous run that builds, checks its own work, and stops when it's actually done. The thing people are using to ship apps overnight.

Built on the loop-engineering idea Peter Steinberger and Boris Cherny (the creator of Claude Code) made famous: stop typing prompts one at a time — design a loop that runs itself.

Made by James (@ EveryThingAI). If you got this from my Instagram — enjoy. 🙏

---

## 📦 Install — 3 steps, ~60 seconds (no tech skills needed)

You need **Claude Code** installed first (it's the AI coding tool from Anthropic — free to start at https://claude.com/claude-code). Once you have it:

**1. Find your skills folder.** On your computer, open this location (copy-paste it):
```
~/.claude/skills/
```
- On Mac: open Finder → press `Cmd+Shift+G` → paste `~/.claude/skills/` → Enter. (If the `skills` folder doesn't exist, just create a folder named `skills` inside the `.claude` folder.)
- On Windows: it's at `C:\Users\YOUR-NAME\.claude\skills\`

**2. Drop the whole `loop-maker` folder into it.** So you end up with:
```
~/.claude/skills/loop-maker/
```
(the folder with this README and SKILL.md inside it)

**3. Restart Claude Code** (close it and open it again). Done. ✅

---

## ▶️ How to use it (this is the whole thing)

Open Claude Code and just type the word **loop**, then say what you're building. Examples:

> **loop** — build me a landing page for my coffee shop, make it look good on a phone

> **loop** — add a login screen to my app and don't stop until the tests pass

> **loop** — clean up all the bugs in this project while I sleep

It will then:
1. Ask you a couple quick questions (only if it needs to)
2. Write a **spec** — exactly what to build, and what NOT to touch
3. Set up a **checker** — so the AI proves its own work instead of guessing it's done
4. Give you **one command to paste** — then you walk away
5. Tell you the honest **safety rules** (always review it in the morning)

That's it. You're not prompting anymore. You're running a loop.

---

## ✅ Why it won't make garbage while you sleep

Every loop it writes has the 3 things that keep an overnight run from going off the rails:

| Part | What it does for you |
|---|---|
| **The Spec (the pin)** | Stops the AI from inventing stuff you didn't ask for |
| **The Checker (not the writer)** | The AI can't just *say* it's done — it has to prove it |
| **The Stop Condition** | A real finish line, so it knows when to actually stop |

Take away any one of these and you get the overnight mess everyone's scared of. loop-maker never hands you a loop missing one.

**One honest rule it always tells you:** review the work in the morning. The loop does the building; you stay the boss.

---

## ❓ Stuck?

- "I don't have Claude Code" → get it free: https://claude.com/claude-code
- "I can't find the .claude folder" → it's hidden; on Mac use `Cmd+Shift+G` in Finder and paste `~/.claude`
- "It's not working" → make sure the folder is exactly `~/.claude/skills/loop-maker/` and you restarted Claude Code

Want the system that runs your whole business this way (not just code)? → **evrythingai.com**
```
