<p align="center">
  <img src="https://raw.githubusercontent.com/ReEmotion/.github/main/profile/assets/banner.svg" alt="ReEmotion — 面向 RK3566、探索 AOT 翻译的独立 PS2 模拟器项目" width="1200">
</p>

<p align="center">
  <strong>面向 RK3566，探索提前编译的独立 PS2 模拟器项目。</strong><br>
  架构设计 · 原生代码翻译 · Homebrew 验证
</p>

<p align="center">
  <a href="https://github.com/ReEmotion/.github/blob/main/profile/README.md">English</a> · 简体中文
</p>

## 我们在做什么

ReEmotion 探索一种 PS2 模拟器执行方式：在离线阶段把 PS2 可执行程序翻译为宿主原生代码，封装进自定义 ELF，再通过我们自己的加载器和 PS2 运行时加载执行。

长期目标是完整 PS2 兼容，**首个目标平台是 RK3566**。项目目前处于**架构设计阶段**，以自检测 homebrew 程序作为初期验证目标。性能与兼容性将随着实现推进逐步评估。

## 架构方向

| 组成 | 职责 |
| --- | --- |
| **AOT 编译器** | 将 PS2 指令与控制流翻译为宿主原生代码，并生成运行时所需元数据。 |
| **自定义 ELF 与加载器** | 封装翻译代码和程序数据，连接运行时接口，将可执行代码映射到宿主进程。 |
| **PS2 运行时** | 管理机器状态、内存和设备行为、异常、中断及模拟时间。 |

当前优先明确这些组成之间的边界：翻译代码如何交还控制权，动态内存访问如何区分 RAM 与 MMIO，以及执行过程如何支持调试和状态对照。

## 当前重点

- 明确 AOT 代码与运行时之间的执行契约。
- 设计地址空间、RAM 快速路径和设备访问接口。
- 建立 homebrew 验证流程，与参考模拟器比较检查点状态和程序结果。
- 逐步形成编译器 → 加载器 → 运行时的最小执行闭环，再扩展系统覆盖并在 RK3566 上测量实际行为。

## 仓库与参考工具

| 仓库 | 用途 |
| --- | --- |
| [**Play-**](https://github.com/ReEmotion/Play-) | Play! 参考分支仓库；远程调试工作位于 [`feature/remote-debugger-mcp`](https://github.com/ReEmotion/Play-/tree/feature/remote-debugger-mcp)。 |
| [**.github**](https://github.com/ReEmotion/.github) | 组织主页与展示素材。 |

**Play! 用于行为对照和调试参考。** ReEmotion 拥有自己的架构，Play! 不是产品运行时的基础。参考侧的 Python CLI 用法见 [远程调试文档](https://github.com/ReEmotion/Play-/blob/feature/remote-debugger-mcp/docs/remote-debugger.md)。

Homebrew 开发使用 [PS2DEV](https://github.com/ps2dev) 与 [PS2SDK](https://github.com/ps2dev/ps2sdk)。感谢 [Play! 项目](https://github.com/jpd002/Play-) 和 PS2 homebrew 社区提供的工具与参考实现。

## 参与讨论

如果你对二进制翻译、模拟器运行时或 PS2 homebrew 感兴趣，欢迎在 [组织主页仓库的 Issues](https://github.com/ReEmotion/.github/issues) 提出设计问题和想法。Play! 远程调试相关问题请使用 [Play- Issues](https://github.com/ReEmotion/Play-/issues)。
