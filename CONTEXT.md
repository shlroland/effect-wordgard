# Effect Wordgard

Effect Wordgard is a thin Effect-managed runtime around Wordgard. It exists to make GardState lifecycle, dependencies, and view mounting explicit without replacing Wordgard's document, change, facet, or command model.

## Language

**Effect-powered Wordgard runtime**:
A runtime layer that uses Effect to manage Wordgard lifecycle, dependencies, and view mounting while preserving Wordgard's native document and extension model.
_Avoid_: Effect ProseMirror, Wordgard replacement, second extension system

**GardState**:
Wordgard's document, selection, and configuration value. The runtime observes and mounts it; it does not own a parallel document store.
_Avoid_: EditorState, Editing Core, controlled document state

**Wordgard View**:
The mounted `Wordgard` UI component bound to one DOM parent. It displays a GardState and translates user interaction into transactions.
_Avoid_: EditorView, Editor Instance as a ProseMirror handle

**Editor Scope**:
The Effect lifecycle boundary owned by one runtime handle and inherited by its mounted Wordgard View. Resources inside the Editor Scope end when the handle is destroyed, not when a View is unmounted.
_Avoid_: App runtime, global editor runtime, Wordgard plugin state

**State Subscription**:
A synchronous listener registration on the runtime handle that notifies after each accepted GardState change. It observes without owning, transforming, or dispatching.
_Avoid_: React state store, polling, transaction interceptor

**Editor Mount**:
The operation that binds a live GardState handle to one DOM parent and creates the sole active Wordgard View.
_Avoid_: Wordgard.create as Core construction, attach view

**Editor Unmount**:
The idempotent operation that destroys the active Wordgard View without destroying the Editor Scope or the current GardState.
_Avoid_: Core destroy, editor reset

**Editor Destroy**:
The irreversible operation that ends the Editor Scope and invalidates the runtime handle.
_Avoid_: View-only unmount

**Facet**:
Wordgard's native extension point. The runtime never wraps, re-merges, or re-exports Facets as a second contribution model.
_Avoid_: Extension.union, Plugin contribution, Command Tag

**Thin Runtime**:
The v1 scope: Editor Scope, Layer-provided services, State Subscription, and mount/unmount/destroy. Schema elements, commands, keymaps, and Facets stay Wordgard's.
_Avoid_: Typed command surface, Action Reentry, NodeView adapter, schema merge
