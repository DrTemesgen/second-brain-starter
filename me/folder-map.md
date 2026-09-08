# Folder Map — Where Work Gets Filed

<!-- THE ROUTING RULE: you open Claude and just talk; Claude decides the
     destination folder from this map, creates files THERE (not in the
     current working directory), and always tells you the full path back
     as a clickable link. If genuinely ambiguous, it asks ONE question —
     never silently guesses, and never creates a "New folder"-style name.
     Populated by onboarding Module 90. -->

*Last updated: {{DATE}}.*

## Destination roots by topic

| Topic | Destination |
|---|---|
| *(example)* Everything under one employer/venture | `{{ROOT}}/<matching subfolder>` |
| Cross-cutting, unclear, or one-off quick items | `{{SYSTEM_HOME}}/_Inbox/YYYY-MM-DD <short name>` — triage later |
| This system's own memory/dossier | `~/.claude/me/` (never mixed with project files) |

<!-- Use whatever path separator your own OS actually uses (\ on Windows,
     / elsewhere) — these examples use / for portability of this template
     itself, not as a rule about your paths. -->

<!-- Replace the example row with your real destination roots — one per
     employer, venture, or major life area is a reasonable shape, but set
     your own. -->

## Routing heuristics

1. **Ownership boundary first** — if more than one "who owns this" applies
   to your life (an employer vs. your own work, for instance), keep that
   boundary clean; it usually matters more later than it seems to now.
2. **Existing home beats new folder** — search this map, then check for an
   existing folder, before creating anything new.
3. **New project folders** only when a real new project starts; clear,
   descriptive names, inside the right root — never at the drive's top
   level, never "New folder."
4. **Always announce the path** in the final summary, as a clickable link.
5. **Inbox discipline** — anything filed to `_Inbox` gets flagged at a
   later session start so it doesn't quietly become permanent.

## Known mess (cleanup candidates — offer, don't act unasked)

<!-- A running punch-list of folder cruft you've noticed — near-duplicate
     folders, stray "New folder (2)"s, whatever's accumulated. Claude
     should offer to clean these up, never do it unprompted — see
     Constitution Article 6. -->
