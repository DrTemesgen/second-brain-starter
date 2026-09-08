# Module 100 — Cost & Model Routing

Writes `constitution/Dispatch.md`'s routing table and
`constitution/The-Stack.md`. Directly implements what `Cost-Control-Guide.md`
already explains — this module is where the guide becomes the user's
actual configured defaults rather than just advice read once.

## Topics to cover

- **What AI tools/subscriptions does the user already have?** Claude plan
  tier, any other assistants or model access, local/offline model
  capability if applicable. This becomes the real rows in `The-Stack.md`
  — delete the example rows shipped in that file and replace with their
  actual toolkit.
- **Model-tier routing preference** — introduce the golden rule from
  `Cost-Control-Guide.md` (cheapest tier that does the job) as the
  recommended default, and confirm they're on board with escalating only
  per-session, on purpose, with a stated reason. Fill `{{DEFAULT_MODEL}}`
  in `Dispatch.md`'s routing table with whatever their actual default tier
  is.
- **Interest in local models** — optional; skip cleanly if they don't have
  the hardware or interest. Don't push this.
- **Default reviewer preference** — for genuinely high-stakes work (money,
  legal, external-facing, hard to reverse), do they want a review offered
  automatically, or only on request? This feeds how `Dispatch.md`'s "offer
  a reviewer sized to the risk" line actually behaves for them.
- **Session-hygiene buy-in** — briefly confirm the one-task-one-session
  habit from Constitution Article 8 makes sense to them; this is more a
  confirmation than a real branching decision, most people agree once it's
  explained with the cost formula from `Cost-Control-Guide.md`.

## What gets written

Both in the **instantiated** copies at `{{SYSTEM_HOME}}/{{SYSTEM_NAME}}/`
(created at Module 00, not the kit's own source files). Fill
`{{DEFAULT_MODEL}}` throughout `Dispatch.md`'s routing table. Replace
`The-Stack.md`'s example rows with their real toolkit — delete rows for
tools they don't have rather than leaving them as dead examples.

## Close

"Module 100 saved. Next: Autonomy & Trust — the last real interview
module. Continue now, or pick this up next session?"
