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

**Read `docs/ARCHITECTURE.md` once before running this the first time** if
you want the full picture of what gets built where; you don't need it to
proceed, this file is self-contained.

## When to activate

- First run of this system — `home` detects an empty or missing dossier and
  routes here automatically.
- The user explicitly asks to (re)configure, or to run a specific module
  again (values/voice/goals drift over time — re-running a single module
  later is normal, not a failure of the first pass).
- Setup was started and abandoned — resume from where it stopped.

## Session start protocol

On every activation, before asking any interview question:

1. **Check for prior progress.** Look for `_onboarding/state.json` at the
   system home (ask where that is, or infer from `~/.claude/me/` already
   existing, if this isn't the very first run). If none exists, this is a
   fresh start — begin at Module 00.
2. **If state exists, read it and the current module's raw file** (if one
   is in progress) under `_onboarding/raw/`.
3. **Report in two or three sentences:** which module is in progress or
   next, and what's already done. Then ask: "Continue here, or jump to a
   different module?"

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
   - Append the verbatim exchange to `_onboarding/raw/{module}.md` (the
     `## Raw` record — useful if a later re-run needs the original
     context).
   - Write the synthesized result **directly into the real destination
     file** (e.g. `~/.claude/me/goals.md`) — replacing the `<!-- -->`
     instructional comments in that file's template with real content,
     preserving the section structure. This is the important difference
     from a typical "produces a document" interview: the destination file
     *is* the product, not a separate summary of it.
   - Update `_onboarding/state.json` (schema below).
   - Confirm: **"Module {N} saved. Next: {module}. Continue now, or pick
     this up next session?"**

## Safety by default — this isn't waiting on Module 110

The system is **not** unsafe before the interview finishes. The moment
Module 00 completes, copy `constitution/Constitution.md` and
`constitution/Autonomy-Ladder.md` into the system home exactly as shipped —
conservative universal defaults (money and credentials permanently 🔴,
deletions 🟠, anything reaching another person 🟡) are already active from
that point. Module 110 lets the user *adjust* from that safe baseline
later; it is not the sole source of safety, and a half-finished interview
should never leave a gap where nothing is governing autonomy.

## Module sequence

| # | Module | Reference | Writes to |
|---|---|---|---|
| 00 | Orientation | `reference/00_orientation.md` | identity constants, `state.json` |
| 10 | Identity & Profile | `reference/10_identity-profile.md` | `me/profile.md` |
| 20 | Goals & Priorities | `reference/20_goals-priorities.md` | `me/goals.md` |
| 30 | Voice & Communication | `reference/30_voice-communication.md` | `me/voice.md` |
| 40 | Values & Principles | `reference/40_values-principles.md` | `me/values.md`, optionally `constitution/Ethos.md` |
| 50 | Work & Project Domains | `reference/50_work-domains.md` | `me/projects.md`, seeds folder-map |
| 60 | Health & Sustainable Pace | `reference/60_health-pace.md` | `me/health.md`, `constitution/The-Rhythm.md` |
| 70 | Finance *(flag as skippable first)* | `reference/70_finance.md` | `me/finance.md` |
| 80 | Agent Roster | `reference/80_agent-roster.md` | `me/agents-guide.md` |
| 90 | Folder & File Organization | `reference/90_folder-organization.md` | `me/folder-map.md` |
| 100 | Cost & Model Routing | `reference/100_cost-model-routing.md` | `constitution/Dispatch.md`, `constitution/The-Stack.md` |
| 110 | Autonomy & Trust | `reference/110_autonomy-trust.md` | `constitution/Autonomy-Ladder.md`, `constitution/Constitution.md` |
| 999 | Assembly (not Q&A) | `reference/999_assembly.md` | `~/.claude/CLAUDE.md`, `Dashboard.md`, completion report |

Complete modules in order by default; honor a request to jump modules and
note the skip in `state.json`. Module 999 checks which modules are actually
done (not just "not explicitly skipped") before generating the final
`CLAUDE.md` and Dashboard.

## State write protocol

`_onboarding/state.json`:

```json
{
  "systemName": null,
  "systemHome": null,
  "yourName": null,
  "completedModules": [],
  "skippedModules": [],
  "inProgressModule": "00_orientation",
  "nextModule": "10_identity-profile",
  "lastUpdated": null
}
```

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
  `docs/ARCHITECTURE.md` if the user wants to do this later, by hand.

## Related files

- `constitution/BOOTSTRAP.md` / `HARVEST.md` — the same disk-persisted,
  resumable philosophy applied to ordinary dispatched sessions, not just
  onboarding.
- `docs/ARCHITECTURE.md` — the full picture of what this kit builds and why.
