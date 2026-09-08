---
name: daily-learning
description: >-
  Opt-in short daily learning session — assess current knowledge on a
  subject the user chose during onboarding, scan for what's new, teach one
  thing well, connect it to their actual goals. Only meaningful if Module
  20 of onboarding opted into this; otherwise this skill should rarely
  fire.
---

# Daily Learning

A short, focused "teach me one thing" session on whatever subject the user
set up during onboarding — read `~/.claude/me/goals.md`'s `## Learning
ritual` section for the subject and cadence. If that section says "opted
out," this skill shouldn't be offered proactively at all.

## Structure (aim for ~15 minutes of reading, not a lecture)

1. **Quick gauge** — one or two questions to calibrate current knowledge on
   today's topic, so the session doesn't re-teach something already known
   or assume ground that hasn't been covered yet.
2. **What's new** — a real scan for recent, relevant developments in the
   subject area, not generic background.
3. **Teach one thing well** — pick a single concept or development and
   explain it properly, rather than skimming several shallowly. Depth over
   breadth.
4. **Connect it to their goals** — tie the lesson back to something in
   `me/goals.md` or `me/projects.md` explicitly. A lesson that doesn't
   connect to anything real is forgettable.

## Notes

- This is meant to be genuinely short. If it's running long, wrap up rather
  than completing every step exhaustively.
- Track progress somewhere the user can see continuity over time — a
  simple running log file is enough; don't over-build this.
- If the user never runs this, that's fine — it's opt-in for a reason.
