# HARVEST — how a session hands its results back

<!-- The pull-out counterpart to BOOTSTRAP.md. Run this at the end of any
     dispatched session so its results actually make it back into the main
     system instead of dying in a closed terminal. Fixed output format on
     purpose — a harvest that's different shape every time is harder to
     fold into the Dashboard at a glance. -->

## When to use this

- A dispatched session (see `Dispatch.md`) has finished its task, or is
  stopping for the day mid-task.
- You want a clean, pasteable summary to bring back to your main session or
  log to `Session-Sync-Log.md`.

## The harvest prompt

Paste this at the end of the session:

> Before we close this session, write a harvest summary in exactly this
> format, nothing extra:
>
> ```
> ## [DATE] · [topic] — [status: done / in progress / blocked]
>
> **Changed:** what actually got built, written, or decided — concretely,
> not "worked on X."
>
> **Decisions & open questions:** anything decided that the main session
> should know about, and anything still unresolved.
>
> **Waiting on me:** anything that needs the person's input, approval, or
> action before this can continue.
>
> **Next:** the concrete next step, if this isn't finished.
>
> **Guardrail flags:** anything that came close to an Autonomy Ladder
> boundary, even if it was handled correctly — worth a second look.
> ```
>
> Paste the finished summary back to me, or append it directly to
> `{{SYSTEM_HOME}}/{{SYSTEM_NAME}}/Session-Sync-Log.md`.

## What the main session does with it

Fold the harvest into `Dashboard.md` — update "What's next," move anything
in "Waiting on me" into the approval queue, add any new live deadline to the
table. A harvest that's read once and never folded in defeats the purpose;
the Dashboard should always reflect the most recent harvest, not last
week's.

---

*Companion ritual: `BOOTSTRAP.md` (how a fresh session links in).*
