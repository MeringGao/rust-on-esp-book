## 工具链安装

### Rust 安装

确保你已安装 [Rust][rust-lang-org]。如果没有，请参阅 [rustup][rustup.rs-website] 网站上的说明。

> [!WARNING]
> 在基于 Unix 的系统上，通过系统包管理器（例如 `brew`、`apt`、`dnf` 等）安装 Rust 可能会导致各种[问题和兼容性冲突][rustup-note]，因此最好使用 [rustup][rustup.rs-website]。

在 Windows 上使用时，请确保你已安装以下列出的 ABI 之一。有关更多详细信息，请参阅 rustup 书中的 [Windows][rustup-book-windows] 章节。

- **MSVC**：推荐的 ABI，包含在 `rustup` 默认需求列表中。用于与 Visual Studio 生成的软件互操作。

    如果不确定，请使用此选项。

- **GNU**：GCC 工具链使用的 ABI。如果你需要与使用 MinGW/MSYS2 工具链构建的软件互操作，请自行安装。

另请参阅[替代安装方法][rust-alt-installation]。

[rustup-note]: https://rust-lang.github.io/rustup/installation/other.html#using-a-package-manager
[rustup.rs-website]: https://rustup.rs/
[rust-alt-installation]: https://rust-lang.github.io/rustup/installation/other.html
[rustup-book-windows]: https://rust-lang.github.io/rustup/installation/windows.html
[rust-lang-org]: https://www.rust-lang.org/

### RISC-V 设备

要为基于 RISC-V 架构的 Espressif 芯片构建 Rust 应用程序（如果你不确定你的设备是什么，请参阅[硬件概述](../introduction/hardware-overview.md)），请执行以下操作：

1. 使用 `rust-src` [组件][rustup-book-components]安装正确的工具链：

   - 你可以使用 `stable` 或 [`nightly`][rustup-book-channel-nightly]：
     ```shell
     rustup toolchain install stable --component rust-src
      ```
      或
      ```shell
     rustup toolchain install nightly --component rust-src
     ```

   > [!NOTE]
   > 其他组件（如 `rustfmt`、`clippy` 或 `rust-analyzer`）不是必需的，但强烈推荐安装。

2. 安装目标：

   ```shell
   rustup target add riscv32imc-unknown-none-elf # 适用于 ESP32-C2 和 ESP32-C3
   rustup target add riscv32imac-unknown-none-elf # 适用于 ESP32-C6 和 ESP32-H2
      ```

      这些目标目前是 [Tier 2][rust-lang-book--platform-support-tier2]。注意 Rust 中 `riscv32` 目标的不同变体涵盖了不同的 [RISC-V 扩展][wiki-riscv-standard-extensions]。

如果你_不_打算使用 ESP32、ESP32-S2 或 ESP32-S3，那么你已经完成，可以跳到[工具安装](tooling/index.md)。

[rustup-book-channel-nightly]: https://rust-lang.github.io/rustup/concepts/channels.html#working-with-nightly-rust
[rustup-book-components]: https://rust-lang.github.io/rustup/concepts/components.html
[rust-lang-book--platform-support-tier2]: https://doc.rust-lang.org/nightly/rustc/platform-support.html#tier-2
[wiki-riscv-standard-extensions]: https://en.wikichip.org/wiki/risc-v/standard_extensions

### Xtensa 设备

如[硬件概述](../introduction/hardware-overview.md)中所述，ESP32、ESP32-S2 和 ESP32-S3 基于 Xtensa 架构。如果你要针对这些芯片，目前需要使用 Rust 编译器的分支。

[`espup`][espup-github] 是一个简化安装和维护开发这些目标所需工具链的工具。

1. 安装 `espup`：
    ```shell
    cargo install espup --locked
    ```
   你也可以直接下载预编译的[发布二进制文件][release-binaries]或使用 [`cargo-binstall`][cargo-binstall]。
2. 通过运行以下命令安装所有支持的 Espressif 目标所需的所有工具链：
    ```shell
    espup install
    ```
3. 在 Unix 系统上，设置环境变量：请参阅 [`espup` 自述文件][source-file-espup]中的不同方法。Windows 用户无需执行其他操作。

[espup-github]: https://github.com/esp-rs/espup
[release-binaries]: https://github.com/esp-rs/espup/releases
[cargo-binstall]: https://github.com/cargo-bins/cargo-binstall
[source-file-espup]: https://github.com/esp-rs/espup?tab=readme-ov-file#environment-variables-setup

#### `espup` 安装的内容

为了支持 Espressif 目标，`espup` 会安装：

- [Espressif Rust 分支][esp-rs/rust]，支持 Espressif 目标
- 支持 RISC-V 目标的 `stable` 工具链
- 支持 Xtensa 目标的 LLVM [分支][llvm-github-fork]
- [GCC 工具链][gcc-toolchain-github-fork]，用于链接最终二进制文件

分支编译器可以与标准 Rust 编译器共存，允许两者都安装在你的系统上。当使用任何可用的[覆盖方法][rustup-overrides]时，会调用分支编译器。

[esp-rs/rust]: https://github.com/esp-rs/rust
[llvm-github-fork]: https://github.com/espressif/llvm-project
[gcc-toolchain-github-fork]: https://github.com/espressif/crosstool-NG/
[rustup-overrides]: https://rust-lang.github.io/rustup/overrides.html
