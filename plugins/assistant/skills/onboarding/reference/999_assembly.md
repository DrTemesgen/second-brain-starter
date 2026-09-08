# Module 999 — Assembly

Not an interview module — this is where everything the previous modules
wrote gets put together into a working system. Run it once modules 00-110
are done or deliberately skipped. **Safe to re-run** — every step below
either checks for an existing file first or is read-only; re-running
Assembly must never be the thing that destroys a day's real Dashboard
edits or a live constitution answer.

## Steps

1. **Check completeness.** Read `~/.claude/_onboarding/state.json` —
   confirm every module is either in `completedModules` or
   `skippedModules`. If something's missing, say so and offer to finish
   it now or proceed with what's there (proceeding is fine; nothing here
   is strictly required for the system to function, since Module 00's
   safety defaults have been active the whole time). For each of Modules
   20, 60, and 70 specifically, *completed* is not the same as *opted
   in* — check whether the actual answer was a decline before treating
   its feature as active: `me/goals.md`'s Learning ritual section says
   "opted out" or a real subject; `me/health.md` has either the short
   opt-out note or full content; `me/finance.md` is either the unchanged
   shipped placeholder or filled in. Use these, not `completedModules`
   alone, to decide whether `CLAUDE.md` rules 7/8/10 apply.

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
   - Delete rules 7/8/10 entirely if step 1 found their feature declined
     or their module skipped (each rule's own comment says which).
     **Keep every surviving rule's original number — do not renumber the
     list.** Several other files address a rule by number (`home/SKILL.md`
     cites rule 12 for routing, `The-Rhythm.md` cites rule 7), and a
     renumbered list breaks every one of them silently. A gap in the
     sequence (rules 1-6, 9, 11-13) is completely fine and expected.

   **Check for an existing file first** — if `~/.claude/CLAUDE.md`
   already exists (a returning user re-running onboarding, or a file
   that predates this kit), never silently overwrite it. Show a
   diff-style summary of what would change and offer: merge, append a
   new section, or write fresh — the user's choice.

3. **Generate `Dashboard.md`** at `{{SYSTEM_HOME}}/Dashboard.md` from
   `{{KIT_ROOT}}/Dashboard.md` (the kit's source template), with
   `systemName`, `yourName`, and today's date filled in throughout, and
   the conditional "Funding & partnerships" section included only if
   Module 50's `seeksFunding` answer (in `state.json`) was yes.
   **Check for an existing file here too, exactly like step 2** — a
   second onboarding run (adjusting an earlier module, or a user who
   re-runs Assembly after Module 999's own sweep flags something) must
   never silently regenerate a `Dashboard.md` that already has real
   "Recent days," an Envelope queue, or live deadlines in it. If one
   exists, offer merge/append/leave-alone, same choices as step 2 — never
   a blind overwrite.

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

5. **Sweep for unresolved `{{...}}` tokens — narrowly, not everywhere.**
   Scope this to exactly: `~/.claude/CLAUDE.md`, `{{SYSTEM_HOME}}/Dashboard.md`,
   and — inside `{{SYSTEM_HOME}}/{{SYSTEM_NAME}}/` — only
   `Constitution.md`, `BOOTSTRAP.md`, and `HARVEST.md` (their
   `{{YOUR_NAME}}`, `{{SYSTEM_NAME}}`, `{{SYSTEM_HOME}}`, `{{DATE}}`,
   `{{YOUR_MISSION}}` tokens are the ones easy to miss individually, and
   these three are the only constitution files with no other owning
   module). Fill every token you can resolve from `state.json` or
   today's date; if `{{YOUR_MISSION}}` was never given, remove it cleanly
   rather than guessing.

   **Do not sweep, and do not touch, any of these — each has its own
   correct handling elsewhere, and a generic sweep would corrupt them:**
   - `me/feedback.md` — its `{{DATE}}` / `{{LOVE / AVOID / TREND / RULE}}`
     tokens are a permanent entry-format template for future log entries,
     not a value to fill in now. No module ever writes this file at
     initial setup; that's correct, not incomplete.
   - `constitution/People/*.md` — permanent stencils meant to be copied
     per-person later, per their own `_README.md`. Never resolve or
     strip their tokens.
   - Any `{{...}}` token in a constitution file whose owning module
     (60, 100) was skipped or left it deliberately — e.g. `The-Rhythm.md`
     if Module 60 declined, or `Dispatch.md`'s `{{DEFAULT_MODEL}}` /
     `The-Stack.md`'s example-tool tokens if Module 100 was skipped. Each
     of those modules already gives the correct instruction for its own
     tokens ("leave the placeholder tokens in place" for The-Rhythm,
     "delete rows for tools they don't have" for The-Stack) — defer to
     that, don't overrule it with a blanket strip-or-fill pass. Note
     these in the completion report as "still open, from a skipped
     module" rather than resolving them yourself.

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
