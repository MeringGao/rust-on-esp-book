# 常见问题解答

本章解决了开发人员在 ESP 芯片上使用 Rust 时可能遇到的常见问题和挑战。无论你是正在设置开发环境、优化代码，还是希望模拟项目，你都可以在这里找到实用的解决方案和最佳实践。

## 编辑器/IDE

使用 [`esp-generate`][esp-generate] 时，你可以在生成过程中自动配置 VS Code、Helix、Neovim 和 Zed 编辑器的推荐设置和扩展。

[esp-generate]: ./getting-started/tooling/esp-generate.md

## 大小和内存优化

### 优化二进制大小

- Cargo 提供了一些默认的配置；我们建议使用 [`release` 配置][release-profile]，因为它会进行优化并移除调试符号。
- Cargo 允许不同的[配置设置][profile-settings-cargo]，这可能会对最终产物的大小产生影响。
  - 请参阅 The Embedded Rust Book 中的[优化：速度与大小的权衡][embedded-book-tradeoffs]。
- 使用外部依赖时要小心，因为它们可能会增加最终产物的大小。
- 如果日志消息不会被使用或阅读，请过滤掉它们。
- 更多建议可以在 [min-sized-rust][min-sized-rust] 仓库中找到。

此外，[Embassy 文档][embassy-documentation] 在[常见问题][frequently-asked-questions]部分包含了一些关于二进制大小的建议。

[embedded-book-tradeoffs]: https://docs.rust-embedded.org/book/unsorted/speed-vs-size.html
[release-profile]: https://doc.rust-lang.org/cargo/reference/profiles.html#release
[profile-settings-cargo]: https://doc.rust-lang.org/cargo/reference/profiles.html#profile-settings
[min-sized-rust]: https://github.com/johnthagen/min-sized-rust
[embassy-documentation]: https://embassy.dev/book
[frequently-asked-questions]: https://embassy.dev/book/#_frequently_asked_questions

### 优化内存使用

我们再次参考 [Embassy 文档][embassy-documentation]，特别是[如何测量资源使用情况（CPU、RAM 等）？][measure-resources]部分。

[measure-resources]: https://embassy.dev/book/#_how_can_i_measure_resource_usage_cpu_ram_etc

## 使用 Git 中的包

[Cargo Book][cargo-book] 和 [Embassy 文档][embassy-documentation] 都包含有关如何从 Git 仓库指定依赖项的信息：

- [从 `git` 仓库指定依赖项][dependencies-from-git]
- [`[patch]` 部分][patch-section]
- [如何切换到 `main` 分支][switch-to-main-branch]

[cargo-book]: https://doc.rust-lang.org/cargo/
[dependencies-from-git]: https://doc.rust-lang.org/cargo/reference/specifying-dependencies.html#specifying-dependencies-from-git-repositories
[patch-section]: https://doc.rust-lang.org/cargo/reference/overriding-dependencies.html#the-patch-section
[switch-to-main-branch]: https://embassy.dev/book/#_how_do_i_switch_to_the_main_branch

## 我可以在驱动程序上使用 `mem::forget` 吗？

应避免使用 `mem::forget` 函数，因为遗忘驱动程序可能会导致非预期的后果。外设驱动程序提供 `Drop` 实现，将外设返回到其默认的未配置状态，并在必要时取消任何当前正在进行的直接内存访问（DMA）事务。遗忘驱动程序可能会导致外设配置错误和/或 DMA 事务无限期运行且永不完成。

## 进入/退出下载模式

下载模式是一种用于固件编程和调试的启动模式。在此模式下，芯片不会从闪存启动应用程序，而是等待通过 UART 或 USB 等接口接收新的固件数据，并将其写入闪存。

### 选择启动模式

当复位发生时，ROM 引导加载程序读取特定绑定引脚（Strapping Pin）的状态，并根据复位时刻的电平选择启动模式：
- 如果启动绑定引脚为高电平 → 芯片进入 SPI 启动模式（从闪存运行应用程序）。
- 如果启动绑定引脚为低电平 → 芯片进入下载模式（等待固件）。
有关启动模式选择的更多信息，请参阅 [ESP-IDF 文档][esp-idf-bootmode]

当设备处于下载模式时，你会看到以下串口输出："waiting for download"。请参阅 [ESP-IDF 下载模式文档][esp-idf-downloadmode]

烧录芯片后，芯片需要返回到 SPI 启动模式以运行新固件。这可以通过复位目标来实现，导致绑定引脚被重新采样，芯片正常启动；或者在 USB-Serial/JTAG 模式下使用 `espflash` 和 `esptool` 的 `--after watchdog-reset` 选项，请参阅 [ESP-IDF 故障排除][esp-idf-troubleshooting]。

[esp-idf-bootmode]: https://docs.espressif.com/projects/esptool/en/latest/esp32c6/advanced-topics/boot-mode-selection.html
[esp-idf-downloadmode]: https://docs.espressif.com/projects/esp-techpedia/en/latest/esp-friends/get-started/try-firmware/try-firmware-troubleshooting.html#download-mode
[esp-idf-troubleshooting]: https://docs.espressif.com/projects/esptool/en/latest/esp32c6/troubleshooting.html#leaving-download-mode-in-usb-serial-jtag-mode
