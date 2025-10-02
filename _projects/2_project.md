---
layout: page
title:  x86 Mini CPU Simulator
description:  A 16-bit CPU simulator with a custom ISA, assembler-style parser, and graphical debugger
img: assets/img/icon.jpeg
importance: 2
categories: ["Academic"]
permalink: /projects/cpu-simulator
related_publications: false
---

A lightweight **16-bit CPU simulator** I built with:
- custom **ISA** (register file, flags, stack, branches, ALU ops),
- an assembler-style **parser** (labels, immediates, `[mem]`, `[reg+reg]`),
- a step/run **debugger UI** (register/memory/flags view).

Source:
- 🧩 Core: `cpu.cpp`, `cpu.h`  
- 🧩 Parser: `parser.cpp`, `parser.h`  
- 🔗 Repo: <https://github.com/B1gF1sh/x86-MINI_SIM>  <!-- kendi linkinle değiştir -->

---

## Screens

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/gui_push_cpu_SIM.jpeg" title="GUI – registers, flags, memories" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/opcodes_last.jpeg" title="Instruction set overview" class="img-fluid rounded z-depth-1" %}
  </div>
</div>

---

## Key Features
- **Registers:** AX, BX, CX, DX, MNK + SP, BP, SI, DI, IP  
- **Flags:** CF, ZF, SF, OF  
- **Memory:** byte/word read-write, stack via SP  
- **Addressing:** `imm`, `[imm]`, `[reg]`, `[reg+reg]`, 8-bit/16-bit variants  
- **Control flow:** `CALL/RET`, `JMP`, `JZ/JNZ`, `JC/JNC`, `JS/JNS`, `JO/JNO`  
- **ALU:** `ADD/SUB/ADC/SBB`, `AND/OR/XOR/NOT/NEG`, **shifts/rotates** (imm & `CL`)  
- **Move forms:** reg↔reg, reg↔mem, imm→reg/mem (8/16-bit)

---

## Example (store & compare)

{% highlight asm %}
; Write 0x1234 into memory[0x0031], read back, compare, branch
MOV AX, 1234h
MOV [0031h], AX
MOV BX, [0031h]
CMP AX, BX
JZ OK
HALT
OK:
CALL PRINT
RET
{% endhighlight %}

> two pass parser for labels **first pass** address decoding → **second pass** code production.

---

## How it works (very short)
- `CPU::run/step()` decodes related opcodes and calls;  `write_mem* / read_mem*` and **flag update** helpers.  
- Parser parses operand types (REG16/REG8/IMM/MEM/REG+REG/LABEL), writes the correct **opcode** sequence.

---

## Build / Run
```bash
g++ -std=c++17 -O2 cpu.cpp parser.cpp -o cpu_sim
./cpu_sim
