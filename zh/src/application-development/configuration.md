# 配置

[`esp-config`][esp-config] 包为 `esp-*` 包提供了一种管理不适合 Cargo 特性的额外配置设置的方式。

## 查找可用配置

完整选项列表可以在你感兴趣的包的[文档]中找到。例如，这些是 [`esp-hal` 的配置选项][esp-hal-config]（适用于 ESP32-C6）。

## 用法

在创建项目时，你可能需要配置一些额外的高级参数，例如，将外设放置在 RAM 中以提高性能，或更改某些包中的 RX/TX 队列大小。为此，你需要配置 `esp-config` 提供的一些设置。

你可以通过两种方式执行此操作：

- 通过设置环境变量。例如，在 `esp-hal` 中，如果你想将匿名符号放置在 RAM 中（`ESP_HAL_CONFIG_PLACE_ANON_IN_RAM`），默认设置为 `false`，你需要创建一个同名环境变量并修改其值。

- 通过在 `.cargo/config.toml` 中设置所需参数（此方法也会设置环境变量）：

  ```toml
  # .cargo/config.toml

  [env]
  ESP_HAL_CONFIG_PLACE_ANON_IN_RAM="true"
  ```

  修改 `.cargo/config.toml` 和 `[env]` 部分后，建议进行**清理构建**。

> [!NOTE]
> 在命令行上设置环境变量将优先于 `[env]` 部分。

## 多配置

根据你的应用程序，你可能会发现希望在同一个项目中支持不同的开发板/芯片/目标。在这种情况下，你可能需要为每个目标设置特定的选项。为此，我们推荐以下设置。

- 一个基准 `.cargo/config.toml`，其中包含你典型的构建修改标志（无论传递什么其他 `--config`，Cargo 都会_始终_读取并尊重此文件）
- `.cargo/` 中每个配置的配置文件
- （**推荐**）一个 Cargo [别名]，用于使用给定配置进行构建，例如 `run-config-a = "run --config=./.cargo/config_a.toml --release"`，但对于简单情况，你可以在 CLI 上传递 `--config`。

查看[此示例仓库]以更全面地了解多配置项目。

## 定义你自己的配置选项

你可能还想在项目中定义某些配置选项。为此，有必要在 `esp_config.yml` 文件中声明性地定义这些选项、它们的默认值以及其他参数和检查。详细信息可在项目仓库的[定义配置选项]部分找到。

[documentation]: https://docs.espressif.com/projects/rust/
[esp-config]: https://crates.io/crates/esp-config
[Defining Configuration Options]: https://github.com/esp-rs/esp-hal/tree/main/esp-config#defining-configuration-options
[esp-hal-config]: https://docs.espressif.com/projects/rust/esp-hal/1.0.0/esp32c6/esp_hal/index.html#additional-configuration
[this example repo]: https://github.com/bjoernQ/esp-hal-multiconfig-example/tree/main
[alias]: https://doc.rust-lang.org/cargo/reference/config.html#alias
