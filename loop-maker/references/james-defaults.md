# James's house rules (auto-inject when working in James's workspace)

When Loop Maker runs inside James's projects (MetaTech AI / AI Guy Official / RizzDial / FounderOS / client work), bake these into every generated master prompt and AGENTS.md without being asked. For giveaway users, these are a good default "Conventions" starting point too.

## Product & UI
- **Research before you decide.** Every meaningful choice starts with real research; log it in the Decision Log.
- **Match the existing UI.** Reuse the components, styles, and patterns already in the codebase before inventing new ones.
- **Mobile-first, always.** Every screen works on a phone from day one; test it there.
- **The 80-year-old test.** Every screen simple enough that an 80-year-old could use it: obvious labels, one primary action, no jargon, big targets.
- **Every page has a way back** (visible exit to the dashboard/home).
- **White-label discipline.** No vendor names visible anywhere client-facing.

## Verification (the one habit that must survive into every run)
- **Test everything, as you go.** Nothing is done until exercised end-to-end.
- **Verified, not assumed — go to the source of truth.** A green badge, a "Success" chip, and a worker's own claim are a system reporting on itself. Read the real DB row, the raw API response, the file on disk before claiming anything passed.
- **Never fake success.** No demo data pretending to be real, no log-display elisions, no hardcoded "it works" paths. If it's fake, remove it or label it.
- **Don't hand over anything you haven't verified yourself first** (creds round-tripped, UI actually driven and screenshotted).

## Working style
- **Multi-agent aggressively** — fan-out, tournaments, skeptics, completeness critics (see orchestration-patterns.md). Floor, not ceiling.
- **Never ask James mid-run.** Decide with research + reasoning, log question/answer/why in the Decision Log.
- **Blocking is not an option.** Another route, or the strong 80% with what-got-cut noted.
- **Root cause, not patches.** Never the same failure twice.
- **Commit every green step** with clear messages; never commit `.env`.
- **Simple beats clever.** The most straightforward approach that works; complexity can come later.
- **End every run with the morning report** and, for major runs, a session-handoff note to the vault.
