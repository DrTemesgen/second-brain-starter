# Module 80 — Agent Roster

Writes `me/agents-guide.md`, and optionally scaffolds new agent `.md`
files into `~/.claude/agents/` — **not** `plugins/assistant/agents/`
inside the kit. That folder is the *installed plugin's own* agents;
Claude Code loads agents from `~/.claude/agents/` (or a project's own
`.claude/agents/`), and a new agent written into the plugin's installed
copy would vanish on the next plugin update and never actually load in
the meantime. `~/.claude/agents/` needs no reinstall and is the user's
own, durable to edit. This module builds the user's roster live — it does
not offer a pre-built menu of specialist agents to pick from.

## Why this module doesn't just offer a menu

Genericized versions of narrow specialist agents (a curriculum-builder with
no curriculum, an institution-ops agent with no institution) are dead
weight in every session's context whether or not they're ever used. A
roster built from what Module 50 actually surfaced as real recurring work
is more useful than any generic menu could be — and it's genuinely how
this whole system's own roster was built the first time, for whoever this
kit is descended from.

## Topics to cover

- **Revisit what Module 50 surfaced** as recurring work types. Ask
  directly: "Of the kinds of work you do again and again, which ones would
  genuinely benefit from a specialist that already knows the context, vs.
  just asking the main session each time?"
- For each candidate agent: **what does it own** (its scope — be specific,
  not "handles marketing" but "drafts and tracks outreach to X kind of
  contact"), and **when should it fire** (the trigger — a phrase, a
  situation, a kind of request).
- **Start small.** 2-4 custom agents is a reasonable starting roster, not a
  ceiling — more can be added later once a real repeated need shows up
  three-plus times (see the growth rule).
- **Already-shipped agents** (`writer`, `researcher`) — check whether any
  candidate would just duplicate one of these; if so, that's not a new
  agent, it's confirmation the shipped one covers it.
- **Growth rule** — confirm or adjust the default: add an agent once a
  specific kind of help has been asked for repeatedly (three-plus times is
  a reasonable bar); retire one that's gone unused for a long stretch
  rather than letting the roster grow indefinitely.

## What gets written

Fill `me/agents-guide.md`'s roster table with whatever was actually agreed
on — including a legitimate "none yet, starting with just `writer` and
`researcher`" as a complete, valid outcome. Only create new files under
`~/.claude/agents/` for agents that were actually specified with a real
scope and trigger — never scaffold a placeholder agent nobody asked for.

## Close

"Module 80 saved. Next: Folder & File Organization. Continue now, or pick
this up next session?"
