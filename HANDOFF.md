# Handoff: Effect Wordgard track

As of 2026-09-16 (charter commit `3072cbb`). Next session: continue this repository only. Do not implement in `effect-prosemirror`.

GitHub: https://github.com/shlroland/effect-wordgard

## Suggested skills

- **domain-modeling** — any glossary or ADR change; charter lives in `CONTEXT.md` + `docs/adr/`
- **tdd** — first implementation slice (Scope / subscription / mount)
- **find-docs** / Wordgard docs — before inventing APIs; substrate is Wordgard, not ProseMirror
- **grilling** — only if v0 surface or handle naming needs another decision round
- **writing-for-agents** — only if `AGENTS.md` needs a pointer for a new doc

Do not load ProseMirror implementation skills as the default path.

## What this is

Wordgard is Marijn Haverbeke’s 2026 green-field rich-text toolkit (not ProseMirror 2.0). Official: https://wordgard.net/ — announcement: https://marijnhaverbeke.nl/blog/wordgard-0.1.html — 0.x, MIT, no PRs.

`effect-wordgard` is a **thin Effect runtime around Wordgard**. Analogous ideas to `effect-prosemirror` (Scope, subscription, mount) but **separate repo, separate glossary, no shared code**.

Charter already written — read these, do not rewrite:

- `CONTEXT.md`
- `docs/design.md`
- `docs/adr/0001-runtime-does-not-wrap-facets.md`
- `AGENTS.md`

## Settled decisions (do not re-open)

From the effect-prosemirror session; user confirmed these:

1. **Location:** independent public repo `effect-wordgard` (this one). Not a workspace package inside `effect-prosemirror`.
2. **v0 thinness:** Editor Scope, Layer-provided services, State Subscription, mount / unmount / destroy. Schema, Facets, commands, keymaps stay native Wordgard.
3. **Deferred:** Action Reentry, typed Command Tag surface, React adapter, any `Extension.union` clone.
4. **Package name:** `effect-wordgard` (React later as `@effect-wordgard/react` if needed; not day one).
5. **Parallelism:** `effect-prosemirror` stays the production PM runtime. This package does not convert or replace it.

## Why not wrap Facets

Wordgard already has CodeMirror-style facets, independent node/mark types, `Command` identity + handlers, `Command.Pure`, `GardState` (headless) vs `Wordgard.create` (mounted), OT collab. Rebuilding ProseKit-style contributions on top would fight that model. See ADR 0001.

## v0 surface (from design.md — names are draft)

```ts
EditingHandle.make(options)
EditingHandle.create(options)
EditingHandle.subscribe(listener)
Editor.mount(handle, parent)
handle.unmount()
handle.destroy()
```

Wordgard `config` / schema / commands pass through unchanged. `EditingHandle` is **not** an Editing Core; do not import PM vocabulary.

Open naming question (not blocking charter): keep `EditingHandle` vs pick a Wordgard-native name. Grill only if it matters before first tests.

## What is implemented

Charter docs only. No `src/`, no package scaffold, no tests, no Wordgard dependency yet.

## What the sibling PM repo already proved (ideas only)

Do not copy files. Useful *behaviour* to mirror later:

- Core Subscription: `core.subscribe(() => void): () => void` — notify after accepted state, not rejected; selection-only and view-originated included; notify even if view sync fails; dispatch from listener is reentry failure; destroy rejects new subscribe. Commit in PM: `13e967d`.
- React adapter is **out of Wordgard v0**. PM `#6` closed: `@effect-prosemirror/react` with `EditorProvider` / `EditorContent` / `useEditor`. PM next is `#7` `useEditorState` — ignore unless the user switches tracks.

PM wayfinder https://github.com/shlroland/effect-prosemirror/issues/1 already marks Wordgard out of scope.

## Next implementation slice (when the user says start coding)

1. Scaffold `effect-wordgard` as a real package (`package.json`, Effect + `wordgard` deps, Vitest, same engineering gates style as PM if useful).
2. First vertical slice: create a scoped handle around `GardState`, subscribe to accepted updates, destroy invalidates.
3. Second: mount/unmount a Wordgard View on a DOM parent without destroying the handle.
4. Pass Wordgard `config` through; do not add contribution merge.

Read Wordgard guide first: https://wordgard.net/docs/guide/ and https://wordgard.net/docs/prosemirror/

## Constraints for the next agent

- Use Wordgard terms: `GardState`, Facet, Plot, Leaf, ChangeSet, Wordgard View.
- Avoid: Editing Core, EditorState, Command Tag, Extension.union, NodeView adapter, ProseMirror Steps.
- Do not port `effect-prosemirror` source.
- Do not implement React or Actions in v0.
- Wordgard is 0.x and does not accept PRs; design to native seams, do not wait on upstream patches.
