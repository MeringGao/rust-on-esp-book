# `esp-config`（可选）

[`esp-config`][esp-config] 是一个通过 TUI 编辑配置选项的工具。使用它完全是可选的，请参阅[配置章节][config-chapter]了解配置文件的组织方式以及如何在不使用 TUI 的情况下手动编辑它们。

[config-chapter]: ../../application-development/configuration.md

## 安装

要安装 `esp-config`：

```shell
cargo install esp-config --features=tui --locked
```

[esp-config]: https://github.com/esp-rs/esp-hal/tree/main/esp-config
