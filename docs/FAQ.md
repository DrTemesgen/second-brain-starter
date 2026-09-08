# FAQ

**Do I need my own Claude subscription/API access?**
Yes — this runs entirely on your own Claude Code installation and your own
account. Nothing here shares billing, an account, or a session with
whoever gave you this kit.

**Does anything I say during onboarding get sent anywhere?**
No. Onboarding runs locally in your own Claude Code session and writes only
to files on your own machine. There's no telemetry, no callback URL, no
mechanism by which your answers could reach anyone else — because none was
built.

**Can I skip modules?**
Yes. Every module is skippable; Finance and the optional Ethos exercise are
explicitly flagged as fine to skip before they even start. A skip is a
complete, valid outcome — the rest of the system works fine around a gap.

**Can I re-run a module later?**
Yes — values, voice, and goals especially tend to drift over time. Ask to
re-run any specific module by name (or number) whenever you want.

**What if I already have a `~/.claude/CLAUDE.md`?**
Onboarding's final Assembly step checks for one before writing anything —
if it exists, you'll be offered a merge, an append, or a fresh overwrite;
it's never silently replaced.

**Is this safe to make public / open-source?**
Structurally, yes — this kit shipped with no personal content by design,
and was checked against a leak-pattern checklist before being handed to
you (see `docs/VERIFICATION-CHECKLIST.md`). But once you run onboarding,
your own `~/.claude/me/*.md` and your constitution folder will contain
real personal information — keep *those* private regardless of what you
decide about the starter kit's own template repo.

**What's the difference between the Constitution and the Autonomy Ladder?**
The Constitution states the fixed principles (money and credentials are
never autonomous, nothing reaches another person without your OK, etc.) —
it changes rarely, and Article 3 (money/credentials) is designed to never
change at all. The Autonomy Ladder is the operational table underneath it —
per-capability tiers you're expected to actually adjust as trust is earned
or your work changes.

**Do I have to use the `writer` and `researcher` agents?**
No — they're starting points. Skip them, adjust them, or replace them
entirely once onboarding Module 80 helps you figure out what you actually
need.

**Something references a `{{PLACEHOLDER}}` I don't recognize — what do I
do?**
It means the module that fills that value either hasn't run yet or was
skipped. Check `docs/SETUP.md`'s troubleshooting section.
