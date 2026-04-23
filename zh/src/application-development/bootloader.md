# 应用程序启动与引导加载程序

上电后，许多嵌入式设备会直接开始执行闪存（Flash）中某个地址的代码。Espressif 芯片稍微复杂一些，需要一些步骤来设置闪存、缓存和一些其他杂项操作。为此，我们需要一个引导加载程序（Bootloader），它是一个简单的应用程序，设置上述操作，然后跳转到执行其他代码。

要启动应用程序，Espressif 设备使用 2 个引导加载程序：

- 第一阶段引导加载程序（ROM 引导加载程序）：设置架构特定的寄存器，检查[启动模式][boot-mode]和复位原因，并加载第二阶段引导加载程序。该引导加载程序烧录在 ROM 中，作为 SoC 的一部分存在，因此不需要烧录，也无法更改。
- 第二阶段引导加载程序：加载你的应用程序并设置内存（RAM、PSRAM 或闪存）。

第二阶段引导加载程序虽然不是_技术上_必需的，但建议使用，因为它支持 OTA（第一阶段引导加载程序只能从闪存中的固定偏移量加载应用程序），并启用闪存加密和安全启动。有关更多信息，请参阅 [OTA 章节](./ota.md)。

有关启动过程的更多信息，请查看 [ESP-IDF 文档][esp-idf-startup]。但是，请注意某些方面可能是 ESP-IDF 特定的。

[boot-mode]: https://docs.espressif.com/projects/esptool/en/latest/esp32c6/advanced-topics/boot-mode-selection.html?highlight=boot%20mode
[esp-idf-startup]: https://docs.espressif.com/projects/esp-idf/en/stable/esp32c6/api-guides/startup.html

## 第二阶段引导加载程序

目前，仅支持 ESP-IDF 引导加载程序作为第二阶段引导加载程序，未来会随着我们计划添加对其他引导加载程序的支持而改变，例如 [MCUBOOT]。

### ESP-IDF 引导加载程序

使用 [ESP 镜像格式][esp-image-format]，更多信息请参阅 [ESP-IDF 文档][esp-idf-second-stage-bootloader]。ESP-IDF 引导加载程序与分区表一起使用，以了解将二进制文件放置在何处。

[esp-idf-second-stage-bootloader]: https://docs.espressif.com/projects/esp-idf/en/stable/esp32c6/api-guides/startup.html#second-stage-bootloader

#### 分区表

Espressif 设备的闪存可以存储多个应用程序以及各种类型的数据，例如校准数据、文件系统和参数存储。为了管理这些，分区表被烧录在设备的默认偏移量处。

ESP-IDF 第二阶段引导加载程序通过查看分区表来了解将二进制文件放置在何处。分区表中的每个条目都有一个名称（标签）、类型（`app`、`data` 或其他）、子类型和在闪存中加载分区的偏移量。

使用 [`espflash`][espflash] 时，如果你不提供第二阶段引导加载程序或分区表，`espflash` 将使用默认的引导加载程序和分区表，但你也可以创建[自定义分区表][custom-partition-table]。


[esp-image-format]: https://docs.espressif.com/projects/esptool/en/latest/esp32/advanced-topics/firmware-image-format.html
[espflash]: ../getting-started/tooling/espflash.md
[custom-partition-table]: https://docs.espressif.com/projects/esp-idf/en/stable/esp32c6/api-guides/partition-tables.html#creating-custom-tables

#### 构建自定义 ESP-IDF 引导加载程序

`espflash` 和 `cargo-espflash` 包含使用默认设置预编译的 ESP-IDF [引导加载程序][bootloaders]，无需额外配置即可轻松入门。但是，如果你需要更高级的功能或自定义设置，则需要自己构建引导加载程序以满足你的特定需求。

构建自定义 ESP-IDF 引导加载程序：
1. [安装 ESP-IDF][esp-idf-install]。
2. 创建一个新项目或进入已有的项目。
   - 使用 `esp-idf/examples` 目录下的任何示例是最简单的方法。
3. 使用 `idf.py menuconfig` 或编辑 `sdkconfig` 文件来进行所需的引导加载程序更改。
   - 有关更多信息，请参阅[配置选项参考][config-reference]。
4. 使用 `idf.py set-target <CHIP_TARGET> build bootloader` 构建引导加载程序。
   - 生成的引导加载程序二进制文件将放置在 `build/bootloader/bootloader.bin` 下。
5. 在 `espflash/cargo-espflash` 中使用构建的引导加载程序二进制文件，使用 `--bootloader` 标志或[配置文件][espflash-config-file]。


[bootloaders]: https://github.com/esp-rs/espflash/tree/main/espflash/resources/bootloaders
[esp-idf-install]: https://docs.espressif.com/projects/esp-idf/en/stable/esp32/get-started/index.html#manual-installation
[config-reference]: https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/kconfig-reference.html#configuration-options-reference
[espflash-config-file]: https://github.com/esp-rs/espflash/tree/main/espflash#configuration-file
[MCUBOOT]: https://docs.mcuboot.com/
