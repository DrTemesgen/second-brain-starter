# Verification checklist

This is the leak-check this kit was run through before being handed to
anyone — kept in-repo so it's reusable if you ever fork this further for
someone else, and so you can verify the copy you received yourself.

## What "clean" means here

Zero live default content matching any category below. A category term
appearing inside an explicitly-marked instructional `<!-- -->` comment as
an illustrative example (e.g. "e.g., if you run a training program in
Ethiopia...") is fine — anything appearing as content a fresh install would
actually ship with is not.

## Grep sweep

Run from the repo root, case-insensitive (`rg -i` shown; any equivalent
grep works). Every one of these should return **no matches** outside
explicitly-marked instructional examples:

```bash
# Any real person's name baked in as live content
rg -i "temesgen|endalew|legesse|drtemesgen"

# The originating system's own name — everything here should say
# {{SystemName}} / {{SYSTEM_NAME}}, never a specific chosen name
rg -i "\belroi\b"

# Contact info
rg -iE "dolce\.temesgen@gmail\.com|@aslm\.org|@sphmmc\.edu\.et"
rg -iE "\+251[ -]?9"

# Named organizations that shouldn't appear in a generic kit
rg -iE "\bASLM\b|\bADHA\b|\bADHN\b|\bSPHMMC\b|Africa CDC|\bMERQ\b|\bBBI\b"

# Specific figures that shouldn't be live defaults anywhere
rg -noE "\$[0-9][0-9,.]*[kKmM]?"        # spot-check every hit by hand
rg -iE "[0-9]{1,3},?[0-9]{3}\+? (followers|learners|countries|seats)"

# Filesystem paths specific to one machine/person
rg -iE "D:\\\\HQ|D:\\\\ASLM|D:\\\\Noochi|C:\\\\Users\\\\[a-z]+\\\\"

# Infrastructure that should never travel between machines
rg -iE "([0-9]{1,3}\.){3}[0-9]{1,3}"    # spot-check every IP hit by hand
rg -iE "ssh\s+[a-z0-9_-]+@"

# General secret/PII hygiene (reuses common sanitizer patterns)
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
- [ ] `plugin.json` and `marketplace.json` both use `{{YOUR_NAME}}` /
      `{{YOUR_EMAIL}}` placeholders, and license is `MIT`, not
      `UNLICENSED`.
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
      `_onboarding/state.json` correctly, and resuming after a stop picks
      up from the right module.
- [ ] `writer` and `researcher`, invoked against a still-empty dossier,
      report missing context rather than fabricating personal details.
