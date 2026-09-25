# GLib 0.18.5 compatibility backport

This is a GYLDLAB-maintained compatibility copy of the published Rust `glib`
0.18.5 crate. It is not an upstream-supported release.

The import is byte-for-byte the crates.io archive with SHA-256
`233daaf6e83ae6a12a52055f568f9d7cf4671dabb78ff9560ab6da230ce00ee5`.
Its original source commit is
`42b9caf98e03ded086362d9653ca58fe94dc8658` in `gtk-rs/gtk-rs-core`.
The published, normalized Cargo manifest is retained so the existing registry
versions of the sibling GLib bindings remain unchanged.

The only Rust source change is the two-line correction from
[upstream PR 1343](https://github.com/gtk-rs/gtk-rs-core/pull/1343), addressing
[RUSTSEC-2024-0429](https://rustsec.org/advisories/RUSTSEC-2024-0429.html).
The MIT license and upstream copyright notices are retained.

Consumers must pin an immutable Git revision. The package version remains
0.18.5 for compatibility; a version-based advisory scanner may still report it.
This patch addresses only the named advisory and does not establish that the
unsupported release line is free of other defects.

Keld tracks qualification and removal of this compatibility copy in KEL-201.
Remove the override when a supported Tao/Wry/WebKit dependency graph using a
fixed GLib release passes Keld's Linux functional and platform acceptance gates.
