---
name: onboarding
description: >-
  Use on first run of this system, or whenever setup is incomplete or the
  user wants to (re)configure it. Runs a structured, resumable interview
  across 13 modules — identity, goals, voice, values, work domains, health,
  finance, agent roster, folder organization, cost/model routing, and
  autonomy boundaries — and writes the answers directly into the live
  system files (~/.claude/CLAUDE.md, ~/.claude/me/*.md, the Dashboard, and
  the constitution folder). Disk-persisted state means it can be paused and
  resumed across sessions without losing progress.
---

# Onboarding

This is how a brand-new copy of this system becomes *yours*. It's a
structured interview, not a form — each module builds real understanding
before writing anything down, and every module's output is a real file the
system will actually consult afterward, not documentation nobody re-reads.

**Read `{{KIT_ROOT}}/docs/ARCHITECTURE.md` once before running this the
first time** if you want the full picture of what gets built where; you
don't need it to proceed, this file is self-contained.

## When to activate

- First run of this system — `home` detects an empty or missing dossier and
  routes here automatically.
- The user explicitly asks to (re)configure, or to run a specific module
  again (values/voice/goals drift over time — re-running a single module
  later is normal, not a failure of the first pass).
- Setup was started and abandoned — resume from where it stopped.

## Session start protocol

On every activation, before asking any interview question:

1. **Check for prior progress first.** State lives at a fixed, always-
   discoverable path: `~/.claude/_onboarding/state.json` — not under the
   system home, deliberately, because `systemHome` itself doesn't exist
   until Module 00 answers it, and progress must be findable before that.
   If the file exists, read it (and the current module's raw file under
   `~/.claude/_onboarding/raw/{module}.md`, if one is in progress).
   **Report in two or three sentences:** which module is in progress or
   next, and what's already done. Then ask: "Continue here, or jump to a
   different module?" If it doesn't exist, this is a fresh start.
2. **Locate the kit's own template source (`{{KIT_ROOT}}`).** If
   `state.json` already has `kitRoot` recorded (from a prior run), use
   that and skip straight to Module 00 (or wherever `nextModule` points).
   Otherwise, this is needed before Module 00 can finish: installing the
   plugin only installs `plugins/assistant/` (this skill, the other
   skills, the agents, the hooks) — it does **not** install the repo's
   `me/`, `constitution/`, `bootstrap/`, `docs/`, or `Dashboard.md`, which
   live at the kit's repo root instead, and are needed as copy *sources*
   throughout this interview. Try to self-locate first: this very file
   lives at `plugins/assistant/skills/onboarding/SKILL.md` relative to
   the kit's repo root, so walking up four directories from this file's
   own path should land on the repo root — check whether that resolved
   path contains a real `me/` subfolder. If it does, that's
   `{{KIT_ROOT}}`, and write it to `state.json` immediately (a fresh
   `state.json` if none existed yet — don't wait for Module 00 to
   "complete" to persist this). If self-location fails (the install
   mechanism didn't expose that path, or the files were moved), ask
   directly: "Where did you put this kit's own files — wherever you
   cloned or unzipped `second-brain-starter`?" and record the answer the
   same way, immediately, so this is never asked twice.

   **Every `me/*.md`, `constitution/*.md`, `bootstrap/CLAUDE.md`,
   `docs/*.md`, or `Dashboard.md` reference anywhere in this skill (this
   file and every file under `reference/`) that describes a *source* to
   copy or generate from means the path under `{{KIT_ROOT}}`** —
   `{{KIT_ROOT}}/me/*.md`, `{{KIT_ROOT}}/constitution/*.md`,
   `{{KIT_ROOT}}/bootstrap/CLAUDE.md`, `{{KIT_ROOT}}/docs/*.md`,
   `{{KIT_ROOT}}/Dashboard.md` — never a path inside the installed
   plugin, which contains none of them.

## Interview discipline

Apply throughout every module:

1. **One question at a time.** Never present a list of questions at once —
   the module reference files list many topics; work through them
   conversationally, not as a checklist read aloud.
2. **After each answer:** a short paraphrase, then one deepening probe, or
   close the thread if it's already concrete and complete. Never move on
   silently without acknowledging the answer.
3. **Laddering for anything goal- or value-shaped:** follow a "what" answer
   with "why does that matter to you?" — typically two to three iterations
   before a real reason (not a surface restatement) surfaces.
4. **Detect thin answers.** Generic, jargon-heavy, or vague answers get one
   follow-up asking for a concrete example or specific number, not a pass.
5. **Saturation signal:** when two consecutive probes produce no new
   information, summarize and close the module — don't manufacture more
   questions past that point.
6. **Every module is skippable.** Some (Finance especially — see Module 70)
   should be flagged as skippable *before* asking anything. A skip is a
   complete, valid outcome — write a clearly-marked placeholder, move on,
   never treat a skip as a failure to revisit unprompted.
7. **End of module — two writes, not one:**
   - Append the verbatim exchange to `~/.claude/_onboarding/raw/{module}.md`
     (the `## Raw` record — useful if a later re-run needs the original
     context).
   - Write the synthesized result **directly into the real destination
     file** (e.g. `~/.claude/me/goals.md`) — replacing the `<!-- -->`
     instructional comments in that file's template with real content,
     preserving the section structure. This is the important difference
     from a typical "produces a document" interview: the destination file
     *is* the product, not a separate summary of it.
   - Update `~/.claude/_onboarding/state.json` (schema below).
   - Confirm: **"Module {N} saved. Next: {module}. Continue now, or pick
     this up next session?"**

## Safety by default — this isn't waiting on Module 110

The system is **not** unsafe before the interview finishes. The moment
Module 00 completes (so `kitRoot`, `systemName`, and `systemHome` are all
known), do two copies — both idempotent: skip any file that already
exists at the destination, so a resumed session never overwrites real
progress from an earlier run.

1. **Copy `{{KIT_ROOT}}/me/*.md`** (10 blank dossier files) into
   `~/.claude/me/`, for any that aren't already there. Module 10 onward
   assumes these already exist with their template structure — without
   this step they never would.
2. **Copy the entire `{{KIT_ROOT}}/constitution/` folder**, every file,
   unmodified, into `{{SYSTEM_HOME}}/{{SYSTEM_NAME}}/`.

Conservative universal defaults (money and credentials permanently 🔴,
deletions 🟠, anything reaching another person 🟡) are already active the
moment copy 2 lands. Module 110 lets the user *adjust* from that safe
baseline later; it is not the sole source of safety, and a half-finished
interview should never leave a gap where nothing is governing autonomy.

**This instantiation also fixes where later modules write.** Every
`constitution/X.md` reference anywhere below — in this file, in the module
table, in the reference files themselves — means the **live instantiated
copy** at `{{SYSTEM_HOME}}/{{SYSTEM_NAME}}/X.md`, never the kit's own
read-only source template. That copy exists from the moment Module 00
completes, so Modules 40/60/100/110 always have a real file to edit, and
Module 999 never needs to (and must never) re-copy the pristine kit
source over it later — that would silently destroy whatever those modules
already wrote. See Module 999's completeness check for how this plays out
when modules are skipped or run out of order.

## Module sequence

| # | Module | Reference | Writes to |
|---|---|---|---|
| 00 | Orientation | `reference/00_orientation.md` | identity constants, `state.json` |
| 10 | Identity & Profile | `reference/10_identity-profile.md` | `me/profile.md` |
| 20 | Goals & Priorities | `reference/20_goals-priorities.md` | `me/goals.md` |
| 30 | Voice & Communication | `reference/30_voice-communication.md` | `me/voice.md` |
| 40 | Values & Principles | `reference/40_values-principles.md` | `me/values.md`, optionally `constitution/Ethos.md`, optionally `constitution/Constitution.md`'s mission line |
| 50 | Work & Project Domains | `reference/50_work-domains.md` | `me/projects.md`, seeds folder-map, sensitive-data categories for `CLAUDE.md` rule 9 |
| 60 | Health & Sustainable Pace | `reference/60_health-pace.md` | `me/health.md`, `constitution/The-Rhythm.md` |
| 70 | Finance *(flag as skippable first)* | `reference/70_finance.md` | `me/finance.md` |
| 80 | Agent Roster | `reference/80_agent-roster.md` | `me/agents-guide.md`, new agents at `~/.claude/agents/*.md` |
| 90 | Folder & File Organization | `reference/90_folder-organization.md` | `me/folder-map.md` |
| 100 | Cost & Model Routing | `reference/100_cost-model-routing.md` | `constitution/Dispatch.md`, `constitution/The-Stack.md` |
| 110 | Autonomy & Trust | `reference/110_autonomy-trust.md` | `constitution/Autonomy-Ladder.md`, `constitution/Constitution.md` |
| 999 | Assembly (not Q&A) | `reference/999_assembly.md` | `~/.claude/CLAUDE.md`, `Dashboard.md`, a final token sweep, completion report |

Complete modules in order by default; honor a request to jump modules and
note the skip in `state.json`. Module 999 checks which modules are actually
done (not just "not explicitly skipped") before generating the final
`CLAUDE.md` and Dashboard.

## State write protocol

`~/.claude/_onboarding/state.json`:

```json
{
  "kitRoot": null,
  "systemName": null,
  "systemHome": null,
  "yourName": null,
  "yourEmail": null,
  "sensitiveDataCategories": null,
  "completedModules": [],
  "skippedModules": [],
  "inProgressModule": "00_orientation",
  "nextModule": "10_identity-profile",
  "lastUpdated": null
}
```

`sensitiveDataCategories` is written by Module 50 (feeds `CLAUDE.md` rule
9 at Module 999) — any field a module introduces along the way belongs in
this schema too; don't let a reference file invent a `state.json` field
this section doesn't document.

`kitRoot` is written the moment step 2 of the session-start protocol
resolves it — before Module 00's questions even begin — precisely because
`state.json` now lives at a fixed path (`~/.claude/_onboarding/`) that
doesn't depend on `systemHome` being known yet. `yourEmail` is written the
moment Module 00 captures it, same as `yourName`.

Update `completedModules`, `skippedModules`, `inProgressModule`,
`nextModule`, and `lastUpdated` after every module. On the terminal module
(999), set `inProgressModule` to `null` once assembly is written —
leaving it populated would make a future resumption treat a finished setup
as still in progress.

## Anti-patterns

- **Starting without reading state first.** Skipping this loses continuity
  and risks silently overwriting a module already completed.
- **Asking multiple questions at once.** Lists produce checklist answers,
  not real ones.
- **Writing only the Raw record and not the real destination file.** The
  destination file is the actual product — a module that only produces a
  raw transcript hasn't done its job.
- **Treating a skip as incomplete.** A deliberately skipped module (Finance
  especially) is a valid, complete outcome. Don't re-raise it unprompted.
- **Silently clobbering an existing `~/.claude/CLAUDE.md`.** If one already
  exists when Module 999 runs, offer to merge or append — never overwrite
  without asking (Constitution Article 6, once the constitution is live).
- **Auto-renaming plugin/skill slugs.** The default slugs (`assistant`,
  `home`, `onboarding`, `writer`, `researcher`) work correctly unrenamed
  forever. Renaming folders, manifests, and git history from inside a
  first-run session is real blast radius for zero functional benefit — see
  `{{KIT_ROOT}}/docs/ARCHITECTURE.md` if the user wants to do this later,
  by hand.
- **Leaving `{{PLACEHOLDER}}` tokens unresolved in generated files.**
  Module 999's final sweep step exists specifically to catch these —
  don't skip it, and don't invent a value for a token whose owning module
  was skipped; report it instead.

## Related files

- `constitution/BOOTSTRAP.md` / `HARVEST.md` — the same disk-persisted,
  resumable philosophy applied to ordinary dispatched sessions, not just
  onboarding.
- `{{KIT_ROOT}}/docs/ARCHITECTURE.md` — the full picture of what this kit
  builds and why.
