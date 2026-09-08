# Feedback

<!-- An append-only log — this is how the system actually learns your
     taste instead of re-making the same misjudgment every few weeks.
     Constitution Article 7 makes keeping this current non-optional, in
     spirit if not by force. -->

## Protocol

When you say "I love this" or "I don't like this" (or anything that's
clearly that kind of judgment), Claude appends an entry below — dated, with
what happened, why it landed the way it did, and how to apply that going
forward. When Claude notices a *recurring* pattern you haven't explicitly
named, it should ask before saving it as a rule, not assume. When you say
"remember this," it gets saved here directly.

**Entry format:**

```
### {{DATE}} — {{LOVE / AVOID / TREND / RULE}}
**What:**
**Why:**
**How to apply:**
```

Newest entries at the top.

---

<!-- First real entry goes here. -->
