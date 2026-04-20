# `esp-generate`

[`esp-generate`][esp-generate] is a project generation tool that assists users in creating a functional project with most of their desired configurations pre-applied.

## Installation

To install `esp-generate`:

```shell
cargo install esp-generate --locked
```

You can also directly download pre-compiled [release binaries][release-binaries] or use [`cargo-binstall`][cargo-binstall].

## What `esp-generate` Сonfigures

`esp-generate` provides more than dependency selection: it applies a known set of crates and feature combinations corresponding to the chosen template options, reducing the amount of manual configuration required to produce a working project.

When options are selected for the template, `esp-generate` updates the generated `Cargo.toml` with the crates and Cargo features those choices require. The templates aim to keep that list as short as practical while still creating a skeleton of an applications that builds and runs for the selected profile, without the need to manually configure the dependencies for the first successful build.

The [Ancillary Crates](../../introduction/ancillary-crates.md) chapter describes how wireless, async, and networking choices map onto individual crates when that level of detail is needed.

Some options have coupled configurations. Logging is configured either via `defmt` or `log` with a corresponding frontend. Certain crates are also included as part of the standard baseline because they support common embedded workflows. For example, `esp-bootloader-esp-idf` includes additional support of 2nd stage bootloader, and `critical-section` is included because many embedded crates rely on it to implement interrupt-critical regions.

> [!TIP]
> Each version of `esp-generate` targets a specific version of the ecosystem crates. Make sure to update `esp-generate` if you want to use the latest released versions.

[release-binaries]: https://github.com/esp-rs/esp-generate/releases
[cargo-binstall]: https://github.com/cargo-bins/cargo-binstall
[esp-generate]: https://github.com/esp-rs/esp-generate
