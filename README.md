<div align="center">

# 🔁 loop-maker

### Stop prompting your AI. Start writing loops.

**A free Claude Code skill that turns "here's what I'm building" into a complete, safe loop your AI runs by itself — builds, checks its own work, and stops when it's actually done.**

The thing people are using to ship apps overnight.

</div>

---

## Why this exists

In June 2026, two people who'd know said the same thing and broke the AI-coding internet:

- **Peter Steinberger** (creator of OpenClaw): *"You shouldn't be prompting coding agents anymore. You should be designing loops that prompt your agents."*
- **Boris Cherny** (creator of Claude Code): his job is now "to write loops" — he ships 20-30 features a day this way.

This skill makes that pattern push-button. You describe what you want, it writes you a safe loop, you walk away.

---

## Prompt vs. Loop (the whole idea in 30 seconds)

**A prompt** = you ask, the AI does one thing, it stops, *you* read it, *you* ask again. You're the engine. You stop → it stops. So when you sleep, work stops.

**A loop** = you write down three things once: (1) what to build, (2) how it checks its own work, (3) when it's allowed to stop. Then the system runs the AI over and over by itself until that stop condition is true. **The loop is the engine.** That's why work continues while you sleep.

It's the difference between cold-calling every lead by hand vs. a system that dials and follows up all night without you. Same idea — now for building.

---

## The 3 things that keep a loop from making garbage overnight

This is the part everyone gets wrong. A loop is only safe because of three parts working together. **loop-maker never writes a loop missing one:**

| Part | What it does |
|---|---|
| **1. The Spec (the pin)** | What to build + what's explicitly OUT of scope. Stops the AI inventing things you didn't ask for. |
| **2. The Verifier (NOT the writer)** | The AI that writes the code can't decide it's done — tests, a screenshot, or a second AI judge checks it. The writer never grades its own homework. |
| **3. The Stop Condition (provable)** | A real finish line the work can *prove* it hit ("all tests pass AND the screenshot looks right"). Never "make it good" — that's unprovable and the loop runs forever or lies. |

Take away any one → overnight garbage. That's the whole secret.

---

## Install (60 seconds)

1. You need **Claude Code** (free: https://claude.com/claude-code).
2. Drop the `loop-maker/` folder from this repo into your skills directory:
   ```
   ~/.claude/skills/loop-maker/
   ```
   (Mac: Finder → `Cmd+Shift+G` → paste `~/.claude/skills/` → drop the folder in. Create the `skills` folder if it's not there.)
3. Restart Claude Code. Done. ✅

Full step-by-step in [`loop-maker/INSTALL.md`](loop-maker/INSTALL.md).

---

## Use it

Open Claude Code and type **`loop`**, then say what you're building:

> **loop** — build me a landing page for my coffee shop, make it look great on mobile

> **loop** — add a login screen and don't stop until the tests pass

> **loop** — clean up the bugs in this project while I sleep

It will:
1. Ask a couple quick questions (only if needed)
2. Write the **spec** (what to build, what not to touch)
3. Set up the **verifier** (so it proves its work)
4. Hand you **one command to paste** — then you walk away
5. Give you the honest **safety rules**

---

## The one rule it always tells you

**The loop does the building. You stay the boss.** Review the work in the morning — the loop amplifies your judgment, it doesn't replace it. It's scoped to one folder so a bad run can't hurt the rest, and nothing risky (deploys, sends, secrets) happens without you.

---

## Who made this

Built by **James** — I run [EveryThingAI](https://evrythingai.com), where we build the AI system that runs a founder's whole business (not just code). This skill is a free taste of how we think.

If it helps you ship something, ⭐ the repo and tag me when you launch.

More free tools: [aiguyofficial.com/resources](https://aiguyofficial.com/resources)

## License

MIT — use it, fork it, build on it.
