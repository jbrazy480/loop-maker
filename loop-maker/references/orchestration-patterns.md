# Orchestration patterns

The delegation vocabulary that goes into every master prompt. The single most load-bearing paragraph in a master prompt is the one that DEFINES what "orchestrate" means — spell these out explicitly and always end with: **"the patterns above are a floor, not a ceiling."**

## The prime directive: plan, delegate, review

The orchestrator (the smartest/most expensive model) never builds anything. It plans the work, delegates every piece of execution to worker agents on cheaper models, reviews what comes back, and sends back anything not good enough with specific instructions to do it better.

Why this wins (all field-tested):
- A whole company was built with ~500K orchestrator tokens because every worker was a cheaper model.
- Smart-orchestrator + cheap-workers produces results roughly equal to smart-orchestrator + smart-workers at a fraction of the cost (tested repeatedly: Opus orchestrating Haiku scouts was ~3x cheaper with identical results).
- The orchestrator's context is the scarcest resource in the run. Workers return **tight summaries (1-2K tokens), never transcripts.** Long command output goes to a file, then `tail`.

## The patterns

**Fan-out researchers** — parallel agents each searching a different way (by source, by angle, by community, by time period). Each is blind to the others; one search angle never finds everything. Merge + dedupe afterward.

**Independent verifiers** — for every important claim or quote a researcher brings back, a separate agent re-fetches the source and confirms it's real and in context. Invent nothing.

**Tournament + judge panel** — when picking between options (business ideas, designs, names, approaches): independent agents each pitch a competing option; a panel of judge personas scores all of them on explicit criteria (for business ideas: pain, urgency, reachability, willingness to pay, buildability, incumbent weakness). Good for taste decisions where there's no objective test.

**Advocate + skeptic pairs** — every finalist gets one agent arguing FOR it and one whose only job is to tear it apart; then FRESH judges (who saw neither pitch made) vote.

**Adversarial verification** — for every finding or "done" claim, spawn a skeptic agent whose only job is to refute it. A skeptic checking an optimist. For high stakes, use 2-3 skeptics and let majority-refute kill the claim. This is the single most-adopted pattern in the field — it's the antidote to agents grading their own homework.

**Completeness critic** — before ANY phase is called done, a fresh agent asks: "What's missing? Which claim is unverified? Which angle wasn't covered? Which deliverable is half-real?" What it finds becomes the next round of work. Repeat until it comes back dry.

**Red team ("try to kill it")** — a dedicated phase near the end: skeptic agents attack the biggest claims (market size, pricing, security, correctness). Rule on every attack, apply every accepted fix back into the plan AND the artifact, keep the honesty artifacts.

**Loop-until-dry** — for discovery work (bugs, problems, edge cases): keep spawning finders until 2 consecutive rounds return nothing new. Fixed counts miss the tail.

## Model-routing table

Give the orchestrator an explicit table of the models in its toolkit, scored on **cost / intelligence / taste**, and let it route each task. Taste = creativity, UI/UX judgment, writing voice. Intelligence = reasoning, code review, planning. Route by what the task needs, not by habit:

- Judging, planning, final review → highest intelligence
- Building, drafting, research synthesis → mid-tier (this is where most tokens go)
- Scouting, scraping, bulk checks, formatting → cheapest

## When NOT to multi-agent

Tightly-coupled coding where every piece needs the same shared context is a bad fit for parallel agents (they duplicate work and collide). For that, keep one builder and use agents only for research and verification. Multi-agent systems burn ~15x the tokens of a single chat — spend that on verification and research, where fresh context is the point.
