# Module 999 — Assembly

Not an interview module — this is where everything the previous modules
wrote gets put together into a working system. Run it once modules 00-110
are done or deliberately skipped.

## Steps

1. **Check completeness.** Read `~/.claude/_onboarding/state.json` —
   confirm every module is either in `completedModules` or
   `skippedModules`. If something's missing, say so and offer to finish
   it now or proceed with what's there (proceeding is fine; nothing here
   is strictly required for the system to function, since Module 00's
   safety defaults have been active the whole time).

2. **Generate the real `~/.claude/CLAUDE.md`** from
   `{{KIT_ROOT}}/bootstrap/CLAUDE.md` (the kit's source template) +
   everything captured across modules:
   - `{{YOUR_NAME}}` and `{{ONE_PARAGRAPH_BIO}}` in the "About the user"
     header — the bio isn't asked as its own question; synthesize it from
     `me/profile.md` (name, credentials, current role) once that's filled.
   - `{{YOUR_EMAIL}}` in the standalone "# userEmail" section at the
     bottom of the file (not one of the numbered rules).
   - `{{SENSITIVE_DATA_CATEGORIES}}` in rule 9, from Module 50 (if that
     module was skipped, use "no specific sensitive-data category
     flagged" rather than leaving the token unresolved).
   - Delete rules 7/8/10 entirely if their owning module was skipped or
     declined (each rule's own comment says which).

   **Check for an existing file first** — if `~/.claude/CLAUDE.md`
   already exists (a returning user re-running onboarding, or a file
   that predates this kit), never silently overwrite it. Show a
   diff-style summary of what would change and offer: merge, append a
   new section, or write fresh — the user's choice.

3. **Generate `Dashboard.md`** at `{{SYSTEM_HOME}}/Dashboard.md` from
   `{{KIT_ROOT}}/Dashboard.md` (the kit's source template), with
   `systemName`, `yourName`, and today's date filled in throughout, and
   the conditional "Funding & partnerships" section included only if
   Module 50 flagged that as regular work.

4. **Verify the constitution folder — do not re-copy it.** The entire
   `constitution/` folder was already instantiated into
   `{{SYSTEM_HOME}}/{{SYSTEM_NAME}}/` the moment Module 00 completed (see
   SKILL.md's "Safety by default"), and Modules 40/60/100/110 have been
   editing that live copy directly ever since. **Never copy the kit's own
   `constitution/` source over it here** — the kit source is pristine and
   unmodified; the instantiated copy is where the user's real answers
   live, and overwriting it would silently destroy them. This step is
   just a sanity check: confirm the folder exists with all expected
   files present, and note anything that still shows shipped defaults
   because its module was skipped (that's correct, not a bug).

5. **Sweep for unresolved `{{...}}` tokens across every instantiated
   file** — `~/.claude/CLAUDE.md`, every `~/.claude/me/*.md`,
   `{{SYSTEM_HOME}}/Dashboard.md`, and every file under
   `{{SYSTEM_HOME}}/{{SYSTEM_NAME}}/`. This is the step that makes the
   promise in `docs/SETUP.md` ("check for any remaining `{{PLACEHOLDER}}`
   token") actually true instead of aspirational — earlier steps write
   the big, obvious files, but identity/path tokens embedded deeper in
   `Constitution.md`, `BOOTSTRAP.md`, and `HARVEST.md` (`{{YOUR_NAME}}`,
   `{{SYSTEM_NAME}}`, `{{SYSTEM_HOME}}`, `{{DATE}}`) are easy to miss
   individually. Fill every token you can resolve from `state.json` or
   today's date. **Do not invent a value for anything else** — if a
   token's owning module was skipped (e.g. `{{YOUR_MISSION}}` if Module
   40's optional mission line was never given), remove the token cleanly
   rather than filling it with a guess, and note it in the completion
   report so the user knows it's still open.

6. **Print a complete "what got built, where" summary** — every file
   created or updated, as a full path, plus anything flagged unresolved
   in step 5. Don't make the user go find things.

7. **Suggest a first real dry run** — e.g. "try asking me 'what's next' and
   I'll read your actual Dashboard and goals file" — so the first real
   interaction after setup demonstrates the system working with real
   content, not a hypothetical.

8. **Mention the optional rename** — if they want their own name for the
   system reflected in the actual slash-command slugs (not just the
   Dashboard prose), point them at `{{KIT_ROOT}}/docs/ARCHITECTURE.md`'s
   manual rename steps. Don't do this automatically — see the SKILL.md
   anti-patterns section for why.

## Final state update

Set `inProgressModule` to `null` in `~/.claude/_onboarding/state.json`
once this is done — leaving it populated would make a future resumption
treat a finished setup as still in progress.

## Close

"{{SYSTEM_NAME}} is set up. Here's everything that got built: [full path
list]. Try it out, or come back to any module anytime to adjust it — this
isn't a one-time interview, it's meant to stay current."
