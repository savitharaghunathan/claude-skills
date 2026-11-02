A worked example of a populated `docs/adr/README.md`, continuing the
`eval-vs-parser.md` example after its amendment. Compare against the blank
`assets/readme.md` template.

```markdown
# Architecture Decision Records

| ADR | Title | Status | Date | Author |
| --- | --- | --- | --- | --- |
| [0001](./0001-parse-formulas-not-eval.md) | Formulas are parsed into an expression tree, not run through eval() | Updated | 2026-11-02 | Grace Hopper |
```

The `Status` cell reads `Updated`, not `Accepted` — it was flipped when the
ADR was amended (see `eval-vs-parser.md`). `Date` stays the original decision
date; the index doesn't track amendment dates, only the ADR body does.
