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
`docs/SETUP.md`. The name/email sweeps below will correctly hit exactly
those four places and nowhere else; that's a PASS, not a finding.

## Grep sweep

Run from the repo root, case-insensitive (`rg -i` shown; any equivalent
grep works). Every one of these should return **no matches outside the
four author-attribution files above** (and none at all for the org/path/
infrastructure sweeps, which have no legitimate hit anywhere):

```bash
# Author's name — expected ONLY in plugin.json, marketplace.json, LICENSE
rg -i "temesgen|endalew|legesse|drtemesgen"

# The originating system's own name — everything here should say
# {{SYSTEM_NAME}}, never a specific chosen name
rg -i "\belroi\b"

# Contact info — expected ONLY in plugin.json, marketplace.json
rg -iE "dolce\.temesgen@gmail\.com|@aslm\.org|@sphmmc\.edu\.et"
rg -iE "\+251[ -]?9"

# Named organizations that shouldn't appear anywhere in a generic kit
rg -iE "\bASLM\b|\bADHA\b|\bADHN\b|\bSPHMMC\b|Africa CDC|\bMERQ\b|\bBBI\b"

# Specific figures that shouldn't be live defaults anywhere
rg -noE "\$[0-9][0-9,.]*[kKmM]?"        # spot-check every hit by hand
rg -iE "[0-9]{1,3},?[0-9]{3}\+? (followers|learners|countries|seats)"

# Filesystem paths specific to one machine/person
rg -iE "D:\\\\HQ|D:\\\\ASLM|D:\\\\Noochi|C:\\\\Users\\\\[a-z]+\\\\"

# Infrastructure that should never travel between machines
rg -iE "([0-9]{1,3}\.){3}[0-9]{1,3}"    # spot-check every IP hit by hand
rg -iE "ssh\s+[a-z0-9_-]+@"

# General secret/PII hygiene (reuses common sanitizer patterns) —
# expected ONLY the author's gmail in the two files named above
rg -iE "[a-zA-Z0-9._%+-]+@(gmail|yahoo|hotmail|outlook|protonmail|icloud)\.(com|net|org)"
rg -iE "-----BEGIN\s+(RSA\s+|EC\s+|DSA\s+|OPENSSH\s+)?PRIVATE KEY-----"
rg -iE "(api|access)[_-]?key|secret[_-]?key" -- --glob '!docs/VERIFICATION-CHECKLIST.md'
```

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
- [ ] Installed fresh in a scratch directory, `/home` correctly detects
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
- [ ] The credential-sweep hook (`hooks.json`) actually fires — try a
      Bash command like `find . -name "*.pem"` combined with a password
      keyword and confirm it's denied. It depends on `jq` and POSIX
      shell being available; on Windows without Git Bash or WSL it may
      silently do nothing (the hook's own `exit 0` swallows the failure)
      — worth knowing before relying on it.
