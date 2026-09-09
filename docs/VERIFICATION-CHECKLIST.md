# Verification checklist

This is the leak-check this kit was run through before being handed to
anyone — kept in-repo so it's reusable if you ever fork this further for
someone else, and so you can verify the copy you received yourself.

**The name/org/path patterns below are specific to *this* kit's own
original author** (used to verify nothing of his leaked into the
generic template). If you're reusing this checklist to sanitize a fork
of your own for someone else, swap them for your own name, organizations,
and file paths first — the patterns are examples of the category to
search for, not a fixed list.

## What "clean" means here

Zero live default content matching any category below. A category term
appearing inside an explicitly-marked instructional `<!-- -->` comment as
an illustrative example (e.g. "e.g., if you run a training program in
Ethiopia...") is fine — anything appearing as content a fresh install would
actually ship with is not.

**Expected, allowed hits — not a leak:** the kit's own author-attribution
fields are supposed to carry his real name/email (see
`docs/ARCHITECTURE.md` and Module 00's own explanation of why) — that's
`plugin.json`, `marketplace.json`, `LICENSE`, and the clone URL in
`docs/SETUP.md`. Exactly those four, for the name sweep; just the two
manifests for the email sweeps. This checklist file is excluded from the
sweeps below because it quotes the very patterns it searches for — with
that exclusion in place, a clean run really does mean zero unexpected
matches.

> **Read this before trusting a clean run.** Two failure modes make these
> commands *look* like they passed when they didn't actually run:
>
> 1. **`-E` is not "extended regex" in ripgrep — it's `--encoding`.**
>    `rg -iE "pattern"` fails with `unknown encoding: pattern`, exit
>    code 2, **and prints nothing** — indistinguishable from a clean
>    result at a glance. (rg's default syntax already supports
>    alternation, `\b`, and character classes, so no `-E` is needed.)
>    Every command below is written without it, and every one was run
>    against this repo before being written down.
> 2. **rg skips hidden directories by default**, so without `--hidden`
>    it never scans `.claude-plugin/` — two of the four files you're
>    told to expect hits in. `--hidden` is included below, along with a
>    `.git` exclusion so commit metadata (which legitimately contains the
>    author's name and email) doesn't drown the results.
>
> **Always check the exit code, not just the output:** `0` = matches
> found, `1` = clean, `2` = the command errored and told you nothing.

## Grep sweep

Run from the repo root:

Patterns are **single-quoted throughout, deliberately.** In double quotes
bash eats `$` and mangles backslash runs — `"\\\$[0-9]"` silently becomes
the pattern `\\-9`, which matches "60-90 minutes" and misses `$10M`. A
pattern broken that way looks like a passing sweep in both directions.

```bash
EXCL="--glob=!docs/VERIFICATION-CHECKLIST.md --glob=!.git"

# Author's name — expected ONLY in LICENSE, SETUP.md, and the 2 manifests
rg -i --hidden $EXCL 'temesgen|endalew|legesse|drtemesgen'

# The originating system's own name — everything should say
# {{SYSTEM_NAME}}, never a specific chosen name. Expect zero.
rg -i --hidden $EXCL '\belroi\b'

# Contact info — expected ONLY in the 2 manifests
rg -i --hidden $EXCL 'dolce\.temesgen@gmail\.com|@aslm\.org|@sphmmc\.edu\.et'
rg -i --hidden $EXCL '\+251[ -]?9'                        # expect zero

# Named organizations — expect zero
rg -i --hidden $EXCL '\bASLM\b|\bADHA\b|\bADHN\b|\bSPHMMC\b|Africa CDC|\bMERQ\b|\bBBI\b'

# Specific figures that shouldn't be live defaults — spot-check by hand.
# `[$]` as a character class, not `\$` — no escaping to get wrong.
rg -n --hidden $EXCL '[$][0-9][0-9,.]*[kKmM]?'
rg -i --hidden $EXCL '[0-9]{1,3},?[0-9]{3}\+? (followers|learners|countries|seats)'

# Filesystem paths specific to one machine/person — expect zero.
# `.` stands in for the path separator on purpose; a literal backslash
# has to survive both shell and regex parsing and errors out instead
# (exit 2, silent).
rg -i --hidden $EXCL 'D:.(HQ|ASLM|Noochi)|C:.Users.[a-z]+'

# Infrastructure that should never travel between machines — expect zero
rg --hidden $EXCL '([0-9]{1,3}\.){3}[0-9]{1,3}'
rg -i --hidden $EXCL 'ssh\s+[a-z0-9_-]+@'

# General secret/PII hygiene — email expected ONLY in the 2 manifests,
# the other two expect zero
rg -i --hidden $EXCL '[a-zA-Z0-9._%+-]+@(gmail|yahoo|hotmail|outlook|protonmail|icloud)\.(com|net|org)'
rg -i --hidden $EXCL -- '-----BEGIN\s+(RSA\s+|EC\s+|DSA\s+|OPENSSH\s+)?PRIVATE KEY-----'
rg -i --hidden $EXCL '(api|access)[_-]?key|secret[_-]?key'
```

**Before trusting any pattern you add or change yourself, prove it can
actually match.** Drop a line containing the thing you're hunting into a
scratch file and confirm the pattern finds it — a regex that silently
matches nothing looks identical to a clean repo. That failure is exactly
how a broken sweep survived two review rounds here.

Run this from a **fresh context** if you're the one who authored or edited
the content — a session that just wrote the content is prone to checking
its own blind spots rather than genuinely re-verifying.

## Structural checks

- [ ] Every `me/*.md` file has section headers and `<!-- -->` comments
      only — no filled-in personal content.
- [ ] Every `constitution/*.md` file uses `{{PLACEHOLDER}}` tokens for
      anything person-specific, never a real name/path/number as a live
      default.
- [ ] `plugin.json` and `marketplace.json` carry the **kit author's**
      real name/email — that's correct, not a leak, since the installer's
      own identity never goes in these files (see
      `docs/ARCHITECTURE.md`) — and license is `MIT`, not `UNLICENSED`.
- [ ] `git log` shows a clean, minimal history with no earlier
      draft/pre-genericization commit ever existing to leak.
- [ ] No `.env`, `*.pem`, `credentials.json`, or similar dangerous files
      exist anywhere in the tree.

## Fresh test-install

- [ ] `claude plugin validate` passes on both the repo root and the
      plugin folder.
- [ ] Installed fresh in a scratch directory, `/assistant:home` correctly detects
      the empty dossier and offers onboarding.
- [ ] Onboarding Module 00 runs a few real turns without error, writes
      `~/.claude/_onboarding/state.json` correctly (including `kitRoot`,
      resolved without asking if self-location works), and resuming
      after a stop picks up from the right module.
- [ ] Module 999's final token sweep actually catches an unresolved
      `{{...}}` token if you deliberately skip a module that owns one
      (e.g. skip Module 40's mission line, confirm `{{YOUR_MISSION}}`
      gets cleanly removed rather than left dangling in `Constitution.md`).
- [ ] `writer` and `researcher`, invoked against a still-empty dossier,
      report missing context rather than fabricating personal details.
- [ ] `verify`, run against a fully-completed setup, reports clean with
      no false positives on `me/feedback.md` or `People/*.md`'s
      permanent template tokens; run against a deliberately incomplete
      one, it correctly names what's missing and which module owns it.
- [ ] The credential-sweep hook (`hooks.json`) actually fires — try a
      Bash command like `find . -name "*.pem"` combined with a password
      keyword and confirm it's denied. It depends on `jq` and POSIX
      shell being available; on Windows without Git Bash or WSL it may
      silently do nothing (the hook's own `exit 0` swallows the failure)
      — worth knowing before relying on it.
