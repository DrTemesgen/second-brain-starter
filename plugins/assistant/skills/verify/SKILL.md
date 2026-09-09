---
name: verify
description: >-
  Health-check for this system's own setup — confirms CLAUDE.md, the
  dossier, the Dashboard, and the constitution folder are all present and
  well-formed, with no leftover {{PLACEHOLDER}} tokens outside the few
  places where that's correct by design. Use when something seems off,
  after manually editing any of those files, or any time onboarding is
  re-run and you want confidence nothing broke.
---

# Verify

A read-only diagnostic, not a repair tool — it tells you what's wrong (or
confirms nothing is), it doesn't fix anything itself. Safe to run any
time, as often as you want; nothing in this skill writes to disk.

This exists because the onboarding `Assembly` module's token sweep only
runs at the end of a possibly multi-session interview. There was
previously no way to just *check* current state without re-running
Assembly — which is safe to re-run (it checks for existing files before
touching anything) but is a much heavier operation than a look.

## What to check

**1. Find the system.** Read `~/.claude/CLAUDE.md` — rule 12 (Routing)
names `{{SYSTEM_HOME}}`, rule 3 (Autonomy boundary) names the
constitution folder's full path. If `CLAUDE.md` doesn't exist at all,
stop and say so: onboarding hasn't produced anything yet. That's a "not
started" state, not a broken one.

**2. Confirm the constitution folder** exists at the path rule 3 names,
containing all ten of: `Constitution.md`, `Autonomy-Ladder.md`,
`Dispatch.md`, `The-Rhythm.md`, `BOOTSTRAP.md`, `HARVEST.md`,
`Session-Sync-Log.md`, `The-Stack.md`, `Cost-Control-Guide.md`,
`Ethos.md` — plus the `People/` subfolder. Report anything missing.

**3. Confirm the dossier** — all ten files from `CLAUDE.md`'s "My
dossier" table exist under `~/.claude/me/`.

**4. Confirm the Dashboard** exists at `{{SYSTEM_HOME}}/Dashboard.md`.

**5. Sweep for unresolved `{{...}}` tokens**, using **exactly the scope
defined in the onboarding skill's `reference/999_assembly.md` step 5** —
read it rather than reimplementing it from memory, so the two can't drift
apart. As of this writing that scope is:

- *In scope:* `~/.claude/CLAUDE.md`; every `~/.claude/me/*.md` **except
  `feedback.md`**; `{{SYSTEM_HOME}}/Dashboard.md`; every `*.md` directly
  inside the constitution folder **except the `People/` subfolder**.
- *Never flag:* `me/feedback.md` (permanent entry-format template) and
  `People/*.md` (permanent per-person stencils). Tokens there are correct
  and must stay.
- *Flag as "open, not broken":* tokens whose owning module was skipped
  **or completed-but-declined** — a declined Module 60 is recorded as
  `completed`, not `skipped`, and deliberately leaves `The-Rhythm.md`'s
  tokens in place. Same for `Dispatch.md`/`The-Stack.md` if Module 100
  didn't run. Check the actual recorded answers, not just
  `completedModules`: `me/health.md` holds either an opt-out note or real
  content, `me/finance.md` is either the shipped placeholder or filled
  in, and `me/goals.md`'s "Learning ritual" section says "opted out" or
  names a subject.

Anything else with a live `{{...}}` token is a genuine finding — report
the file, the token, and which module owns it (the onboarding skill's
`SKILL.md` module table maps tokens to modules).

**6. Read `~/.claude/_onboarding/state.json`** if it exists, and report
which modules are completed, which skipped, and whether
`inProgressModule` is still non-null — if it is while everything above
looks complete, that mismatch is worth flagging on its own.

## Reporting

A few lines, not a wall of text — same register as `home`:

- **Clean:** say so plainly. Don't manufacture caveats.
- **Findings:** list exactly what and where, separating *broken* (a real
  missing file or an unresolved token that should have been filled) from
  *open by choice* (a token left behind by a module that was skipped or
  declined — expected, not a defect).
- For each real finding, name the module that would fix it (e.g. "re-run
  Module 40 to set `{{YOUR_MISSION}}` in `Constitution.md`, or say the
  word and I'll just delete that line if you don't want a mission
  statement").
- **Never fix anything found here.** Report, then let the person choose.
  Re-running the owning module is the repair path; this skill is the
  diagnosis.
