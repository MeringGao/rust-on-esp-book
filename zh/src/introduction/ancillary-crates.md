# 辅助包概述

在详细描述用于编写应用程序的各种包和概念之前，先对整个生态系统有一个初步的了解可能会有所帮助，包括 `esp-hal` 意义上的生态系统和更广泛的嵌入式 Rust 意义上的生态系统。

## `esp-hal` 生态系统

开始一个项目的第一步是创建它，主要方式是使用 `esp-generate`。在本书的[专门章节](../getting-started/tooling/esp-generate.md)中可以阅读更多关于这个工具的信息。

将 Espressif 芯片与 Rust 结合使用的核心包是 `esp-hal`。通过它，你将能够执行芯片的基本初始化，以及访问芯片上可用的外设（Peripheral）的驱动程序。选定芯片的完整 [`esp-hal` 文档]将明确提供关于哪些外设可用以及各自驱动程序稳定性的信息。

此外，你可能希望使用芯片的更高级功能。例如，网络和连接。生态系统的这一部分由 `esp-radio` 负责，它组合了 Espressif 产品中一个或多个可用的通信协议的驱动程序：`Wi-Fi`、`BLE`、`esp-now` 和通信底层的 `IEEE 802.15.4`。每个芯片的详细信息可在 [`esp-radio` 子仓库]中找到。还值得一提的是，无线支持需要协议栈在后台持续运行（定时器、中断、状态机）。`esp-radio` 依赖 [`esp-radio-rtos-driver`] 的实现，该实现定义了协议栈可靠运行所需的调度和运行时接口。`esp-rtos` 是我们提供和支持的默认后端；原则上，用户可以自由地用该驱动程序的另一个实现来替换它。当你启用适当的模板选项时，`esp-generate` 会自动添加 `esp-rtos`。

如需更高级的芯片内存操作，并在 `no_std` 中使用 `alloc` 包中需要堆分配的集合，欢迎使用 `esp-alloc`。本书中有一个专门的[章节](./../application-development/alloc.md)介绍此内容。

下表简要描述了 `esp-hal` 生态系统中的所有包及其用途：

| 包                    | 描述                                                                                                    |       稳定性       |
| ------------------------ | -------------------------------------------------------------------------------------------------------------- | --------------------- |
| `esp-alloc`              | 内存分配工具。                                                                                   | 不稳定              |
| `esp-backtrace`          | 提供回溯支持。                                                                                   | 不稳定              |
| `esp-bootloader-esp-idf` | 为 ESP-IDF 第二阶段引导加载程序提供额外支持，包括 OTA。                                 | 不稳定              |
| `esp-build`              | 用于 esp-hal 和其他相关包的构建工具，旨在用于构建脚本中。            | 不稳定              |
| `esp-config`             | 配置系统。                                                                                          | 不稳定              |
| `esp-hal`                | 适用于所有 Espressif ESP32 设备的裸机（`no_std`）HAL。                                                     | 稳定<sup>*</sup>    |
| `esp-hal-proc-macros`    | 用于 esp-hal 系列 HAL 包的过程宏。                                             | 不稳定              |
| `esp-lp-hal`             | 适用于某些 Espressif 设备中低功耗和超低功耗核心的裸机（`no_std`）HAL。         | 不稳定              |
| `esp-metadata`           | Espressif 设备的元数据，主要用于构建脚本。                                   | 不稳定              |
| `esp-preempt`            | 线程和线程感知同步原语，主要用于 `esp-radio`。                         | 不稳定              |
| `esp-println`            | Espressif 设备的打印和日志功能。                                                         | 不稳定              |
| `esp-riscv-rt`           | 适用于 Espressif RISC-V CPU 的最小启动/运行时。                                                        | 不稳定              |
| `esp-rom-sys`            | ROM 代码支持。                                                                                              | 不稳定              |
| `esp-rtos`               | 用于 esp-radio 的调度器实现，支持 `esp-hal` 的 embassy。                                         | 不稳定              |
| `esp-sync`               | Espressif 设备的同步原语。                                                              | 不稳定              |
| `esp-storage`            | Espressif 设备的存储工具。                                                               | 不稳定              |
| `esp-radio`              | Espressif 设备的 Wi‑Fi、BLE、IEEE 802.15.4 和 ESP‑NOW 功能。                                    | 不稳定              |
| `xtensa-lx`              | 对 Xtensa LX 处理器和外设的低层访问。                                                      | 不稳定              |
| `xtensa-lx-rt`           | 适用于 Espressif Xtensa LX CPU 的最小启动/运行时。                                                     | 不稳定              |

> [!NOTE]
> `esp-hal` 中各个外设驱动程序的稳定性各不相同。请参阅[外设支持部分][peripheral-support]了解每个外设的稳定性详情。

你可以在 [esp-rs 文档][docs]中找到关于这些包的详细信息。

[docs]: https://docs.espressif.com/projects/rust/index.html
[peripheral-support]: https://github.com/esp-rs/esp-hal/tree/main/esp-hal#peripheral-support

## 嵌入式 Rust 生态系统集成

嵌入式 Rust 环境中最流行的硬件抽象层是 [`embedded-hal`]，它为多个外设提供了一系列特质（Trait），允许编写与 HAL 无关的设备驱动程序。`esp-hal` 在其驱动程序中实现了这些特质。此外，还实现了嵌入式 Rust 行业中不同包使用的各种特质，例如用于随机数生成器（RNG）外设的 [`rand_core`] 特质，以及 [`embedded-io`] 特质，它们是 `no_std` 应用程序中 `std::io` 特质的类似物。

[`esp-hal` documentation]: https://docs.espressif.com/projects/rust/esp-hal/latest/
[`esp-radio` sub-repository]: https://github.com/esp-rs/esp-hal/tree/main/esp-radio
[`esp-radio-rtos-driver`]: https://github.com/esp-rs/esp-hal/tree/main/esp-radio-rtos-driver
[`embedded-hal`]: https://docs.rs/embedded-hal/latest/embedded_hal/index.html
[`rand_core`]: https://crates.io/crates/rand_core
[`embedded-io`]: https://crates.io/crates/embedded-io
