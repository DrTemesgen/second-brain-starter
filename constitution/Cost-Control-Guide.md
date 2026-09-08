# Cost Control Guide

<!-- This file exists because someone learned these lessons the expensive
     way, so you don't have to. It's not a port of anyone's actual billing
     history — it's the distilled rules that came out of that experience.
     Read it once at setup, then again whenever a bill surprises you. -->

## The one formula that actually matters

**Cost ≈ session lifetime × context size × model tier.**

The instinctive suspects — skills, agents, scheduled automation — are
usually *not* where the money goes. The real driver is almost always a
single long-lived session that keeps re-reading its entire accumulated
history on every turn, at a premium model tier, for days. A session that's
lived three days and re-reads 200K tokens of history on turn 400 costs more
than a hundred fresh, focused, cheap-tier sessions combined. Size and
duration compound; tier just multiplies the result.

## The rules

**1. One task, one session.** Close cleanly at every task boundary and open
fresh for the next one. A session's job is the task in front of it, not
"be the place everything happens." (Constitution Article 8.)

**2. Flag a session that's outlived a day.** If a session is still open the
next calendar day, that's worth noticing and closing, even mid-task — the
accumulated re-read cost is already compounding by then.

**3. Default to the cheapest model tier that does the job.** Escalate
per-session, on purpose, with a stated reason ("this needs deeper
reasoning because X") — then drop back to default afterward. Escalating by
default "just in case it does better" is how a manageable bill becomes a
surprising one. Most work — drafting, organizing, routine coding, research
summarizing — doesn't need the top tier.

**4. Treat a subagent fan-out as a decision, not a reflex.** Each parallel
subagent has its own context cost. Fanning out three agents to explore a
codebase is often worth it; fanning out ten to do what one focused pass
could do is not. Ask "does this genuinely need parallel independent work,"
not "could this be parallelized."

**5. Keep your memory index a title, not a diary.** If you're running a
rolling memory/index file (see `me/` and any session-memory system), each
entry should be one line — a title plus a short hook — with real detail
living in its own topic file. An index that accumulates news directly
becomes a second, duplicate memory system, and eventually hits a read-size
cap and silently truncates. Compact it periodically; verify nothing was
lost when you trim it.

**6. Know your fixed cost floor.** Every session pays a fixed token cost
before any task even starts — system instructions, memory index, installed
agents/skills/commands, any connected integrations. Every installed skill's
description costs context in *every* session whether you use it that day
or not. Audit this occasionally (quarterly is reasonable) rather than
letting installs accumulate unreviewed. Curate to what you actually use;
archive rather than delete what you remove, so it's restorable if you need
it back.

**7. Audit honestly at session close, not defensively.** A brief self-check
— did the spend match the work, did the model tier match the task's actual
complexity — catches drift before it becomes a pattern. The point is
cutting waste, never cutting quality: this is not a rule that should ever
be used to justify skimping on a task that genuinely needs more.

**8. A fix can quietly regress — recheck it.** If you change a default
(model tier, an automation's frequency, what's installed) specifically to
control cost, schedule a later check to confirm it actually held. Defaults
creep back without anyone deciding that on purpose.

## What this guide is *not*

It's not a rule to build cheaply instead of well, and it's not a reason to
refuse a task that genuinely warrants more depth, more review, or a bigger
model. It's a rule against *default* waste — the spend that happens because
nobody was watching, not the spend a hard problem actually deserves.
