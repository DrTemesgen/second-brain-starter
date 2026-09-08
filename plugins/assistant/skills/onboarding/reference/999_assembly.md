# Module 999 — Assembly

Not an interview module — this is where everything the previous modules
wrote gets put together into a working system. Run it once modules 00-110
are done or deliberately skipped.

## Steps

1. **Check completeness.** Read `state.json` — confirm every module is
   either in `completedModules` or `skippedModules`. If something's
   missing, say so and offer to finish it now or proceed with what's there
   (proceeding is fine; nothing here is strictly required for the system
   to function, since Module 00's safety defaults have been active the
   whole time).

2. **Generate the real `~/.claude/CLAUDE.md`** from `bootstrap/CLAUDE.md` +
   everything captured across modules. **Check for an existing file
   first** — if `~/.claude/CLAUDE.md` already exists (a returning user
   re-running onboarding, or a file that predates this kit), never
   silently overwrite it. Show a diff-style summary of what would change
   and offer: merge, append a new section, or write fresh — the user's
   choice.

3. **Generate `Dashboard.md`** at `{{systemHome}}/Dashboard.md` from the
   kit's template, with `systemName` and `yourName` filled in throughout,
   and the conditional "Funding & partnerships" section included only if
   Module 50 flagged that as regular work.

4. **Instantiate the constitution folder** at
   `{{systemHome}}/{{systemName}}/` — copy every file from `constitution/`
   in the kit, with all modules' answers already written into it from
   their individual module steps (Constitution, Autonomy-Ladder, The-
   Rhythm, Dispatch, The-Stack should already reflect the real answers by
   this point — this step is about placement, not re-writing content).

5. **Print a complete "what got built, where" summary** — every file
   created or updated, as a full path. Don't make the user go find things.

6. **Suggest a first real dry run** — e.g. "try asking me 'what's next' and
   I'll read your actual Dashboard and goals file" — so the first real
   interaction after setup demonstrates the system working with real
   content, not a hypothetical.

7. **Mention the optional rename** — if they want their own name for the
   system reflected in the actual slash-command slugs (not just the
   Dashboard prose), point them at `docs/ARCHITECTURE.md`'s manual rename
   steps. Don't do this automatically — see the SKILL.md anti-patterns
   section for why.

## Final state update

Set `inProgressModule` to `null` in `state.json` once this is done —
leaving it populated would make a future resumption treat a finished setup
as still mid-module.

## Close

"{{systemName}} is set up. Here's everything that got built: [full path
list]. Try it out, or come back to any module anytime to adjust it — this
isn't a one-time interview, it's meant to stay current."
