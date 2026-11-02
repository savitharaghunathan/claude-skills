A worked example, following one ADR through its life and into the index files
that reference it. It illustrates the template, the `updated` status, and the
amendment convention from SKILL.md — it isn't a real decision in this skill's
own repo.

## As first written (`docs/adr/0001-parse-formulas-not-eval.md`)

```markdown
---
adr: "0001"
title: "Formulas are parsed into an expression tree, not run through eval()"
status: accepted
date: "2026-11-02"
author: "Grace Hopper"
---

# Formulas are parsed into an expression tree, not run through eval()

Users type arbitrary formulas to solve and plot, and `eval()` would run
whatever they type with full access to the runtime. A parser turns the
input into an expression tree instead — the same tree we walk to simplify
an equation, solve it, and sample points to draw its graph. The trade-off:
writing and maintaining a parser is real, ongoing work that `eval()` would
have made disappear in one line.
```

## After a later amendment, same file

The original decision still holds, so this isn't a new ADR — it's an update
note added above the original paragraph, with `status` flipped to `updated`:

```markdown
---
adr: "0001"
title: "Formulas are parsed into an expression tree, not run through eval()"
status: updated
date: "2026-11-02"
author: "Grace Hopper"
---

# Formulas are parsed into an expression tree, not run through eval()

**Update (2026-12-10):** Added a term-rewriting pass that simplifies the
tree before plotting, cutting typical render time in half — the original
decision to parse instead of eval still holds.

Users type arbitrary formulas to solve and plot, and `eval()` would run
whatever they type with full access to the runtime. A parser turns the
input into an expression tree instead — the same tree we walk to simplify
an equation, solve it, and sample points to draw its graph. The trade-off:
writing and maintaining a parser is real, ongoing work that `eval()` would
have made disappear in one line.
```

Note what didn't change: `date` stays at the original decision date. The
amendment's date lives only in the inline `**Update (...):**` note, and the
original paragraph is untouched below it.

See `readme.md` for this ADR's row in `docs/adr/README.md` after the
amendment, and `reconciliation.md` for its row in `docs/adr/RECONCILIATION.md`
after a later periodic review.
