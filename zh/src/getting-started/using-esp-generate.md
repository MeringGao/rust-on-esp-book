# 使用 `esp-generate`

所有必要工具安装完成后，你就可以创建第一个在 Espressif 芯片上运行的 Rust 项目了。

## 生成项目

首先，通过运行以下命令启动交互式配置工具：

```shell
esp-generate
```

`esp-generate` 会提示你选择芯片和项目名称，然后启动一个 TUI，其中包含配置项目生成过程的选项。

![截图](../assets/esp-generate.png)

根据你的项目需要调整选项。请参阅 README 中的[可用选项][available-options]部分。TUI 底部有每个选项的简短描述。

[available-options]: https://github.com/esp-rs/esp-generate?tab=readme-ov-file#available-options

## 烧录选项

有两种将代码烧录到目标设备的选项：

- `espflash`：默认烧录工具。
- `probe-rs`：启用基于实时传输（RTT）的选项，并允许芯片内调试。
  - 在生成项目时，确保启用 `Use probe-rs to flash and monitor instead of espflash.`（`probe-rs` 选项）。

> [!TIP]
> 使用 `espflash` 时，你可能希望在 `Flashing, logging and debugging (espflash)` 下启用 `Use the log crate to print messages.` 和 `Use esp-backtrace as the panic handler.`

> [!TIP]
> 使用 `probe-rs` 而不是 `espflash` 时，你可能希望在 `Flashing, logging and debugging (probe-rs)` 下启用 `Use defmt to print messages.` 和 `Use panic-rtt-target as the panic handler.`

## 生成项目

准备就绪后，你可以在 TUI 的根目录按 `s` 生成项目。保存项目时，工具会检查所需和可选工具是否已安装并显示结果，这可能包括要求你安装可能遗漏的任何工具，或根据生成选项现在需要的工具。

## 运行代码

让你的代码运行起来非常简单，只需执行：

```shell
cargo run --release
```

此命令会编译你的应用程序，将其烧录到目标设备，并开始监控日志输出。

🎉 恭喜你——你已成功将第一个 Rust 程序烧录到 ESP32 上！

你现在已准备好深入使用 Rust 在 ESP32 平台上进行开发。
