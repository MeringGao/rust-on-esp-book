# 空中升级（OTA）

空中升级（Over The Air Updates，OTA）是指_无需_生产烧录工具即可更新应用程序的能力。OTA 严重依赖引导加载程序来处理 OTA 镜像（固件更新）的切换、替换和回滚。对于每个我们支持的引导加载程序，我们都有一个引导加载程序支持包，由于目前我们只支持 ESP-IDF 引导加载程序，所以我们只有 [`esp-bootloader-esp-idf`] 包。

我们在 `esp-hal` 仓库中有一个[小型 OTA 示例]。这个示例很基础，但展示了使 OTA 功能工作的构建块。请务必查看文档，因为该示例还提供了使用 `espflash` 创建 OTA 二进制文件的说明。


[`esp-bootloader-esp-idf`]: https://github.com/esp-rs/esp-hal/blob/main/esp-bootloader-esp-idf
[small OTA example]: https://github.com/esp-rs/esp-hal/tree/main/examples/ota
