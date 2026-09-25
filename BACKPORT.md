# GLib 0.18.5 compatibility backport

This is a GYLDLAB-maintained compatibility copy of the published Rust `glib`
0.18.5 crate. It is not an upstream-supported release.

The import is byte-for-byte the crates.io archive with SHA-256
`233daaf6e83ae6a12a52055f568f9d7cf4671dabb78ff9560ab6da230ce00ee5`.
Its original source commit is
`42b9caf98e03ded086362d9653ca58fe94dc8658` in `gtk-rs/gtk-rs-core`.
The published, normalized Cargo manifest is retained so the existing registry
versions of the sibling GLib bindings remain unchanged.

The production changes are the exact accepted upstream corrections from:

- [PR 1343](https://github.com/gtk-rs/gtk-rs-core/pull/1343), addressing
  [RUSTSEC-2024-0429](https://rustsec.org/advisories/RUSTSEC-2024-0429.html).
- [PR 1491](https://github.com/gtk-rs/gtk-rs-core/pull/1491), initializing the
  terminating pointer on initial allocation in `StrV` and `PtrSlice`.
- [PR 2038](https://github.com/gtk-rs/gtk-rs-core/pull/2038), restoring the empty
  terminator after `StrV::clear()` releases its elements, including its ordinary
  unit test for clear and destruction on the corrected implementation.

The latter two source defects were confirmed to apply to the published 0.18.5
implementation. They preserve signatures, capacity policy and ownership.
Keld application-path reachability is not established by this source review.
The MIT license and upstream copyright notices are retained.

The existing `StrV` test also includes upstream's test-only correction
[`107ad15`](https://github.com/gtk-rs/gtk-rs-core/commit/107ad15cce3a3292c3d5a3a64b09e0017d28275a).
It repairs five invalid slice accesses while preserving every terminator,
length and content assertion. This is required to run the existing test suite
meaningfully on current Rust. This test-only correction leaves the production
implementation unchanged.

Consumers must pin an immutable Git revision. The package version remains
0.18.5 for compatibility; a version-based advisory scanner may still report it.
This copy addresses the named corrections and does not establish that the
unsupported release line is free of other defects.

Keld tracks qualification in KEL-201 and supported replacement in KEL-253.
Remove the override when a supported Tao/Wry/WebKit dependency graph using a
fixed GLib release passes Keld's Linux functional and platform acceptance gates.
