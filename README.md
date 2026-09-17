# Effect Wordgard

Thin Effect-managed runtime around [Wordgard](https://wordgard.net).

This repository is a charter and design track. It is not a ProseMirror adapter and it does not replace [`effect-prosemirror`](https://github.com/shlroland/effect-prosemirror).

v0 will own lifecycle only: Effect Scope, service Layers, GardState subscription, and view mount/unmount/destroy. Schema, Facets, and commands stay native Wordgard APIs.

See [HANDOFF.md](./HANDOFF.md) to continue this track, plus [CONTEXT.md](./CONTEXT.md), [docs/design.md](./docs/design.md), and [docs/adr/0001-runtime-does-not-wrap-facets.md](./docs/adr/0001-runtime-does-not-wrap-facets.md).
