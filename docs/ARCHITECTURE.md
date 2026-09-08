# Architecture

## The four destinations

This kit is one repo, but it unpacks to four places on your machine during
onboarding:

| Destination | Gets | Source in this repo |
|---|---|---|
| `~/.claude/CLAUDE.md` | Global always-on rules | `bootstrap/CLAUDE.md` |
| `~/.claude/me/*.md` | Your dossier (10 files) | `me/*.md` |
| `{{SYSTEM_HOME}}/Dashboard.md` + `{{SYSTEM_HOME}}/{{SYSTEM_NAME}}/*` | Working dashboard + constitution/ritual layer | `Dashboard.md`, `constitution/*` |
| Claude Code's own plugin store (wherever it caches installed plugins) | The installed plugin (agents/skills/hooks) | `plugins/assistant/*` |
| **Wherever you cloned/unzipped this repo — keep it** | The template *source* itself (`{{KIT_ROOT}}`) — onboarding reads `me/`, `constitution/`, `bootstrap/`, and `Dashboard.md` from here every time it needs a fresh copy | this whole repo |

`~/.claude/` is fixed by Claude Code itself. `{{SYSTEM_HOME}}` is wherever
you told onboarding Module 00 you want your working dashboard to live — the
equivalent of "open a folder and talk to Claude." **The repo clone is not
disposable** — installing the plugin only copies `plugins/assistant/`
into Claude Code's own store; it does not copy `me/`, `constitution/`,
`bootstrap/`, or `Dashboard.md`. Onboarding locates that clone
automatically most of the time (it can find its own file's location and
walk up to the repo root), asking you directly only if that fails — see
`SKILL.md`'s session-start protocol if you're curious how. Either way,
deleting the clone after installing breaks onboarding.

## Why only two starter agents

Earlier drafts of a kit like this considered shipping several pre-built
specialist agents (a curriculum-builder, an operations agent, a publishing
pipeline). They were cut. A genericized version of a narrow specialist —
one built around a domain that may not be yours — ends up doing nothing for
most users while still costing context in every session, whether it's ever
invoked or not.

Instead: two genuinely universal agents (`writer`, `researcher`) ship by
default, and onboarding Module 80 builds the rest of your roster live, from
whatever recurring work Module 50 actually surfaced about your life. This
is slower than picking from a menu, but it produces a roster that's
actually yours instead of a reskinned version of someone else's.

## Patterns documented here instead of shipped as code

A few things from more elaborate personal setups are genuinely useful but
too specific to any one person's infrastructure to ship as working code.
They're described here as patterns — build your own version if you want
them, using Claude itself to help.

### A topic radar skill

A short, recurring scan of a specific field for developments relevant to
your work — new tools, research, competitors, whatever you'd want surfaced
without hunting for it yourself. If you want one: pick a topic, describe
the cadence and format you want, and ask Claude to build you a skill
modeled on `daily-learning`'s structure but scoped to your subject.

### Scheduled sync and health-checks

A twice-daily (or whatever cadence you want) git commit-and-push of your
config and working files, plus a lightweight scheduled check that pings
you if something's gone quiet. Neither ships here — both depend on your
OS's task scheduler and your own repo layout. If you want this: ask Claude
to set up a scheduled task that runs a git add/commit/push on your `{{SYSTEM_HOME}}`
and `~/.claude` (as two separate commits/repos is a reasonable default,
since they have very different sensitivity — see the next section), and a
second scheduled check that reads the first one's last-run timestamp and
flags you if it's gone stale. The core insight worth keeping if you build
this: a monitor that can't report its own death needs a *second*,
independent check watching its freshness — silence is the warning, not a
reassuring headline status.

### Two-repo separation

If you end up wanting the same separation this kit's own lineage uses —
one repo for `~/.claude` (which can accumulate genuinely sensitive
material: credentials references, health/finance notes, private project
memory) and a separate one for your day-to-day working folder — that's a
reasonable pattern to adopt once you have enough real content to want it
split. Not necessary on day one.

## Optional: renaming the default slugs

The plugin folder (`assistant`), and its skills/agents (`home`,
`onboarding`, `daily-learning`, `writer`, `researcher`) ship with plain,
boring names on purpose — your system's actual personal name lives in
`Dashboard.md` and `CLAUDE.md` prose, not in a slash-command slug, so
nothing about how the system *works* depends on these names.

If you still want to rename them (e.g. `/onboarding` → `/get-started`):

1. Rename the corresponding folder under `plugins/assistant/skills/` or
   `plugins/assistant/agents/`.
2. Update the `name` field in that skill/agent's frontmatter.
3. Update any cross-references to the old name elsewhere in the kit (a
   simple repo-wide search for the old slug will find them).
4. Re-run `claude plugin validate` before reinstalling.

Do this once you're comfortable with the system, not during your first
onboarding session — it's real surface area for a mistake, for a
cosmetic benefit.

## Why the dossier ships empty

Every `me/*.md` file and every `constitution/*.md` file ships with section
headers and `<!-- -->` instructional comments, never real content. The
content is what onboarding produces — the templates are the *shape*, not a
starting draft to lightly edit. This is deliberate: a pre-filled template
either has to be someone else's actual life (wrong for you) or generic
placeholder prose that looks finished but isn't (worse than obviously
empty, because it's easy to skip reading closely).
