# Session Sync Log

<!-- The actual sync primitive for multi-session work: an append-only,
     newest-first log every session (main or dispatched) reads on
     `BOOTSTRAP.md` and writes to on `HARVEST.md`. Its whole value is being
     boring and consistent — don't restructure it, just append. -->

*Newest entries at the top. Each entry: date, session/task, one line on
what happened. Full harvest detail belongs in the harvest itself (pasted
into the Dashboard or kept in the dispatching session) — this log is the
index, not the archive.*

---

<!-- First real entry goes here once you start dispatching sessions. -->
