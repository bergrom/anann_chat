# Domain Docs

## Layout and reading rules

This repo uses a single-context layout:

- `CONTEXT.md` at the repo root: domain glossary.
- `docs/adr/`: architectural decision records.

Before exploring the codebase, read `CONTEXT.md` and ADRs relevant
to the area being changed.

If these documents do not exist, proceed silently.
The domain-modeling skill creates them lazily as terms and decisions
are resolved, typically through grill-with-docs or
improve-codebase-architecture.

## Use the glossary's vocabulary

Use terms from `CONTEXT.md` in issue titles, proposals, hypotheses
and test names. Avoid synonyms the glossary explicitly rejects.

If a needed concept is missing, reconsider whether it belongs to
the domain; note genuine gaps for domain-modeling.

## Flag ADR conflicts

Explicitly surface any proposal that contradicts an existing ADR,
identifying the ADR and explaining why it may be worth reopening.
