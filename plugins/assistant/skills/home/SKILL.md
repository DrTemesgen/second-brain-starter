---
name: home
description: >-
  The front door. Use when the user opens a session and wants to know
  what's next, asks a general "what am I working on" question, wants to
  register or remember something, or opens this system without a specific
  task in mind. Detects first-run (no dossier yet) and routes to onboarding
  automatically.
---

# Home

This is the entry point — what runs when there's no specific task yet, just
"tell me what's going on."

## First-run / in-progress detection

Check in this order — don't rely on dossier content alone, since a
partially-completed onboarding can look empty at a glance:

1. **Check `~/.claude/_onboarding/state.json` first.** This is a fixed
   path, always discoverable, independent of whether onboarding ever
   finished. If it exists and `inProgressModule` is non-null:

   > Looks like setup is mid-way — you'd completed [N] module(s), currently
   > on [module]. Want to pick up where you left off?

   Route to `onboarding` if yes. **Don't fall through to step 2** — a
   dossier with some files filled and others still template-only is not a
   fresh install, it's this state.

2. **If `state.json` doesn't exist at all,** check whether
   `~/.claude/me/goals.md` has real content past its shipped `<!-- -->`
   comments. If it doesn't:

   > This looks like a fresh install — nothing's been customized yet. Want
   > to run onboarding now? It's a guided interview, takes it one step at
   > a time, and you can pause and resume anytime. (Or, if you'd rather
   > explore the files first, that's fine too — say so and I'll hold off.)

   Route to `onboarding` if yes. Don't force it — some people want to look
   around first.

## Normal operation (dossier already populated)

1. **Read `Dashboard.md`** at the system home — this is the actual state of
   things, kept current by prior sessions. (The system home's path isn't
   knowable in the abstract — read it from `~/.claude/CLAUDE.md` rule 12
   (Routing), which onboarding's Assembly step resolves to a real path.
   Rule numbers are stable even when some rules are absent — Assembly
   never renumbers the surviving ones.)
2. **Read `me/goals.md`** — flag anything in the live-deadlines table
   that's close, per whatever session-start behavior was set in onboarding
   Module 20 (some users want this, some explicitly don't — respect what
   was set).
3. **If `~/.claude/CLAUDE.md` rule 7 (Wellbeing guardian) is present**,
   also glance at `The-Rhythm.md` in the constitution folder — this is
   the only point in an ordinary session where that file actually gets
   read, so it's what makes rule 7 more than a standing intention. Flag
   per that file's own rules (once, briefly, never twice in one session).
4. **Report in a few lines**, not a wall of text: what's next, anything
   urgent, anything waiting in the approval queue (`Dashboard.md`'s
   "Envelope" section).
5. **Handle the actual request** — "remember this" goes to the relevant
   `me/*.md` file or `me/feedback.md`; "add to my dashboard" edits
   `Dashboard.md` directly; a specific task gets picked up per the
   constitution folder's `Dispatch.md` — find that folder the same way,
   via `~/.claude/CLAUDE.md` rule 3 (Autonomy boundary), not by guessing a
   relative path.

## What this skill is not

Not a place to do the actual work — it orients, routes, and hands off. A
genuinely substantive task should follow `Dispatch.md`'s ritual (clarify →
propose model/tool → do the work, or dispatch it), not happen inline inside
a "what's next" check-in.
