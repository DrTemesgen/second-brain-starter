---
name: verify
description: >-
  Health-check for this system's own setup — confirms the dossier,
  CLAUDE.md, Dashboard, and constitution folder are actually well-formed,
  with no leftover {{PLACEHOLDER}} tokens outside the few files where
  that's correct by design. Use when something seems off, after manually
  editing any of these files, or any time onboarding is re-run and you
  want confidence nothing broke.
---

# Verify

A read-only diagnostic, not a repair tool — it tells you what's wrong (or
confirms nothing is), it doesn't fix anything itself. Safe to run any
time, as often as you want; it never writes to disk.

This exists because Module 999's own token sweep only runs once, at the
end of a possibly multi-session interview, and there was previously no
way to just check current state without re-running the whole of Assembly
(which is a heavier operation — see `{{KIT_ROOT}}/docs/ARCHITECTURE.md`
if curious why Assembly is safe to re-run but still isn't the same thing
as a quick check).

## What to check, and how to read the result

1. **Find the system home.** Read `~/.claude/CLAUDE.md` rule 12
   (Routing) for `{{SYSTEM_HOME}}` and rule 3 (Autonomy boundary) for
   `{{SYSTEM_NAME}}`/where the constitution folder lives. If `CLAUDE.md`
   doesn't exist at all, stop here and say so — onboarding hasn't
   produced anything yet, this isn't a "broken" state, just a "not
   started" one.

2. **Confirm the constitution folder is actually there**, at
   `{{SYSTEM_HOME}}/{{SYSTEM_NAME}}/`, with the expected files:
   `Constitution.md`, `Autonomy-Ladder.md`, `The-Rhythm.md`,
   `BOOTSTRAP.md`, `HARVEST.md`, `Session-Sync-Log.md`, `The-Stack.md`,
   `Cost-Control-Guide.md`, `Ethos.md`, `People/`. Report any missing.

3. **Confirm the dossier is complete.** All 10 files listed in
   `CLAUDE.md`'s "My dossier" table should exist under `~/.claude/me/`.

4. **Sweep for unresolved `{{...}}` tokens** — but with the same
   exclusions Module 999's own sweep uses, since these are correct by
   design, not bugs:
   - `~/.claude/me/feedback.md`'s entry-format template — its tokens are
     permanent, meant for future entries, never resolved.
   - `{{SYSTEM_HOME}}/{{SYSTEM_NAME}}/People/*.md` — permanent stencils,
     same reason.
   - Any token in `The-Rhythm.md`, `Dispatch.md`, or `The-Stack.md` whose
     owning module (60, 100) was recorded as skipped in `state.json` —
     those are deliberately left, not broken.

   Anywhere else, a real `{{...}}` token is a genuine finding — report
   the file, the token, and which module should own it (cross-reference
   `SKILL.md`'s module table in the `onboarding` skill if unsure).

5. **Read `~/.claude/_onboarding/state.json`** if it exists, and report:
   which modules are completed, which skipped, whether `inProgressModule`
   is still non-null (meaning onboarding thinks it's mid-way, even if
   everything above looks fine — worth flagging as a mismatch if so).

## Reporting the result

A few lines, not a wall of text — this mirrors `home`'s own reporting
style:

- Everything clean: say so plainly, don't manufacture caveats.
- Something's off: list exactly what and where, and name which
  `onboarding` module would fix it (e.g. "re-run Module 40 to resolve
  `{{YOUR_MISSION}}` in `Constitution.md`, or tell me to just delete that
  line if you don't want a mission statement").
- Never silently fix anything found here — that's what re-running the
  relevant `onboarding` module is for. This skill only reports.
