# Professional x86-64 Decompiler

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux-lightgrey.svg)

A production-grade decompiler that converts x86-64 assembly code from PE (Windows) and ELF (Linux) executables into high-level C++ or C# code.

## ✨ Features

- **Multi-Format Support**: Parse PE (Portable Executable) and ELF (Executable and Linkable Format) files
- **Intelligent Function Detection**: Automatically identifies function prologs and real code sections
- **x86-64 Disassembly**: Comprehensive support for x86-64 instruction set including:
  - Data movement (MOV, LEA, PUSH, POP)
  - Arithmetic operations (ADD, SUB, INC, DEC)
  - Bitwise operations (AND, OR, XOR)
  - Control flow (JMP, CALL, RET, conditional jumps)
  - REX prefix handling for 64-bit operations
  - RIP-relative addressing
- **Dual Output Languages**: Generate decompiled code in C++ or C#
- **Jump Table Detection**: Intelligently skips import trampolines and jump tables
- **Production-Ready**: Error handling, validation, and clean architecture

## 🚀 Quick Start

### Prerequisites

- C++11 or later compiler (GCC, Clang, MSVC)
- Standard C++ libraries

### Building

```bash
# Using g++
g++ -std=c++11 -O2 decompiler.cpp -o decompiler

# Using MSVC
cl /EHsc /O2 decompiler.cpp

# Using CMake (if available)
mkdir build && cd build
cmake ..
make
```

### Running

```bash
./decompiler
# Or on Windows: decompiler.exe
```

## 📖 Usage

1. **Start the decompiler**:
   ```
   ./decompiler
   ```

2. **Enter the executable path**:
   ```
   Enter executable file path: /path/to/your/executable.exe
   ```

3. **Select output language**:
   ```
   Select output language:
   1. C++
   2. C#
   Choice: 1
   ```

4. **View results**: The decompiler will display:
   - PE/ELF header information
   - Section details
   - Disassembled instructions
   - Decompiled high-level code

## 🏗️ Architecture

### Core Components

```
┌─────────────────────────────────────────┐
│         ExecutableParser                │
│  - PE/ELF format detection              │
│  - Header parsing                       │
│  - Section identification               │
└─────────────┬───────────────────────────┘
              │
              ▼
┌─────────────────────────────────────────┐
│       SimpleDisassembler                │
│  - Byte-to-instruction conversion       │
│  - x86-64 opcode decoding               │
│  - REX prefix handling                  │
└─────────────┬───────────────────────────┘
              │
              ▼
┌─────────────────────────────────────────┐
│          AsmParser                      │
│  - Instruction classification           │
│  - Operand type detection               │
│  - IR generation                        │
└─────────────┬───────────────────────────┘
              │
              ▼
┌─────────────────────────────────────────┐
│        CodeGenerator                    │
│  - High-level code generation           │
│  - Variable declaration                 │
│  - C++/C# output formatting             │
└─────────────────────────────────────────┘
```

### Supported Instructions

#### Data Transfer
- `MOV` - Move data
- `LEA` - Load effective address
- `PUSH/POP` - Stack operations

#### Arithmetic
- `ADD/SUB` - Addition/Subtraction
- `INC/DEC` - Increment/Decrement
- `MUL/IMUL` - Multiplication
- `DIV/IDIV` - Division

#### Logical
- `AND/OR/XOR` - Bitwise operations
- `NOT` - Bitwise NOT
- `SHL/SHR/SAL/SAR` - Shift operations

#### Control Flow
- `JMP` - Unconditional jump
- `JE/JNE/JZ/JNZ` - Conditional jumps
- `JG/JGE/JL/JLE` - Signed comparisons
- `JA/JAE/JB/JBE` - Unsigned comparisons
- `CALL/RET` - Function calls

#### Other
- `CMP/TEST` - Comparisons
- `NOP` - No operation
- `INT3` - Breakpoint

## 📋 Example Output

### Input Executable
```assembly
0x00001910: sub rsp, 40
0x00001914: lea rcx, [rip + 0x39d5]
0x0000191b: call 0x7bc
0x00001920: nop
0x00001921: add rsp, 40
0x00001925: ret
```

### Decompiled C++ Output
```cpp
#include <iostream>
#include <cstdint>

void decompiled_function() {
    int rsp = 0;
    int rcx = 0;
    
    rsp -= 40;
    rcx = &(rip + 0x39d5);
    call_0x7bc();
    // nop
    rsp += 40;
    return;
}
```

## 🔧 Configuration

The decompiler can be customized by modifying the following parameters in the source:

- `maxInstructions`: Maximum number of instructions to disassemble (default: 150)
- Function prolog patterns in `isFunctionProlog()`
- Output formatting in `CodeGenerator` class

## ⚠️ Limitations

- **Simplified disassembly**: Not all x86-64 instructions are supported
- **No data flow analysis**: Variables are treated independently
- **Limited type inference**: All variables default to `int`
- **No optimization detection**: Cannot reverse compiler optimizations
- **Basic control flow**: Loops and conditionals shown as gotos
- **Import resolution**: External function names not resolved

## 🛣️ Roadmap

- [ ] Full x86-64 instruction set support
- [ ] Advanced control flow reconstruction (if/while/for detection)
- [ ] Data type inference
- [ ] String and constant detection
- [ ] Import/export table parsing
- [ ] Symbol table support
- [ ] Multi-function decompilation
- [ ] Interactive mode with function selection
- [ ] Output to file option
- [ ] ARM architecture support

## 🤝 Contributing

Contributions are welcome! Please feel free to submit pull requests or open issues for bugs and feature requests.

### Development Setup

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments

- x86-64 instruction set documentation from Intel and AMD
- PE format specification from Microsoft
- ELF format specification from System V ABI

## 📞 Contact

**Developer**: @slyemane  
**GitHub**: https://github.com/slyemane

---

**Copyright (C) 2025 @slyemane - All Rights Reserved**
