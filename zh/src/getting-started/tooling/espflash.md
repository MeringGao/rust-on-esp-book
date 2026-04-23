# `espflash`

[`espflash`][espflash] 是一个专为 Espressif SoC 和模块设计的串口烧录工具。它原生支持所有与 `esp-hal` 兼容的芯片。

## 安装

要安装 [`espflash`][espflash]，请执行以下命令：

```shell
cargo install espflash --locked
```

或者，你可以使用 [`cargo-binstall`][cargo-binstall] 从[发布页面]下载预编译产物并使用它们：

```bash
cargo binstall espflash
```

> [!NOTE]
> [`espflash`][espflash] 使用的默认波特率是 115200——你可能想提高它以加快烧录速度。
> 最简单的方法是设置 `ESPFLASH_BAUD` 环境变量。

[cargo-binstall]: https://github.com/cargo-bins/cargo-binstall
[releases]: https://github.com/esp-rs/espflash/releases
[espflash]: https://github.com/esp-rs/espflash/tree/main/espflash/
