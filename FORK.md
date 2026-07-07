# About this fork

This repository is a fork of [rsmpi/rsmpi](https://github.com/rsmpi/rsmpi),
the MPI bindings for Rust. It exists for one reason: to get a fix that is
already merged upstream published to [crates.io](https://crates.io) sooner
than upstream has cut a release.

## Why the fork exists

Upstream merged a fix for a compilation failure against **OpenMPI 5**
(bumping `bindgen`, see upstream commit `4f3e7ef` / PR #223). That fix is on
`main` upstream but has **not yet been published to crates.io** — the latest
released `mpi` there is still `0.8.1`, which does not build against OpenMPI 5.

Our projects need that fix now, so rather than wait for the next upstream
release we publish our own crates from this fork.

## What we changed

To publish to crates.io without colliding with the upstream packages, the
**package names** were renamed:

| Upstream package (crates.io) | This fork publishes as |
| ---------------------------- | ---------------------- |
| `mpi`                        | `proofman-mpi`         |
| `mpi-sys`                    | `proofman-mpi-sys`     |

The **importable library names are unchanged** (`mpi` and `mpi_sys`). This is
done via an explicit `[lib] name = ...` in each crate's `Cargo.toml`, so
consuming code does not have to change:

```rust
use mpi::traits::*; // still works
```

You only change how you *depend* on the crate:

```toml
# Instead of:
# mpi = "0.8.1"

# use:
mpi = { package = "proofman-mpi", version = "0.8.1" }
```

Aside from the rename, this fork tracks upstream and carries no functional
divergence.

## When this fork goes away

This is a **temporary** fork. Once upstream `rsmpi` publishes a release that
includes the OpenMPI 5 fix, dependents should switch back to the official
`mpi` / `mpi-sys` crates and this fork can be retired.

## Upstream

- Repository: https://github.com/rsmpi/rsmpi
- Crates: [`mpi`](https://crates.io/crates/mpi), [`mpi-sys`](https://crates.io/crates/mpi-sys)

Please direct bug reports and feature requests unrelated to the packaging
rename to the upstream project.
