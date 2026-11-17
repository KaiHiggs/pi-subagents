# Fork: operator-directed workspace coordination

This branch is based on upstream `v0.86.0`, matching the version of the separately installed plugin.
It removes the blanket writer-count/isolation instruction from the model-facing tool description and the
bundled delegation guidance. Workspace layout and resource coordination belong to the operator/project contract.
It adds no implicit shared-write permissions, locks, scheduling rules, or new execution mode.

The operator-requested delegation gate, native async-wake guidance and failure-reporting safeguards remain.
Custom descriptions may request serialized writing; the fork simply stops imposing it universally.

## Verification

- Focused description tests: 16 passed, including default/full/compact/custom modes and explicit serialized choice.
- Full unit suite: 4,355 passed, 17 skipped, zero failures.
- Integration suite: 1,307 passed, 10 skipped, zero failures.
- Typecheck and package build pass. The built extension is checked, not only TypeScript source.

## Installation is separate

This fork has not replaced the active plugin. That installation has xcomms-specific native-host patches and
hash-pinned checks; preserve and verify those before any replacement. Upstream `v0.86.0` is not by itself a copy
of those locally patched runtime files.

Tool declarations may remain pinned in resumed sessions. Editing a skill or source file does not establish
that a running model received new instructions. A supported package update plus a deliberate new-session or
documented declaration-refresh step is required before treating the new policy as active.

The local `route-subagent-models-at-runtime` skill, outside this repository, also contains a legacy one-writer
reference. It was not modified here and should be reconciled during an explicitly authorized deployment.
