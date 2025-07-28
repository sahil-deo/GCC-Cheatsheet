# GCC/G++ Compiler Reference Guide

A comprehensive reference for GCC/G++ compiler flags and common usage patterns.

## Basic Usage

```bash
g++ source.cpp -o output [options]
```

| Command | Description |
|---------|-------------|
| `g++ file.cpp` | Compiles file.cpp to a.out |
| `-o output` | Names the output binary |
| `-c file.cpp` | Compiles to object file file.o, no linking |
| `-S` | Outputs assembly code |
| `-E` | Runs only the preprocessor |
| `-v` | Prints verbose compilation steps |
| `--help` | Displays all available options |

## Compile Options

| Flag | Description |
|------|-------------|
| `-std=c++17` | Specify C++ standard |
| `-Wall` | Enable common warnings |
| `-Wextra` | Enable extra (less common) warnings |
| `-Werror` | Treat all warnings as errors |
| `-pedantic` | Enforce strict ISO C++ compliance |
| `-g` | Include debug symbols |
| `-DNAME=value` | Define macro from command line |
| `-I/path/to/includes` | Add custom include path |
| `-L/path/to/libs` | Add custom library path |
| `-l<name>` | Link with library lib<name>.so/.a |

## Optimization Flags

| Flag | Description |
|------|-------------|
| `-O0` | No optimization (fastest compile) |
| `-O1` | Basic optimization |
| `-O2` | Recommended for release builds |
| `-O3` | More aggressive optimization |
| `-Ofast` | Unsafe but faster (-O3 + relax checks) |
| `-Os` | Optimize for binary size |
| `-Og` | Optimize for debugging experience |
| `-flto` | Enable link-time optimization |
| `-march=native` | Use all CPU-specific instructions |
| `-funroll-loops` | Unroll loops (can improve performance) |
| `-fno-exceptions` | Remove exception support |
| `-fno-rtti` | Disable RTTI (smaller binary) |

## Debugging & Analysis

| Flag | Description |
|------|-------------|
| `-g` | Add debug symbols |
| `-fsanitize=address` | Detect memory errors (AddressSanitizer) |
| `-fsanitize=undefined` | Detect UB like overflow, null deref |
| `-fstack-protector-strong` | Protect against stack buffer overflow |
| `-D_GLIBCXX_DEBUG` | Debug STL usage (slow, dev use only) |

## Code Cleanliness / Warning Flags

| Flag | Description |
|------|-------------|
| `-Wshadow` | Variable shadowing |
| `-Wconversion` | Implicit conversions |
| `-Wsign-conversion` | Signed/unsigned issues |
| `-Wnull-dereference` | Possible null pointer deref |
| `-Wunused-variable` | Unused variables |
| `-Wformat` | printf/scanf format issues |
| `-Wduplicated-cond` | Duplicate conditions in if/else |
| `-Wduplicated-branches` | Identical branches |

## Linker Flags

| Flag | Description |
|------|-------------|
| `-static` | Statically link libraries |
| `-shared` | Build a shared library (.so) |
| `-rdynamic` | Export symbols for dynamic linking |
| `-Wl,--gc-sections` | Strip unused sections |

## File Type Flags

| Flag | Output Type |
|------|-------------|
| `-c` | .o object file |
| `-S` | .s assembly file |
| `-E` | Preprocessed |
| none | Linked binary |

## Recommended Flag Combinations

### Development Build
```bash
g++ main.cpp -std=c++17 -g -Wall -Wextra -Og
```
Perfect for development with debug symbols and reasonable optimization.

### Release Build (Performance)
```bash
g++ main.cpp -std=c++17 -O3 -march=native -flto -DNDEBUG
```
Maximum performance for production releases.

### Debugging Memory Issues
```bash
g++ main.cpp -g -fsanitize=address -fsanitize=undefined
```
Comprehensive memory error detection and undefined behavior checking.

### Minimal Binary Size
```bash
g++ main.cpp -Os -s -ffunction-sections -fdata-sections -Wl,--gc-sections
```
Creates the smallest possible binary by optimizing for size and stripping unused code.

## Quick Tips

- Use `-O2` for most release builds unless you need maximum performance
- Always include `-Wall -Wextra` during development
- Add `-g` when you might need to debug
- Use sanitizers (`-fsanitize=address,undefined`) to catch hard-to-find bugs
- For maximum portability, avoid `-march=native`
- Add `-DNDEBUG` in release builds to disable assert() statements
