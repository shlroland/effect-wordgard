# Effect Wordgard Design Draft

## Goal

Give Effect applications a scoped, mountable handle around Wordgard's `GardState` without replacing Wordgard's document, change, facet, or command model.

## Non-goals

- Do not wrap Facets, schema elements, commands, or keymaps in an Effect contribution model.
- Do not port `effect-prosemirror` Extension, Command Tag, or NodeView APIs.
- Do not make Wordgard commands asynchronous.
- Do not implement Action Reentry in v0.
- Do not implement a React adapter in v0.
- Do not share a codebase or glossary with `effect-prosemirror`.

## Relationship to Effect ProseMirror

`effect-prosemirror` remains the production Effect runtime on ProseMirror. This package is a parallel track on Wordgard. Ideas may be analogous (Scope, subscription, mount) but the vocabulary and implementation stay separate.

## v0 surface

```ts
EditingHandle.make(options)
EditingHandle.create(options)
EditingHandle.subscribe(listener)
Editor.mount(handle, parent)
handle.unmount()
handle.destroy()
```

Wordgard configuration (`config: Extension[]`, schema elements, commands) is passed through unchanged.
