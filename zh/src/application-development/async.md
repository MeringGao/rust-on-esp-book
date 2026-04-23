# 异步选项

> [!NOTE]
> 本节不作为异步教程或教学材料。有关这些目的，请访问[官方 async-book]。

`esp-hal` 为大多数支持的驱动程序提供阻塞和异步 API。驱动程序默认以[`Blocking`]模式构建。要设置异步驱动程序，必须使用 `into_async` 方法将它们转换为[`Async`]模式。有关更多信息并入门，请查看 [`esp-hal` 包]中的 `examples`。

> [!NOTE]
> 我们的 `Async` 驱动程序不是 `Send`，因为它们在当前核心上注册中断。将它们移动到另一个核心可能会导致问题。如果用户需要发送（移动）驱动程序到另一个核心，他们应该发送 `Blocking` 版本，然后在正确的核心上调用 `into_async` 以正确绑定它。

## Embassy

[Embassy] 是一个专为嵌入式 Rust 开发设计的异步（async）框架；其 [`embassy-executor`] 包提供了一个 `async/await` 执行器，它执行固定数量的任务，这些任务在启动时静态分配，但稍后可以添加更多任务。要稍后生成更多任务，你可以保留 `Spawner` 的副本，例如通过将其作为参数传递给初始任务。有关 `embassy` 的更多信息，请访问 [Embassy 书]。

[`esp-rtos`] 包提供 [`esp-hal`] 和 [Embassy] 异步框架之间的集成。它支持：

1. 中断模式执行器
2. 多核感知线程模式 embassy 执行器
3. Embassy 时间驱动器
4. 定时器等待队列

## ArielOS

[ArielOS] 是一个用于安全、内存安全、低功耗物联网的操作系统。它建立在嵌入式 Rust 生态系统的各种项目之上，包括 `esp-hal`。ArielOS 专注于紧密集成，添加缺失的操作系统功能，如多核调度器、安全网络、可移植驱动程序和统一构建系统。结果是强大的基于 C 的实时操作系统（RTOS）解决方案的替代方案，但完全使用 Rust 实现。它与 embassy 有很好的集成，可以以各种方式与 embassy 一起使用。

## RTIC

[实时中断驱动并发（RTIC）] 是一个社区支持的并发框架，用于构建实时系统。实时任务不是异步的，但"软件"任务是异步的。目前，仅支持 ESP32-C3 和 ESP32-C6。

<!-- TODO: change ArielOS to crates.io link when it's ready -->
[official async-book]: https://rust-lang.github.io/async-book/
[`Blocking`]: https://docs.espressif.com/projects/rust/esp-hal/1.0.0/esp32c6/esp_hal/struct.Blocking.html
[`Async`]: https://docs.espressif.com/projects/rust/esp-hal/1.0.0/esp32c6/esp_hal/struct.Async.html
[Embassy]: https://embassy.dev
[embassy-executor]: https://crates.io/crates/embassy-executor
[`esp-rtos`]: https://crates.io/crates/esp-rtos
[`esp-hal`]: https://crates.io/crates/esp-hal
[Embassy book]: https://embassy.dev/book/
[esp-hal package]: https://github.com/esp-rs/esp-hal
[ArielOS]: https://github.com/ariel-os/ariel-os
[Real-Time Interrupt-driven Concurrency (RTIC)]: https://crates.io/crates/rtic
