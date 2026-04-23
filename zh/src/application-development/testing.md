# 测试

测试是应用程序开发不可或缺的一部分。以我们在 `esp-hal` 中的做法为例，你可以为应用程序编写并运行直接在硬件本身上运行的测试。

## 主机测试

在可能且有意义的地方，你应该尝试尽可能多地在主机上测试，而不是在目标设备上测试。在主机上测试更容易集成到 CI 中，速度更快，而且不会浪费设备上的闪存写入周期。_需要_真实硬件才能运行的测试应该使用硬件在环测试设置。

## 硬件在环测试

硬件在环（Hardware In Loop，HIL）测试是在测试设置中使用真实设备。我们使用 [`embedded-test`] 框架编写单元测试和集成测试，因此原则上，该过程与非嵌入式项目仅略有不同。我们使用 [`probe-rs`]（检查 [`hil-test` 子仓库]中的正确修订版）在目标设备上烧录和运行测试。为此，你**必须**仅使用开发套件上的 `USB-Serial-JTAG` 端口（请参阅[硬件概述](../introduction/hardware-overview.md)）。如果你的设备没有此端口，你将需要使用 [esp-prog] 或另一个合适的编程器，并按照[连接说明]进行连接（在页面上选择所需的芯片）。

使用 `esp-generate` 并在 `probe-rs` 下选择 `embedded-test` 将在你的项目中设置测试，这样当设备正确连接时，你就可以在本地运行 `cargo test`。

### `embedded-test`

[`embedded-test`] 测试是作为放置在 `#[test]` 宏下的函数编写的，类似于 `std` 测试框架。通常，测试的结果是这个函数的结果，即如果代码发生了恐慌（panic），测试被认为失败，并运行下一个测试。然而，有许多方法可以自定义此过程，例如 `#[should_panic]` 属性宏，其中 `panic` 被认为是测试成功完成，为测试设置超时，以及更多可以在 [`embedded-test` 文档]中找到的内容。它还支持与 IDE 集成，因为它模仿了默认的 Rust 测试框架。

[`embedded-test`]: https://github.com/probe-rs/embedded-test
[`probe-rs`]: https://probe.rs
[`hil-test` sub-repository]: https://github.com/esp-rs/esp-hal/tree/main/hil-test
[esp-prog]:  https://docs.espressif.com/projects/esp-dev-kits/en/latest/other/esp-prog/user_guide.html
[connection instructions]: https://docs.espressif.com/projects/esp-idf/en/v5.2.3/esp32s2/api-guides/jtag-debugging/configure-other-jtag.html
[`embedded-test` documentation]: https://docs.rs/embedded-test/0.6.2/embedded_test/
