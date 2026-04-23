# 术语表（Terminology）

本文档记录了本书翻译中使用的术语规范，分为三类：

## 1. 保持英文（Use English as-is）

以下术语在中文文本中直接使用英文原文：

| 英文 | 说明 |
|------|------|
| `no_std` | Rust 特性，表示不使用标准库 |
| `std` | Rust 标准库 |
| `alloc` | Rust 分配库 |
| `esp-hal` | Espressif 硬件抽象层包 |
| `esp-rs` | Espressif Rust 组织 |
| `esp-generate` | 项目生成工具 |
| `espflash` | 串口烧录工具 |
| `esp-config` | 配置工具 |
| `esp-alloc` | 内存分配包 |
| `esp-println` | 打印和日志包 |
| `esp-backtrace` | 回溯支持包 |
| `esp-bootloader-esp-idf` | ESP-IDF 引导加载程序支持包 |
| `esp-build` | 构建工具包 |
| `esp-hal-proc-macros` | 过程宏包 |
| `esp-lp-hal` | 低功耗核心 HAL |
| `esp-metadata` | 元数据包 |
| `esp-preempt` | 线程和同步原语包 |
| `esp-riscv-rt` | RISC-V 启动/运行时 |
| `esp-rom-sys` | ROM 代码支持包 |
| `esp-rtos` | 调度器实现 |
| `esp-sync` | 同步原语包 |
| `esp-storage` | 存储工具包 |
| `esp-radio` | 无线通信包 |
| `xtensa-lx` | Xtensa LX 处理器低层访问 |
| `xtensa-lx-rt` | Xtensa LX 启动/运行时 |
| `embedded-hal` | 嵌入式硬件抽象层 |
| `rand_core` | 随机数生成器核心 |
| `embedded-io` | 嵌入式 I/O 特质 |
| `embedded-test` | 嵌入式测试框架 |
| `probe-rs` | 调试工具 |
| `defmt` | 高效日志框架 |
| `log` | Rust 日志门面 |
| `critical-section` | 临界区包 |
| `embassy-executor` | Embassy 执行器 |
| `allocator_api2` | 分配器 API |
| `cargo-binstall` | Cargo 二进制安装工具 |
| `espup` | 工具链安装工具 |
| `idf.py` | ESP-IDF 构建工具 |
| Embassy | 异步嵌入式框架 |
| ArielOS | 安全、内存安全的物联网操作系统 |
| RTIC | 实时中断驱动并发框架 |
| ESP32, ESP32-S2, ESP32-S3, ESP32-C2, ESP32-C3, ESP32-C6, ESP32-H2, ESP32-H | Espressif SoC 系列 |
| ESP8266, ESP8684, ESP8685 | 旧款/兼容芯片 |
| Xtensa | Cadence 处理器架构 |
| RISC-V | 开源指令集架构 |
| SoC | 系统级芯片 |
| DevKit, DevKitC | 开发套件 |
| GPIO | 通用输入输出 |
| SPI | 串行外设接口 |
| I2C | 集成电路间总线 |
| UART | 通用异步收发传输器 |
| USB | 通用串行总线 |
| JTAG | 联合测试行动组（调试接口） |
| BLE | 低功耗蓝牙 |
| Wi-Fi | 无线局域网 |
| ESP-NOW | Espressif 无线通信协议 |
| IEEE 802.15.4 | 无线个人区域网络标准 |
| ROM | 只读存储器 |
| RAM | 随机存取存储器 |
| PSRAM | 伪静态随机存取存储器 |
| DMA | 直接内存访问 |
| RTT | 实时传输 |
| OTA | 空中升级 |
| HIL | 硬件在环 |
| RTOS | 实时操作系统 |
| TUI | 文本用户界面 |
| HAL | 硬件抽象层 |
| ABI | 应用程序二进制接口 |
| MSVC | Microsoft Visual C++ 编译器 |
| GNU | GNU 工具链 |
| SemVer | 语义化版本控制 |
| LLVM | 底层虚拟机编译器基础设施 |
| GCC | GNU 编译器集合 |
| CI | 持续集成 |
| IDE | 集成开发环境 |
| VS Code | Visual Studio Code |
| Helix, Neovim, Zed | 编辑器名称 |
| Cargo | Rust 包管理器和构建工具 |
| rustup | Rust 工具链安装器 |
| WROOM | Espressif 模块系列 |
| RGB, WS2812B | LED 类型 |
| MCUboot | 开源引导加载程序 |
| `#[test]` | Rust 测试属性宏 |
| `#[should_panic]` | Rust 测试属性宏 |
| `#[ram(reclaimed)]` | 内存属性宏 |
| `heap_allocator!` | 堆分配器宏 |

## 2. 翻译并标注（Translate + Annotate on first use）

以下术语首次出现时标注英文原文：

| 中文 | 英文 | 首次出现示例 |
|------|------|-------------|
| 外设 | Peripheral | 外设（Peripheral） |
| 工具链 | Toolchain | 工具链（Toolchain） |
| 引导加载程序 | Bootloader | 引导加载程序（Bootloader） |
| 分区表 | Partition Table | 分区表（Partition Table） |
| 分区 | Partition | 分区（Partition） |
| 分配器 | Allocator | 分配器（Allocator） |
| 堆 | Heap | 堆（Heap） |
| 栈 | Stack | 栈（Stack） |
| 内存碎片 | Fragmentation | 内存碎片（Fragmentation） |
| 闪存 | Flash | 闪存（Flash） |
| 中断 | Interrupt | 中断（Interrupt） |
| 驱动程序 | Driver | 驱动程序（Driver） |
| 包 | Crate | 包（Crate） |
| 目标 | Target | 目标（Target） |
| 组件 | Component | 组件（Component） |
| 特性 | Feature | 特性（Feature） |
| 配置 | Profile | 配置（Profile） |
| 别名 | Alias | 别名（Alias） |
| 回溯 | Backtrace | 回溯（Backtrace） |
| 恐慌处理程序 | Panic Handler | 恐慌处理程序（Panic Handler） |
| 原子操作 | Atomic | 原子操作（Atomic） |
| 嵌入式 | Embedded | 嵌入式（Embedded） |
| 固件 | Firmware | 固件（Firmware） |
| 硬件 | Hardware | 硬件（Hardware） |
| 软件 | Software | 软件（Software） |
| 日志记录 | Logging | 日志记录（Logging） |
| 配置 | Configuration | 配置（Configuration） |
| 应用程序 | Application | 应用程序（Application） |
| 开发 | Development | 开发（Development） |
| 环境 | Environment | 环境（Environment） |
| 生态系统 | Ecosystem | 生态系统（Ecosystem） |
| 文档 | Documentation | 文档（Documentation） |
| 仓库 | Repository | 仓库（Repository） |
| 发布 | Release | 发布（Release） |
| 稳定版 | Stable | 稳定版（Stable） |
| 每日构建版 | Nightly | 每日构建版（Nightly） |
| 上游 | Upstream | 上游（Upstream） |
| 分支 | Fork | 分支（Fork） |
| 内存 | Memory | 内存（Memory） |
| 处理器 | Processor | 处理器（Processor） |
| 架构 | Architecture | 架构（Architecture） |
| 模块 | Module | 模块（Module） |
| 寄存器 | Register | 寄存器（Register） |
| 缓存 | Cache | 缓存（Cache） |
| 地址 | Address | 地址（Address） |
| 偏移量 | Offset | 偏移量（Offset） |
| 二进制 | Binary | 二进制（Binary） |
| 镜像 | Image | 镜像（Image） |
| 更新 | Update | 更新（Update） |
| 回滚 | Rollback | 回滚（Rollback） |
| 加密 | Encryption | 加密（Encryption） |
| 安全启动 | Secure Boot | 安全启动（Secure Boot） |
| 校准 | Calibration | 校准（Calibration） |
| 文件系统 | Filesystem | 文件系统（Filesystem） |
| 参数 | Parameter | 参数（Parameter） |
| 标签 | Label | 标签（Label） |
| 类型 | Type | 类型（Type） |
| 子类型 | Subtype | 子类型（Subtype） |
| 条目 | Entry | 条目（Entry） |
| 预构建 | Pre-built | 预构建（Pre-built） |
| 设置 | Settings | 设置（Settings） |
| 监视器 | Monitor | 监视器（Monitor） |
| 调试 | Debug | 调试（Debug） |
| 调试探针 | Probe | 调试探针（Probe） |
| 编程器 | Programmer | 编程器（Programmer） |
| 端口 | Port | 端口（Port） |
| 桥接器 | Bridge | 桥接器（Bridge） |
| 发光二极管 | LED | 发光二极管（LED） |
| 引脚 | Pin | 引脚（Pin） |
| 按钮 | Button | 按钮（Button） |
| 复位 | Reset | 复位（Reset） |
| 启动 | Boot | 启动（Boot） |
| 下载 | Download | 下载（Download） |
| 模式 | Mode | 模式（Mode） |
| 绑定引脚 | Strapping Pin | 绑定引脚（Strapping Pin） |
| 电源 | Power Supply | 电源（Power Supply） |
| 通信 | Communication | 通信（Communication） |
| 协议 | Protocol | 协议（Protocol） |
| 层 | Layer | 层（Layer） |
| 状态机 | State Machine | 状态机（State Machine） |
| 调度器 | Scheduler | 调度器（Scheduler） |
| 运行时 | Runtime | 运行时（Runtime） |
| 接口 | Interface | 接口（Interface） |
| 后端 | Backend | 后端（Backend） |
| 模板 | Template | 模板（Template） |
| 选项 | Option | 选项（Option） |
| 骨架 | Skeleton | 骨架（Skeleton） |
| 基线 | Baseline | 基线（Baseline） |
| 依赖 | Dependency | 依赖（Dependency） |
| 手动 | Manually | 手动（Manually） |
| 高级 | Advanced | 高级（Advanced） |
| 队列 | Queue | 队列（Queue） |
| 性能 | Performance | 性能（Performance） |
| 资源 | Resource | 资源（Resource） |
| 约束 | Constraint | 约束（Constraint） |
| 开销 | Overhead | 开销（Overhead） |
| 计算 | Computational | 计算（Computational） |
| 连续 | Contiguous | 连续（Contiguous） |
| 映射 | Mapping | 映射（Mapping） |
| 物理 | Physical | 物理（Physical） |
| 区域 | Region | 区域（Region） |
| 保留 | Reserved | 保留（Reserved） |
| 覆盖 | Overwrite | 覆盖（Overwrite） |
| 布局 | Layout | 布局（Layout） |
| 段 | Segment | 段（Segment） |
| 宏 | Macro | 宏（Macro） |
| 声明 | Declaration | 声明（Declaration） |
| 虚拟 | Virtual | 虚拟（Virtual） |
| 外部 | External | 外部（External） |
| 限制 | Restriction | 限制（Restriction） |
| 全局 | Global | 全局（Global） |
| 夜间特性 | Nightly Feature | 夜间特性（Nightly Feature） |
| 应用程序接口 | API | 应用程序接口（API） |
| 特质 | Trait | 特质（Trait） |
| 无关的 | Agnostic | 无关的（Agnostic） |
| 随机数生成器 | RNG | 随机数生成器（RNG） |
| 类似物 | Analogue | 类似物（Analogue） |
| 并发 | Concurrency | 并发（Concurrency） |
| 执行器 | Executor | 执行器（Executor） |
| 任务 | Task | 任务（Task） |
| 生成 | Spawn | 生成（Spawn） |
| 生成器 | Spawner | 生成器（Spawner） |
| 多核 | Multicore | 多核（Multicore） |
| 感知 | Aware | 感知（Aware） |
| 线程 | Thread | 线程（Thread） |
| 线程模式 | Thread-mode | 线程模式（Thread-mode） |
| 时间驱动器 | Time Driver | 时间驱动器（Time Driver） |
| 定时器 | Timer | 定时器（Timer） |
| 等待者 | Waiter | 等待者（Waiter） |
| 物联网 | IoT | 物联网（IoT） |
| 低功耗 | Low-power | 低功耗（Low-power） |
| 内存安全 | Memory-safe | 内存安全（Memory-safe） |
| 网络 | Networking | 网络（Networking） |
| 统一 | Unified | 统一（Unified） |
| 实时 | Real-time | 实时（Real-time） |
| 集成 | Integration | 集成（Integration） |
| 测试 | Test | 测试（Test） |
| 单元测试 | Unit Test | 单元测试（Unit Test） |
| 集成测试 | Integration Test | 集成测试（Integration Test） |
| 测试框架 | Harness | 测试框架（Harness） |
| 主机 | Host | 主机（Host） |
| 循环 | Loop | 循环（Loop） |
| 修订版 | Revision | 修订版（Revision） |
| 连接 | Connect | 连接（Connect） |
| 产物 | Artifact | 产物（Artifact） |
| 过滤 | Filter | 过滤（Filter） |
| 切换 | Switch | 切换（Switch） |
| 补丁 | Patch | 补丁（Patch） |
| 分支 | Branch | 分支（Branch） |
| 遗忘 | Forget | 遗忘（Forget） |
| 非预期的 | Unintended | 非预期的（Unintended） |
| 后果 | Consequence | 后果（Consequence） |
| 错误地 | Erroneously | 错误地（Erroneously） |
| 无限期地 | Indefinitely | 无限期地（Indefinitely） |
| 完成 | Complete | 完成（Complete） |
| 接收 | Receive | 接收（Receive） |
| 写入 | Write | 写入（Write） |
| 高 | High | 高（High） |
| 低 | Low | 低（Low） |
| 电平 | Level | 电平（Level） |
| 采样 | Sample | 采样（Sample） |
| 重新采样 | Re-sample | 重新采样（Re-sample） |
| 看门狗 | Watchdog | 看门狗（Watchdog） |
| 故障排除 | Troubleshooting | 故障排除（Troubleshooting） |

## 3. 普通词汇（Common words）

普通英文词汇直接翻译为中文，无需标注。
