# 内存分配

在 `no_std` 环境中，[`alloc`][alloc] 包可作为堆分配的选项。这启用了有用的常见 Rust 项，例如 `Vec` 和 `Box`，以及其他需要堆分配的集合。在某些情况下，`alloc` 可能是你希望使用的依赖项所必需的。

我们提供了自己的 `no_std` 堆分配器（Allocator），[`esp-alloc`][esp-alloc]。但在启用它之前，用户应该理解**为什么**他们可能想要堆分配以及所涉及的权衡。

## 为什么不使用堆？

虽然堆分配提供了灵活性，但它也带来了一些代价：

- **碎片化**：随着时间的推移，动态分配可能导致_碎片化_：小的、分散的分配可能会阻止大的分配，即使总内存可用。这可能导致微妙的运行时故障。
- **运行时开销**：分配和释放内存会产生计算成本，以及所选分配器的任何开销。

## 可配置的内存放置和回收 RAM

某些 Espressif 芯片具有不连续的内存映射，并非所有物理 RAM 都可以作为单个平坦的堆使用。例如，某些区域保留给 ROM 代码使用，不能被覆盖。以 ESP32 的内存布局为例。

<p align="center">
<img src="../assets/esp32-mm.webp" alt="ESP32 内存映射"/>
</p>

第二阶段引导加载程序在启动过程中使用的某些内存不能用作栈，但一旦进入主应用程序，可以用作堆。你可以在堆分配器声明中使用 `#[ram(reclaimed)]` 宏来使用这些原本未使用的内存。

```rust
// 使用 dram2_seg 中的 64kB 作为堆，否则未使用。
heap_allocator!(#[ram(reclaimed)] size: 64000);
```

## PSRAM

我们的芯片有几百千字节的内部 RAM，这可能对某些应用程序来说不够。某些 Espressif 芯片能够使用外部 PSRAM（伪静态 RAM）内存的虚拟地址。外部内存的使用方式与内部数据 RAM 相同，但有一定的限制。

> [!NOTE]
> 在 Xtensa 芯片上，PSRAM 中的原子操作无法正常工作——它们可能导致数据竞争并违背其目的。这意味着分配器不得用于分配 `Atomic*` 类型——无论是直接还是间接。ESP32 的限制可在此处找到。这**不影响**我们的 RISC-V 芯片，在 RISC-V 芯片上 PSRAM 与原子操作配合正常工作。

### 分配器注意事项

你只能有一个**全局分配器**，但分配器可以使用多个区域（例如 PSRAM、内部 RAM 或甚至多个块）。你可以使用夜间特性 `allocator_api` 和 [`allocator_api2`][allocator api2] 使用多个分配器，[`esp-alloc`][esp-alloc] 实现了该功能。

[esp-alloc]: https://crates.io/crates/esp-alloc
[alloc]: https://doc.rust-lang.org/alloc/
[here]: https://docs.espressif.com/projects/esp-idf/en/v5.4.1/esp32/api-guides/external-ram.html#restrictions
[allocator api2]: https://crates.io/crates/allocator-api2
