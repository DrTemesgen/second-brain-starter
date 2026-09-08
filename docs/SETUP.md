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
```

Fix anything that reports invalid before continuing — a manifest error here
means the plugin won't load at all.

## 3. Add it as a local marketplace and install

In a Claude Code session:

```
/plugin marketplace add <path-to-this-folder>
/plugin install assistant@second-brain-starter
```

<!-- Exact command names/flags can drift between Claude Code versions —
     if either of these doesn't match what your version expects, run
     `/plugin` on its own first; it'll show the current subcommands. -->

## 4. Run onboarding

```
/home
```

On a fresh install, `home` detects nothing's configured yet and offers to
start the onboarding interview. Say yes, and work through it at your own
pace — every module can be paused and resumed, and several (Finance
especially) are explicitly fine to skip.

## 5. Confirm it worked

After onboarding finishes, check:

- `~/.claude/CLAUDE.md` exists and reflects your real answers (not
  placeholder tokens).
- `~/.claude/me/*.md` — all 10 files have real content, or an explicit,
  intentional skip note (Finance/Health if you opted out).
- Your system home (wherever you said it should live) has a real
  `Dashboard.md` and a constitution folder with your actual settings.

If anything still shows a `{{PLACEHOLDER}}` token after onboarding
completed, that's worth fixing by hand or re-running the relevant module.

## Troubleshooting

- **Plugin won't load / validate fails:** check the two `.claude-plugin/*.json`
  manifests for valid JSON — a trailing comma or unescaped character is the
  usual cause.
- **Onboarding seems to have lost progress:** check
  `{{systemHome}}/_onboarding/state.json` — it should show which module was
  last in progress. If it's missing entirely, onboarding will just start
  fresh from Module 00; nothing else breaks.
- **Something references a `{{PLACEHOLDER}}` that never got filled:** most
  likely a module was skipped rather than completed — re-run it, or fill
  the placeholder by hand.
