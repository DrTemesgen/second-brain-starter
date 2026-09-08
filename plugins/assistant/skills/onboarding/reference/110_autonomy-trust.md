# Module 110 — Autonomy & Trust

Writes `constitution/Autonomy-Ladder.md` and, if anything in Module 40 or
elsewhere implied a change to a fixed article, `constitution/Constitution.md`.
This module *adjusts* an already-safe default — the ladder has been active
with conservative defaults since Module 00 completed (see the Safety by
default note in the main SKILL.md).

## Topics to cover

Walk every row of the shipped `Autonomy-Ladder.md` explicitly — don't
silently accept the defaults without asking, but don't belabor the obvious
ones either:

- File organization, building/deploying to their own private environments,
  research/drafting, dossier/dashboard housekeeping, reversible edits they
  explicitly asked for — confirm 🟢 (autonomous) still feels right, or
  tighten if not.
- Anything reaching another person — confirm 🟡 (draft-only). This one is
  never demoted further; say so plainly (Constitution Article 4).
- Deleting/moving/overwriting their existing files, bulk operations,
  account or security settings changes, making something public, entering
  data into third-party forms — confirm 🟠 (confirm-first) or ask if any
  should be tighter for them specifically.
- Production/live infrastructure — if Module 50 surfaced anything they
  depend on operationally (a live site, a service others use), add a row
  for it and confirm 🟠 at minimum.
- Money, credentials, account creation — confirm 🔴 (never), and be
  explicit that *this* tier can't be lowered no matter how it's framed
  later, including by them — that's the point of a hard guardrail
  (Constitution Article 3, which covers exactly these three, not more).
- Permanent deletion — shipped at 🔴 too, but as a strong *default*, not
  a constitutional floor like the row above (Article 3 doesn't cover it).
  If they have a real reason to run it at 🟠 confirm-first instead (still
  warned every time, per Article 6), that's a legitimate choice — just
  make sure it's a deliberate one, not a default nobody looked at.
- **Anything specific to their own work** worth its own row — a
  certification/exam system, regulated client data, anything with its own
  particular risk profile that the shipped default rows don't cover.

## Interview notes

This module is closer to a confirmation pass than deep laddering — most of
the shipped defaults are reasonable and won't change. Move quickly through
rows that are clearly fine; spend real time only on rows the user wants to
adjust or new rows specific to their situation.

## What gets written

Update the Tier column in the **instantiated**
`{{SYSTEM_HOME}}/{{SYSTEM_NAME}}/Autonomy-Ladder.md` (created at Module
00, not the kit's own source file) for any row they adjusted, add any new
rows they specified, and set the "Reviewed" date. Only touch that same
instantiated `Constitution.md` if they want to actually amend an article
(rare — most adjustments belong in the ladder, not the constitution
itself); if so, add a line to its amendment log.

## Close

"Module 110 saved. Last step: Assembly — this one isn't a Q&A, it's where
everything gets put together. Ready to run it now?"
