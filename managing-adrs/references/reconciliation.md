A worked example of a populated `docs/adr/RECONCILIATION.md`, recording a
later periodic review of the ADR from `eval-vs-parser.md`. Compare against
the blank `assets/reconciliation.md` template.

```markdown
# ADR Reconciliation

| ADR | Title | Status | Last reviewed | Review result |
| --- | --- | --- | --- | --- |
| [0001](./0001-parse-formulas-not-eval.md) | Formulas are parsed into an expression tree, not run through eval() | Updated | 2027-01-15 | Still matches current implementation. |
```

This review happened independently of the amendment in `eval-vs-parser.md` —
reconciliation is a periodic check, not something that runs every time an
ADR changes. Nothing here touches the ADR's body; a reconciliation review
that *does* find drift becomes a new amendment in the ADR itself, following
[Updating an ADR](../SKILL.md#updating-an-adr).
