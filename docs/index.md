# FMRuby Core Documentation

<div align="center">
  <img src="images/topimage.png" alt="FMRuby Logo">
</div>

Welcome to the FMRuby Core documentation!

## About FMRuby Core

FMRuby Core is a lightweight embedded operating system designed for ESP32-S3-N16R8, featuring multi-VM support (mruby/Lua) and hardware-accelerated graphics.

## Key Features

- **Multi-VM Runtime**: Support for mruby (PicoRuby), Lua 5.4, and native C applications
- **Graphics System**: Hardware-accelerated graphics with LovyanGFX-compatible API
- **NTSC Video Output**: Via SPI to separate ESP32-WROVER
- **Audio System**: APU-emulated audio processing
- **Task Management**: FreeRTOS-based multitasking with per-app memory isolation
- **Dual-Platform Development**: Build for ESP32 hardware or Linux simulation (SDL2)
- **USB Host Support**: Keyboard and mouse input
- **SD Card Support**: Filesystem access for applications and data

## Quick Start

### Building for ESP32

```bash
rake build:esp32
```

### Building for Linux Simulation

```bash
rake build:linux
./build/fmruby-core.elf
```

### View All Build Commands

```bash
rake -T
```

## Project Architecture

- **Multi-VM Application Runtime**: Run Ruby, Lua, and C applications
- **Canvas-based Graphics**: Efficient rendering system
- **Hardware Abstraction Layer (HAL)**: Platform-independent API
- **Messaging System**: Inter-process communication
- **Memory Management**: Isolated memory allocation per application

## Next Steps

For detailed information about the system architecture, API documentation, and development guidelines, please see the [About](about.md) page.
