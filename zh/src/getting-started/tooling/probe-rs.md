# `probe-rs`

[`probe-rs`][probe-rs] 项目提供了一套工具，用于通过各种调试探针与嵌入式微控制器交互，并对 [Espressif 芯片][chips] 提供强大的支持。

除了烧录和监控外，它还提供了强大的调试功能。

如果你不确定现在是否需要它，可以跳过安装，稍后再回来安装。

配备 `USB-JTAG-SERIAL` 外设的 Espressif 设备无需任何外部硬件即可使用 `probe-rs`。对于没有此外设的设备，你需要一个外部编程器，例如 [ESP-Prog][esp-prog]。

> [!NOTE]
> `USB-JTAG-SERIAL` 外设在 ESP32-C6、ESP32-H2、ESP32-S3 和 ESP32-C3（修订版 0.3 或更高版本）中可用

[probe-rs]: https://probe.rs/
<!--- the search currently doesn't work on the probe-rs website --->
[chips]: https://probe.rs/targets/?q=espressif&p=0
[esp-prog]: https://docs.espressif.com/projects/esp-iot-solution/en/latest/hw-reference/ESP-Prog_guide.html

## 安装

请参阅 probe-rs 网站上的[安装][probe-rs-installation]和[设置][probe-rs-setup]指南。

[probe-rs-installation]: https://probe.rs/docs/getting-started/installation/
[probe-rs-setup]: https://probe.rs/docs/getting-started/probe-setup/
