# Setup

## 1. Get the files onto your machine

```bash
git clone https://github.com/DrTemesgen/second-brain-starter
cd second-brain-starter
```

Or, if you received this as a plain folder rather than a git URL: put it
somewhere on your machine and run `git init` inside it yourself, so you
have your own history from the start.

## 2. Validate the plugin

```bash
claude plugin validate ./plugins/assistant
claude plugin validate .
jq --version
```

Fix anything the first two report invalid before continuing — a manifest
error here means the plugin won't load at all. The `jq` check is a
different kind of failure: everything still installs and works without
it, but the credential-sweep hook depends on it and fails *silently* if
it's missing (most common on Windows without Git Bash or WSL) — better
to know that now than to believe a security guard is active when it
isn't. Install `jq` if you want that guard working.

## 3. Add it as a local marketplace and install

In a Claude Code session:

```
/plugin marketplace add <path-to-this-folder>
/plugin install assistant@second-brain-starter
```

<!-- Exact command names/flags can drift between Claude Code versions —
     if either of these doesn't match what your version expects, run
     `/plugin` on its own first; it'll show the current subcommands. -->

**Keep the folder you cloned/unzipped.** Installing the plugin only
copies `plugins/assistant/` into Claude Code's own plugin store — it does
**not** copy `me/`, `constitution/`, `bootstrap/`, or `Dashboard.md`.
Onboarding reads those directly from wherever you put the kit in step 1,
every time it needs a fresh template. Deleting that folder after
installing breaks onboarding, even if the plugin still shows as
installed.

## 4. Run onboarding

```
/home
```

On a fresh install, `home` detects nothing's configured yet and offers to
start the onboarding interview. Say yes, and work through it at your own
pace — every module can be paused and resumed, and several (Finance
especially) are explicitly fine to skip.

**Roughly how long this takes:** 13 modules, one question at a time, real
conversation rather than a form — figure 60-90 minutes total if you did
it all in one sitting, though almost nobody does. Module 00 alone is
under 5 minutes, and the system is fully safe (conservative defaults
active, nothing destructive possible) from the moment that one finishes —
everything after that is refinement, on whatever schedule you want across
as many sessions as you want.

## 5. Confirm it worked

After onboarding finishes, check:

- `~/.claude/CLAUDE.md` exists and reflects your real answers (not
  placeholder tokens).
- `~/.claude/me/*.md` — most of the 10 files should have real content;
  two are correctly *not* filled by onboarding itself and that's not a
  failure: `feedback.md` starts empty and fills in as you actually give
  feedback later, and `agents-guide.md` can legitimately say "none yet"
  if Module 80 didn't build a custom roster.
- Your system home (wherever you said it should live) has a real
  `Dashboard.md` and a constitution folder with your actual settings.

If anything still shows a `{{PLACEHOLDER}}` token after onboarding
completed, that's worth fixing by hand or re-running the relevant module.

## Troubleshooting

- **Plugin won't load / validate fails:** check the two `.claude-plugin/*.json`
  manifests for valid JSON — a trailing comma or unescaped character is the
  usual cause.
- **Onboarding seems to have lost progress:** check
  `~/.claude/_onboarding/state.json` — it should show which module was
  last in progress. If it's missing entirely, onboarding will just start
  fresh from Module 00; nothing else breaks.
- **Something references a `{{PLACEHOLDER}}` that never got filled:**
  ask to `/verify` first — it's a quick, read-only check that tells you
  exactly what's unresolved and which module owns it, without re-running
  anything. Then re-run that specific module, or fill the placeholder by
  hand. (Re-running the whole of Assembly also works and is safe to do —
  it checks for existing files before touching anything — but `verify`
  is faster for just checking.)
- **Onboarding can't find its own templates / asks where you put the kit:**
  this means it couldn't infer its own location automatically — just tell
  it the path from step 1. It'll remember (`kitRoot` in `state.json`) and
  won't ask again. If you moved or deleted that folder, put it back (or
  re-clone) before continuing.
- **The credential-sweep hook doesn't seem to be doing anything:** it's a
  POSIX shell command that needs `jq` on `PATH`. On macOS/Linux this is
  usually already true; on Windows without Git Bash or WSL it may not be,
  and the hook fails silently rather than erroring loudly. Install `jq`
  or run Claude Code through Git Bash/WSL if you want this guard active.
