# About FMRuby Core

## Overview

FMRuby Core is an embedded operating system designed for ESP32-S3-N16R8, providing a lightweight multi-VM runtime environment with hardware-accelerated graphics capabilities.

## System Architecture

### Multi-VM Runtime

FMRuby Core supports multiple execution environments:

- **mruby (PicoRuby)**: Ruby scripting with PicoRuby implementation
- **Lua 5.4**: Lua scripting engine
- **Native C**: Direct C function execution

Each VM operates with isolated memory management, ensuring application stability and security.

### Hardware Platform

**Target Hardware**: ESP32-S3-N16R8
- 16MB Flash
- 8MB PSRAM
- Dual-core processor
- Hardware graphics acceleration support

**Supported Peripherals**:
- USB Host (keyboard/mouse)
- SD Card
- SPI (for NTSC video output to separate ESP32-WROVER)

### Graphics System

- **Canvas-based Rendering**: Efficient graphics abstraction
- **LovyanGFX-compatible API**: Industry-standard graphics interface
- **NTSC Video Output**: Analog video output capability
- **Hardware Abstraction Layer**: Platform-independent graphics API

### Audio System

- APU-emulated audio processing
- Sound synthesis and playback capabilities

### Task Management

- **FreeRTOS-based**: Industry-standard RTOS foundation
- **Multitasking**: Concurrent application execution
- **Memory Isolation**: Per-application memory protection
- **Messaging System**: Inter-process communication (IPC)

## Project Structure

```
components/          ESP-IDF components
  ├── lua/          Lua 5.4 VM and extensions
  ├── picoruby-esp32/ mruby VM (submodule)
  ├── fmrb_*/       FMRuby core libraries
  │   ├── fmrb_hal/     Hardware abstraction layer
  │   ├── fmrb_gfx/     Graphics system
  │   ├── fmrb_mem/     Memory management
  │   ├── fmrb_msg/     Messaging system
  │   ├── fmrb_audio/   Audio system
  │   └── ...
  └── ...
main/               FMRuby OS kernel and application layer
  ├── kernel/       Core OS kernel
  ├── app/          Application runtime
  └── drivers/      Hardware drivers
flash/              Flash filesystem contents
  ├── apps/         Applications
  └── configs/      Configuration files
host/               PC simulation environment (SDL2)
lib/                Custom mrbgems and patches
doc/                Documentation
```

## Build Requirements

### ESP32 Build

- **Docker**: ESP-IDF v5.5.1 container
- **Ruby**: For build scripts (Rakefile)

### Linux Simulation Build

**Ubuntu/Debian**:
```bash
sudo apt-get install libsdl2-dev libmsgpack-dev pkg-config clang-format clang-tidy llvm
```

**macOS**:
```bash
brew install sdl2 msgpack pkg-config llvm
```

**Ruby Gems**:
```bash
gem install serialport
```

## Development Workflow

### Build Commands

```bash
# Linux simulation
rake build:linux

# ESP32 hardware
rake build:esp32

# Clean build
rake clean

# View all commands
rake -T
```

### Documentation Generation

```bash
# C/C++ API documentation (Doxygen)
rake doc:c

# Ruby API documentation (YARD)
rake doc:ruby

# Generate all documentation
rake doc:all

# Clean documentation
rake doc:clean
```

## Key Technologies

- **ESP-IDF v5.5.1**: Espressif IoT Development Framework
- **FreeRTOS**: Real-time operating system
- **PicoRuby**: Lightweight mruby implementation
- **Lua 5.4**: Scripting language
- **LovyanGFX**: Graphics library
- **SDL2**: Simulation environment for Linux/macOS
- **MkDocs**: Documentation site generator
- **Material for MkDocs**: Documentation theme
- **Doxygen**: C/C++ API documentation
- **YARD**: Ruby API documentation

## Dual-Platform Development

FMRuby Core supports development on two platforms:

1. **ESP32 Target**: Full hardware implementation with all peripheral support
2. **Linux Simulation**: SDL2-based simulation for rapid development and testing

This approach enables:
- Fast iteration during development (Linux)
- Hardware validation without constant flashing (Linux)
- Full hardware testing when needed (ESP32)

## More Information

For detailed development guidelines, architecture decisions, and coding standards, refer to the CLAUDE.md file in the fmruby-core repository.

## License

See LICENSE file in the fmruby-core repository for details.
