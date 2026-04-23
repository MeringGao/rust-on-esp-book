# 硬件概述

`esp-rs` 组织下的包支持 [ESP32、ESP32-S、ESP32-C 和 ESP32-H 系列 SoC][espressif-socs]。

每个 SoC 都有自己的独特功能，同时共享一些共同特性。要为你的项目选择合适的芯片，请使用 [Espressif 产品选型器][product-selector]。

Espressif 的产品组合基于两种不同的系统架构：

- [Xtensa][xtensa-architecture]：ESP32 和 ESP32-S 系列基于 Xtensa 架构。
- [RISC-V][riscv-architecture]：ESP32-C 和 ESP32-H 系列基于 RISC-V 架构。

我们不会在这里深入介绍这两种架构之间的细节或差异。Rust 对这两种架构的官方支持有所不同。Xtensa 尚未得到 Rust 的官方支持；Rust 不支持 Xtensa 的原因是 Rust 使用 LLVM 作为其编译器基础设施的一部分，而 LLVM 目前还不支持 Xtensa。因此，我们维护了 LLVM 和 Rust 编译器的自定义分支，其中包含 Xtensa 支持，并且我们正在积极努力将这些变更推向上游，以在未来实现官方支持。

> [!NOTE]
> 我们正在积极努力将我们的分支推向上游。以下是当前状态：
>
> 1. LLVM 分支：我们最近取得了重大进展。有关详细信息，请参阅[追踪问题][llvm-github-fork-upstream issue]。
> 2. Rust 编译器分支：我们已提交了所有可行的 Xtensa 补丁。进一步的进展取决于这些变更能否被上游合并到 LLVM 中。

有关不同 SoC 的更多信息，请参阅[技术文档][espressif-docs]。

> [!NOTE]
> ESP8266 不受 `esp-hal` 支持。
>
> 但是，ESP32-C2（ESP8684）和 ESP32-C3（ESP8685）是受支持的。值得注意的是，ESP32-C3 与 ESP8266 引脚兼容，使其成为合适的直接替代方案。

[espressif-socs]: https://www.espressif.com/en/products/socs
[product-selector]: https://products.espressif.com/#/
[xtensa-architecture]: https://www.cadence.com/content/dam/cadence-www/global/en_US/documents/tools/silicon-solutions/compute-ip/isa-summary.pdf
[riscv-architecture]: https://en.wikipedia.org/wiki/RISC-V
[espressif-docs]: https://www.espressif.com/en/support/documents/technical-documents
[llvm-github-fork-upstream issue]: https://github.com/espressif/llvm-project/issues/4

## 了解 Espressif 开发套件

让我们以 [ESP32-C6-DevKitC-1][c6-devkitc] 为例。它是一款基于 ESP32-C6 的开发板，配备：

![ESP32-C6-DevKitC-1](../assets/esp32-c6-devkitc-1-v1.2.png)

- ESP32-C6-WROOM-1 模块：
  - 支持 Wi-Fi、BLE 和 IEEE 802.15.4。
  - 8 MB SPI 闪存（Flash）。
- 可用的 GPIO 引脚。
- 2 个按钮：Boot 和 Reset
  - Boot 按钮：下载按钮。按住 Boot 然后按 Reset 可启动固件下载模式，通过串口下载固件。
    - 有关更多信息，请参阅[启动模式选择][boot-mode-selection]。
  - Reset 按钮：复位设备。
- 2 个 USB-C 端口：
  - USB-C 转 UART 端口：用于为开发板供电、向芯片烧录应用程序，以及通过板载 USB 转 UART 桥接器与 ESP32-C6 芯片通信。
  - USB-C 端口：用于为开发板供电、向芯片烧录应用程序、使用 USB 协议与芯片通信，以及进行 JTAG 调试。
- RGB LED：可寻址 RGB LED，由 GPIO8 驱动。
  - 注意这不是标准的 RGB LED，而是 [WS2812B LED][esp-hal-smartled]。

[c6-devkitc]: https://docs.espressif.com/projects/esp-dev-kits/en/latest/esp32c6/esp32-c6-devkitc-1/index.html
[boot-mode-selection]: https://docs.espressif.com/projects/esptool/en/latest/esp32c6/advanced-topics/boot-mode-selection.html?highlight=boot%20mode
[esp-hal-smartled]: https://github.com/esp-rs/esp-hal-community/tree/main/esp-hal-smartled
