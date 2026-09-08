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

## First-run detection

Before doing anything else, check whether `~/.claude/me/goals.md` exists
**and** has real content past its shipped `<!-- -->` comments (an empty
template doesn't count as set up). If it doesn't:

> This looks like a fresh install — nothing's been customized yet. Want to
> run onboarding now? It's a guided interview, takes it one step at a time,
> and you can pause and resume anytime. (Or, if you'd rather explore the
> files first, that's fine too — say so and I'll hold off.)

Route to the `onboarding` skill if they say yes. Don't force it — some
people want to look around first.

## Normal operation (dossier already populated)

1. **Read `Dashboard.md`** at the system home — this is the actual state of
   things, kept current by prior sessions.
2. **Read `me/goals.md`** — flag anything in the live-deadlines table
   that's close, per whatever session-start behavior was set in onboarding
   Module 20 (some users want this, some explicitly don't — respect what
   was set).
3. **Report in a few lines**, not a wall of text: what's next, anything
   urgent, anything waiting in the approval queue (`Dashboard.md`'s
   "Envelope" section).
4. **Handle the actual request** — "remember this" goes to the relevant
   `me/*.md` file or `me/feedback.md`; "add to my dashboard" edits
   `Dashboard.md` directly; a specific task gets picked up per
   `constitution/Dispatch.md`'s routing.

## What this skill is not

Not a place to do the actual work — it orients, routes, and hands off. A
genuinely substantive task should follow `Dispatch.md`'s ritual (clarify →
propose model/tool → do the work, or dispatch it), not happen inline inside
a "what's next" check-in.
