---
name: managing-adrs
description: Use when creating or updating an Architecture Decision Record (ADR), when the user asks to "record a decision" or "write an ADR", or before making/implementing a hard-to-reverse architectural, technology, or boundary decision that came from weighing real alternatives. Also use before changing code in an area that might already have a documented rationale — check docs/adr/ first.
---

# Managing ADRs

ADRs live in `docs/adr/`, one file per decision, sequentially numbered: `0001-slug.md`, `0002-slug.md`. Create the directory lazily — only when the first ADR is actually needed.

An ADR is a single paragraph by default. The value is recording *that* a decision was made and *why*, not filling out sections.

An ADR captures the decision and the trade-off, never the implementation or design. Leave schemas, API shapes, configs, and code structure to the code and any design docs — if a draft starts describing *how* something is built, cut it back to *what* was decided and *why*.

## When to write one

**Qualifies:**
- Architectural shape — monorepo vs. polyrepo, event-sourced vs. CRUD
- Integration pattern between components — async events vs. sync HTTP
- Technology choice that carries lock-in — database, message bus, auth provider
- Boundary/ownership decision — "X owns this data, others reference it by ID"
- Deliberate deviation from the obvious path — "manual SQL instead of an ORM, because..."
- Constraint invisible in the code — "can't use AWS because of compliance"
- A rejected alternative someone will likely propose again later

**Doesn't qualify:**
- Anything trivially reversible
- The only reasonable option — nothing was actually traded off
- Routine library or tool picks

## Statuses

| Status | Meaning |
|---|---|
| `pending` | Proposed, not yet agreed — still open for discussion |
| `accepted` | The current, agreed decision |
| `rejected` | Considered and explicitly turned down — recorded so it isn't re-proposed |
| `updated` | Still the active decision, but amended — see [Updating an ADR](#updating-an-adr) |
| `superseded` | Replaced outright by a newer ADR (see `superseded_by`) |

## Before writing: get agreement

An ADR *records* a decision — it doesn't make one. Before creating the file, restate the decision back to the user in a sentence or two ("So: formulas get parsed into an expression tree instead of run through eval() — recording that?") and confirm.

If the decision is genuinely still open, it's fine to write the ADR now with `status: pending` rather than waiting — just don't mark it `accepted` until it actually is.

## Creating a new ADR

1. Check for an existing decision first: grep `docs/adr/` for the topic. Don't create a second ADR that silently contradicts or duplicates one that already exists.
2. Scan `docs/adr/` for the highest existing number; the new one is that + 1 (first ever is `0001`).
3. Pick a short, lowercase, hyphenated slug for the filename.
4. Write the file from `assets/adr.md`.
5. Add a row for it to `docs/adr/README.md` (create that file from `assets/readme.md` if this is the first ADR).

### Optional fields / sections

Add only when they add real value — most ADRs won't need any of these:

- `status_note` — one line explaining a `rejected` or `superseded` status
- `superseded_by: "0007"` — set on the old ADR when a newer one replaces it
- **Considered Options** — only when the rejected alternatives are worth remembering
- **Consequences** — only when a non-obvious downstream effect needs calling out

## Updating an ADR

Three tiers, don't mix them up:

1. **Typo or wording fix, meaning unchanged** — edit the file in place, no status change.
2. **Material amendment, original decision still holds** — don't rewrite the body. Add a dated update note directly under the title, above the original paragraph, and set `status: updated`. See `references/eval-vs-parser.md` for a full before/after.
3. **Full reversal or incompatible replacement** — write a new ADR for the new decision. Set the old ADR's `status: superseded` and `superseded_by: "NNNN"`. Never delete or rewrite the old body; it's the historical record of what was decided and why at the time.

In every case, update the status column for that ADR in `docs/adr/README.md`.

## docs/adr/README.md

A hand-maintained index so the set of decisions can be scanned without opening every file. Create it alongside the first ADR from `assets/readme.md`. Add a row when creating an ADR; update the `Status` cell whenever an ADR's status changes.

## docs/adr/RECONCILIATION.md

A periodic drift check, separate from the ADRs themselves and from the README. Use it when reviewing whether past decisions still match reality — don't touch an ADR's body for this unless something material actually changed (then follow [Updating an ADR](#updating-an-adr) instead). Create it from `assets/reconciliation.md`, once there are enough ADRs that a periodic review is worth doing — it's overhead for a one- or two-ADR repo.

## Helping future agents

Before changing code in an area that looks deliberate, unusual, or hard to explain, grep `docs/adr/` for a related decision before "fixing" it — it may be intentional.

## Quick reference

| Situation | Action |
|---|---|
| New hard-to-reverse, non-obvious, trade-off-driven decision | New ADR, next number, add to README |
| Decision still being discussed | New ADR with `status: pending` |
| Decision considered and turned down | New ADR (or update existing) with `status: rejected` |
| Typo/wording fix | Edit the existing ADR in place, no status change |
| Material amendment, decision still holds | Add dated update note under the title, `status: updated` |
| Full reversal | New ADR + old one gets `status: superseded` / `superseded_by` |
| Possible duplicate | Grep `docs/adr/` before creating |
| About to touch a "weird" area of code | Grep `docs/adr/` before changing it |
