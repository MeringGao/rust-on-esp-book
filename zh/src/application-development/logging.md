# 日志记录

日志记录是嵌入式系统开发的关键方面，它提供了系统行为的可见性，并有助于调试和监控。在 Rust 生态系统中，两个常用的日志记录框架是 [`defmt`][defmt] 和 [`log`][log]。

无论你选择以下哪种工具来生成项目，[`esp-generate`][esp-generate] 都会确保一切设置正确，以便最终用户只需根据自己的需要调整使用的日志记录工具。

## `defmt`

[`defmt`][defmt] 是一个专为资源受限环境（如嵌入式系统）设计的高效日志记录框架。它提供紧凑的、二进制编码的日志消息，减少了与传统基于字符串的日志记录相关的开销。有关更多信息，请参阅 [`defmt` 文档][defmt-documentation]。我们建议在 Espressif 芯片上将 `defmt` 与 `probe-rs` 配对使用以获得最佳效果。

## `log`

[`log`][log] 包是 Rust 社区中广泛采用的日志门面。它定义了一组宏（`info!`、`warn!`、`error!` 等）来捕获各种级别的日志消息。我们在 [`esp-println`] 中提供了[日志记录器]实现，但如果你愿意，也可以实现自己的日志记录器。

[log]: https://crates.io/crates/log
[defmt]: https://crates.io/crates/defmt
[defmt-documentation]: https://defmt.ferrous-systems.com/introduction
[filtering]: https://defmt.ferrous-systems.com/filtering#filtering
[esp-generate]: ./../getting-started/tooling/esp-generate.md
[logger]: https://docs.rs/log/latest/log/#implementing-a-logger
[`esp-println`]: https://github.com/esp-rs/esp-hal/tree/main/esp-println
