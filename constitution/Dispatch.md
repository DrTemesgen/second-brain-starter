# Dispatch — the control tower

<!-- This is the routing doc: how work gets from "an idea you said out loud"
     to "the right model, the right tool, running in the right place" without
     you having to make that call from scratch every time. Your main session
     (wherever you run `/assistant:home`) is the control tower — this file is how it
     thinks about routing. -->

## The loop

1. **You state a task.** Substantive or new work gets clarifying questions
   first — not a token one or two, real ones, each tied to what you're
   actually trying to get done. Low-stakes or purely mechanical work (a
   typo fix, a rename, "what's next") skips straight to doing it.
2. **Dispatch proposes a model + tool + a ready-to-paste launch prompt** —
   see the routing table below. You get to see the recommendation and why,
   not just a fait accompli.
3. **You open wherever that session runs and paste the prompt** (a fresh
   Claude Code session, a subagent, another tool entirely — whatever was
   recommended). It runs `BOOTSTRAP.md` first.
4. **Dispatch logs it** in the Active Work table below.
5. **At session end, you run `HARVEST.md`** and paste the summary back (or
   it lands directly in `Session-Sync-Log.md`).
6. **Dispatch folds the harvest into `Dashboard.md`** and offers a reviewer
   sized to the risk — a one-line suggestion, never a blocking gate. Money,
   legal, external-facing, or hard-to-reverse work gets offered a real
   review; a quick internal script doesn't.

## The routing table

| Kind of work | Model | Where | How to launch |
|---|---|---|---|
| Quick / mechanical (rename, typo, status check) | Cheapest available | Current session | Just do it, no dispatch needed |
| Research / analysis | {{DEFAULT_MODEL}} | Current session or a subagent | Dispatch if it'll run long or fan out wide |
| Writing / drafting | {{DEFAULT_MODEL}} | Current session | Draft-only always — Constitution Art. 4 |
| Build / code | {{DEFAULT_MODEL}}, escalate only if the task genuinely needs it | Fresh session in the project repo | `BOOTSTRAP.md` + the task |
| Planning / architecture | {{DEFAULT_MODEL}} or one tier up | Current session, or a planning-mode pass | State the decision that's actually undecided |
| Review (code, writing, a decision) | Match the reviewer to the risk | A fresh session or subagent, never the session that produced the work | On request, or when risk clearly warrants it — not automatically |
| Orchestration (many parallel subtasks) | {{DEFAULT_MODEL}} directing; subtasks at whatever tier fits each | Main session directs, subagents execute | Only for genuinely parallel, independent work |

<!-- Fill in DEFAULT_MODEL during onboarding Module 100 — whatever your
     current cheapest-good-enough tier is. Add rows for any tool you use
     regularly (see The-Stack.md for a fuller routing table by tool). -->

**The golden rule:** cheapest tier that actually does the job. Escalate on
purpose, with a stated reason, for one session — then drop back down. Escalating
by default because a bigger model "might do better" is exactly the habit
that turns a manageable bill into a surprising one; see
`Cost-Control-Guide.md`.

## Active Work

<!-- A live table, not a log — rows move to "done" and get cleared
     periodically rather than accumulating forever. Rebuild it if it's gone
     stale; a stale tracking table is worse than none. -->

| Task | Model · Tool | Session | Status | Started | Harvested |
|---|---|---|---|---|---|
| *(empty — add a row when you dispatch something)* | | | | | |

## The Watch

<!-- A lightweight self-check for anything with real stakes in flight — not
     a monitoring system, just a habit of asking the same few questions
     periodically instead of assuming silence means "fine." -->

For anything you'd genuinely mind going wrong quietly, check periodically:

- 🟢/🟡/🔴 — Is it still moving, or stalled?
- 🟢/🟡/🔴 — Does the last update match what you expected?
- 🟢/🟡/🔴 — Is anything waiting on you that you haven't noticed?
- 🟢/🟡/🔴 — Has a deadline moved closer without the Dashboard reflecting it?
- 🟢/🟡/🔴 — Would you be surprised if you checked the actual state right now?

A single 🔴 is worth a real look, not just a note-and-move-on.
