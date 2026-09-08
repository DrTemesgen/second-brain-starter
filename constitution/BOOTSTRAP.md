# BOOTSTRAP — how a fresh session becomes part of this system

<!-- This is a ritual, not code — a fixed prompt you (or a session you've
     dispatched) paste at the start of a new Claude Code session to bring it
     up to speed on everything that matters, fast, without re-explaining it
     from scratch every time. Mechanism ported near-verbatim from the
     original design; only the identity/path placeholders are yours to
     fill. -->

## When to use this

- You're opening a brand-new session for a task dispatched from your main
  session (see `Dispatch.md`).
- A session got interrupted (crash, closed terminal) and needs to
  reconstitute context fast.
- You're handing a task to someone else's session, or a subagent, that
  needs the same operating rules you do.

## The bootstrap prompt

Paste this (or a close paraphrase) at the start of the new session:

> You're picking up work inside {{SYSTEM_NAME}}, a personal Claude Code
> system. Before doing anything else:
>
> 1. Read `~/.claude/CLAUDE.md` — the always-on operating rules.
> 2. Read `{{SYSTEM_HOME}}/{{SystemName}}/Constitution.md` — the guardrails
>    that govern everything else here. Follow them without exception.
> 3. Read `{{SYSTEM_HOME}}/Dashboard.md` — what's currently in flight, so
>    you don't duplicate work or contradict a decision already made.
> 4. Check `~/.claude/me/` for anything relevant to the task you're about
>    to do (goals, projects, voice, values — whichever applies).
> 5. Confirm you understand: draft-only for anything reaching another
>    person, confirm-first before destructive or bulk changes, never for
>    money or credentials — per `Autonomy-Ladder.md`.
> 6. Append one line to `Session-Sync-Log.md` noting you've started this
>    task, what it is, and roughly when you expect to check back in.
> 7. Give me one line back: "Linked. Working on: [task]." Then begin.

## Why this exists

Multi-session work (see `Dispatch.md`) only stays coherent if every session
that touches it starts from the same footing. Skipping bootstrap is how a
dispatched session quietly reinvents a decision the main session already
made, or breaks a guardrail nobody told it about — not through carelessness,
just through not knowing. Thirty seconds of reading here is cheaper than the
rework later.

---

*Companion ritual: `HARVEST.md` (how a session hands its results back).*
