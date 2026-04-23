# `esp-generate`

[`esp-generate`][esp-generate] 是一个项目生成工具，可帮助用户创建功能齐全的项目，并将大部分所需配置预先应用。

## 安装

要安装 `esp-generate`：

```shell
cargo install esp-generate --locked
```

你也可以直接下载预编译的[发布二进制文件][release-binaries]或使用 [`cargo-binstall`][cargo-binstall]。

## `esp-generate` 配置的内容

`esp-generate` 提供的不仅仅是依赖项选择：它会应用一组与所选模板选项对应的已知包和特性组合，从而减少产生可工作项目所需的手动配置量。

当为模板选择选项时，`esp-generate` 会用这些选择所需的包和 Cargo 特性更新生成的 `Cargo.toml`。模板旨在尽可能缩短该列表，同时仍为所选配置文件创建可构建和运行的应用程序骨架，无需为第一次成功构建手动配置依赖项。

[辅助包](../../introduction/ancillary-crates.md)章节详细介绍了无线、异步和网络选择如何映射到各个包，当需要这种详细程度时。

某些选项有耦合配置。日志记录通过 `defmt` 或 `log` 及相应的前端进行配置。某些包也作为标准基线的一部分包含，因为它们支持常见的嵌入式工作流程。例如，`esp-bootloader-esp-idf` 包含第二阶段引导加载程序的额外支持，`critical-section` 被包含是因为许多嵌入式包依赖它来实现中断临界区。

> [!TIP]
> 每个版本的 `esp-generate` 都针对生态系统包的特定版本。如果你想使用最新发布的版本，请确保更新 `esp-generate`。

[release-binaries]: https://github.com/esp-rs/esp-generate/releases
[cargo-binstall]: https://github.com/cargo-bins/cargo-binstall
[esp-generate]: https://github.com/esp-rs/esp-generate
