# Runtime Does Not Wrap Facets

Status: Accepted.

Effect Wordgard is a thin lifecycle runtime around Wordgard, not a second extension framework. Schema elements, commands, keymaps, and Facets are configured with Wordgard's native APIs. The runtime may require Effect services and expose Scope, subscription, and mount operations; it does not introduce `Extension.union`, Command Tags, or contribution merge.

Wrapping Facets would fight Wordgard's composition model and duplicate work already done in `effect-prosemirror`. Action Reentry and a typed command surface are deferred until a later phase proves they are needed on top of Wordgard changes.
