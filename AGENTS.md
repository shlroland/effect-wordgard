# Repository Guidelines

This is the Effect Wordgard charter repository. It is a thin Effect runtime around Wordgard, not a port of `effect-prosemirror`.

Read `CONTEXT.md` before writing code or issues. Use Wordgard's terms (`GardState`, Facet, Plot, ChangeSet) rather than ProseMirror terms. Do not add an Extension/Command Tag layer. Implementation of Scope, subscription, and mount comes after this charter; do not scaffold a competing extension framework.

Design context belongs in `CONTEXT.md`, `docs/design.md`, and `docs/adr/`.
