# Module 00 — Orientation

The shortest module, and the only one that has to run first — everything
else assumes these answers exist.

## Topics to cover

1. **What should this system be called?** Not "assistant" — their own name
   for it, not a name inherited from wherever this kit came from. Explain
   briefly why this matters: it's not cosmetic, it's the difference
   between inheriting someone else's system and actually owning this one.
   If they want to think about it, a placeholder is fine — this can change
   later by editing `Dashboard.md` and `bootstrap`-derived `CLAUDE.md`.
2. **Where should it live day-to-day?** A working folder they open and
   talk to — e.g. `~/SecondBrain` or a similarly plain path. Doesn't need
   to be named anything in particular; just needs a real path. This
   becomes `{{SYSTEM_HOME}}` everywhere else in the kit.
3. **Their name**, and how they want to be addressed (full name for formal
   contexts, a short form for everyday use).
4. **Their email** — used only for plugin/manifest authorship fields,
   never sent anywhere. Say this explicitly; it's a reasonable thing to be
   cautious about.
5. **Confirm locality.** State plainly: everything from here on stays on
   their machine, in files they own, unless they explicitly ask to send
   something somewhere. This is Constitution Article 5 — worth saying out
   loud once at the very start, not just leaving it implicit in a file
   they may not read yet.

## What gets written

- `systemName`, `systemHome`, `yourName` in `state.json`.
- These seed the identity block of the real `~/.claude/CLAUDE.md` that
  Module 999 (Assembly) will generate — don't write `CLAUDE.md` itself
  yet, just capture the answers.

## Close

One line: "Got it — building `{{systemName}}` at `{{systemHome}}`. Next:
your profile." Move to Module 10.
