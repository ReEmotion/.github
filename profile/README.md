<p align="center">
  <img src="https://raw.githubusercontent.com/ReEmotion/.github/main/profile/assets/banner.svg" alt="ReEmotion — an independent PS2 emulator exploring AOT translation for RK3566" width="1200">
</p>

<p align="center">
  <strong>An independent PS2 emulator project exploring ahead-of-time translation for RK3566.</strong><br>
  Architecture design · Native code translation · Homebrew validation
</p>

<p align="center">
  English · <a href="https://github.com/ReEmotion/.github/blob/main/profile/README.zh-CN.md">简体中文</a>
</p>

## What we're building

ReEmotion explores a different execution approach for PS2 emulation: translate PS2 executables offline into host-native code, package that code in a custom ELF, and execute it through our own loader and PS2 runtime.

Our long-term goal is full PS2 compatibility, with **RK3566 as the initial target**. The project is currently in the **architecture design stage**; self-test homebrew programs are our initial validation target. Performance and compatibility will be evaluated as the implementation develops.

## Architecture direction

| Component | Role |
| --- | --- |
| **AOT compiler** | Translate PS2 instructions and control flow into host-native code, with the metadata needed by the runtime. |
| **Custom ELF & loader** | Package translated code and program data; resolve runtime interfaces and map executable code into the host process. |
| **PS2 runtime** | Maintain machine state, memory and device behavior, exceptions, interrupts, and emulated time. |

We are designing the boundaries between these components first: how translated code hands control back to the runtime, how dynamic memory accesses distinguish RAM from MMIO, and how execution remains observable for debugging and comparison.

## Current focus

- Define the execution contract between AOT code and the runtime.
- Design address spaces, RAM fast paths, and device access interfaces.
- Establish a homebrew workflow for comparing checkpoints and program results with a reference emulator.
- Build toward a minimal compiler → loader → runtime execution loop, then expand system coverage and measure behavior on RK3566.

## Repositories & references

| Repository | Purpose |
| --- | --- |
| [**Play-**](https://github.com/ReEmotion/Play-) | Our Play! reference fork, including remote debugging work on [`feature/remote-debugger-mcp`](https://github.com/ReEmotion/Play-/tree/feature/remote-debugger-mcp). |
| [**.github**](https://github.com/ReEmotion/.github) | The organization profile and its presentation assets. |

**Play! is an external reference for behavior comparison and debugging.** ReEmotion has its own architecture; Play! is not the foundation of our product runtime. See the [remote debugger documentation](https://github.com/ReEmotion/Play-/blob/feature/remote-debugger-mcp/docs/remote-debugger.md) for the reference-side Python CLI.

Our homebrew workflow uses [PS2DEV](https://github.com/ps2dev) and [PS2SDK](https://github.com/ps2dev/ps2sdk). Thanks to the [Play! project](https://github.com/jpd002/Play-) and the PS2 homebrew community for the tools and reference implementations that support this exploration.

## Join the discussion

Interested in binary translation, emulator runtimes, or PS2 homebrew? Bring design questions and ideas to the [organization profile repository's Issues](https://github.com/ReEmotion/.github/issues). For our Play! remote-debugging work, use [Play- Issues](https://github.com/ReEmotion/Play-/issues).
