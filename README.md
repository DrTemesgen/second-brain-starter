# Second-Brain Starter

A personal AI operating system for [Claude Code](https://claude.com/claude-code) — a Constitution, an autonomy ladder, a dashboard, a dossier of files Claude reads to actually know your context, and a thorough self-serve interview that builds all of it around *your* work, not anyone else's.

This is a **starter kit**, not a finished product. Everything in it ships empty on purpose — the onboarding interview is what makes it yours.

## What you get

- **A guided onboarding interview** (13 modules — a short orientation, then identity, goals, voice, values, work domains, health, finance, your own agent roster, folder organization, cost/model routing, autonomy boundaries, and a final assembly step) that writes real, working config files as you answer, not a report you read once and forget.
- **A constitution and autonomy ladder** — plain-language rules about what this system can do on its own, what it drafts but never sends, and what it never does at all (money and credentials, full stop).
- **A dashboard** — one file that's the front door to your day: what's next, what's waiting on your OK, live deadlines, everything else indexed underneath it.
- **A dispatch ritual and cost-control guide** — the actual discipline (session hygiene, model-tier routing, one-task-one-session) that keeps this cheap to run, written up front instead of learned the expensive way.
- **Two starter agents** (`writer`, `researcher`) and a place to build your own — the onboarding interview helps you design a roster from your actual recurring work rather than handing you someone else's.
- **A `verify` health-check** — a read-only skill that confirms nothing's broken (no leftover `{{PLACEHOLDER}}` tokens, all the expected files present) any time you want to check, without re-running the whole interview.

## Quick start

1. **Clone this repo** somewhere on your machine.
2. **Install it as a local Claude Code plugin marketplace** — see [`docs/SETUP.md`](docs/SETUP.md) for the exact commands.
3. **Run `/assistant:home`** in a Claude Code session (plugin skills carry the plugin name as a prefix, so it is `assistant:home`, never bare `home`). On first run, it'll notice nothing's configured yet and offer to start onboarding.
4. **Answer honestly, skip what you want to skip** (Finance especially is explicitly optional) — you can pause anytime and pick up later; progress is saved to disk, not lost when you close the terminal.
5. Once onboarding finishes, `~/.claude/CLAUDE.md`, `~/.claude/me/*.md`, your `Dashboard.md`, and your own constitution folder are all real, filled-in files — read through them, adjust anything by hand, and start using it.

## Before you commit anything real

This repo is private by default and should stay that way unless you deliberately decide otherwise — see Constitution Article 5 once it's set up. Nothing about your onboarding answers ever leaves your own machine; there's no telemetry, no callback, no shared account.

## Learn more

- [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md) — how the pieces fit together, and what to build yourself if you want more (scheduled sync, a topic-specific radar skill, additional agents).
- [`docs/FAQ.md`](docs/FAQ.md) — common questions.
- [`docs/VERIFICATION-CHECKLIST.md`](docs/VERIFICATION-CHECKLIST.md) — how this kit was checked for leftover personal content before being handed to you; reuse it if you ever fork this further for someone else.

## License

MIT — see [`LICENSE`](LICENSE). Use it, fork it, change anything.
