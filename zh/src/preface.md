<p style="text-align:center;"><img src="../assets/esp-rs.svg" width="25%"></p>

> [Read in English (阅读英文版)](../)

# 前言

欢迎来到我们的 Espressif 产品嵌入式 Rust 开发指南。本书旨在帮助你入门并熟悉我们的工具和生态系统。在书中，我们将介绍软件栈的结构，并演示使用项目生成和工具的基本工作流程。阅读完本书后，你将准备好通过参考文档和外部培训资源探索更高级的内容。

## 本书适合谁阅读

本书面向对嵌入式开发感兴趣的 Rust 开发者，即使你没有嵌入式系统的经验。虽然熟悉底层编程概念会有所帮助，但我们会在需要时介绍关键概念。如果你想扩展基础知识，可以学习额外的[资源][resources]。

## 稳定性与可用性

虽然我们努力追求稳定性，但用户应该预期会有周期性的修改，因为我们会改进 API、提升性能并引入新功能。已经稳定的[模块][modules]不会受到破坏性变更的影响，这符合语义化版本控制（`SemVer`）的规范。然而，`unstable`（不稳定）功能——例如 `esp-hal` 的某些部分和某些驱动程序——正在积极开发中，不受 `SemVer` 保证的覆盖。这意味着使用这些不稳定的组件可能会在一次简单的 `cargo update` 后破坏你的项目，就像使用 Rust 的 `nightly`（每日构建版）编译器一样。这种不稳定性在整个 Rust 嵌入式生态系统中很常见，该生态系统仍在快速发展中。请预期频繁的变化并密切跟踪依赖项。对于所有主要包，我们提供了版本之间的迁移指南，以帮助你保持最新。

## 额外资源

如果你对本书中涉及的某些概念不熟悉，或者希望加深理解，以下资源可能会有所帮助：

| 资源                                                     | 描述                                                                           |
| -------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| [The Rust Programming Language][rust-book]               | 在深入嵌入式开发之前学习 Rust 基础知识。                      |
| [The Embedded Rust Book][embedded-rust-book]             | Rust 嵌入式工作组的资源集合。                         |
| [Embedded Rust (`no_std`) on Espressif][no_std-training] | 在 Espressif 芯片的 `no_std` 环境中工作的指南。                       |
| [Awesome ESP Rust][awesome-esp-rust]                     | 使用 Rust 编程语言开发 Espressif 产品的资源列表 |
| [Awesome Embedded Rust][awesome-embedded-rust]           | 与 Rust 编程语言中嵌入式和底层编程相关的资源列表，包括一系列有用的包。                       |

## 为本书做出贡献

本书的编写工作在此仓库[协调][book-repository]。

如果你在按照说明操作时遇到困难，或者发现某些章节表述不清，请在[问题追踪器][book-issues]中报告。欢迎以拉取请求的形式贡献拼写错误或清晰度改进！

## 支持与社区

如果你需要帮助、有问题，或者想讨论与 `esp-rs` 相关的话题，可以通过以下渠道联系我们：

- **Matrix**: [加入我们的社区聊天](https://matrix.to/#/#esp-rs:matrix.org)。
- **GitHub Discussions**: [参与社区讨论](https://github.com/esp-rs/esp-hal/discussions)。

我们希望本书能为你提供知识和信心，帮助你使用 Rust 在 Espressif 产品上构建稳健、高效且安全的嵌入式应用程序。让我们开始吧！

[modules]: https://docs.espressif.com/projects/rust/esp-hal/1.0.0/esp32c6/esp_hal/index.html#modules
[resources]: #额外资源
[rust-book]: https://doc.rust-lang.org/book/
[embedded-rust-book]: https://docs.rust-embedded.org/book/index.html
[no_std-training]: https://esp-rs.github.io/no_std-training/
[awesome-esp-rust]: https://github.com/esp-rs/awesome-esp-rust.git
[awesome-embedded-rust]: https://github.com/rust-embedded/awesome-embedded-rust
[book-repository]: https://github.com/esp-rs/book
[book-issues]: https://github.com/esp-rs/book/issues/
