## C Language Based Lab
## Basic Details:
Name: B M Vikas

College: Vidyavardhaka College of Engineering

Email ID: bmvikas25@gmail.com

GitHub Profile: VIKAS2504
<details>
<summary><b>Task 1:</b> Task 1: To compile C code, use the GCC compiler for the native architecture, or utilize a cross-compiling toolchain to target the RISC-V architecture. </summary>   
<br>
   
### Compilation using GCC Compiler

Execution of sum1ton.c file

1. Open the bash terminal and navigate to the directory where you want to create your file.
2. Run the following command to create and open the file in the editor:
   ```bash
   gedit sum1ton.c
3. Use these commands to run the C code:
   ```bash
   gcc sum_1ton.c
   ./a.out
  ![Code](https://github.com/user-attachments/assets/c3bbbc08-4d9c-4292-8bd0-3be40754b7f1)

### RISC-V
  ```
  cat sum1ton.c
  riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
  riscv64-unknown-elf-objdump -d sum1ton.o
  ```

![riscv](https://github.com/user-attachments/assets/530c95b8-4d3d-4bdf-a3ad-286740dc4f70)

To locate main in code use `/main`
![riscvmain](https://github.com/user-attachments/assets/5ba725be-498b-4b3a-8421-e60a96e78ea3)
</details>

<details>
<summary><b>Task 2:</b> Task 2: The task is to review the C-based and RISC-V-based lab videos and perform the compilation of C code using both the GCC and RISC-V compilers. </summary>   
<br>
   
### RISC-V SPIKE Simulator 

This guide provides detailed instructions to install *SPIKE, a RISC-V ISA simulator, and the **Proxy Kernel (pk)* for running RISC-V programs. By following this document, you can test, debug, and analyze RISC-V applications efficiently.  

### Introduction to SPIKE  
SPIKE is an open-source simulator for the RISC-V ISA, written in C++. It models RISC-V cores and cache systems, allowing developers to test programs and operating systems like Linux without requiring actual hardware.  

### Testing SPIKE with a Sample Program  

Test your SPIKE installation using a simple program (sum_1ton.c). Compile and execute it with both GCC and the RISC-V compiler to compare results.  

### Compile and Run with GCC 
```
gcc sum_1ton.c  
./a.out
```
![VirtualBox_vsdworkshop_13_01_2025_20_50_53](https://github.com/user-attachments/assets/6e9fa614-7db8-4e08-a1ca-100ae25d6ce5)

  
### Compile and Run with SPIKE  
```
spike pk sum_1ton.o
```
### Assembly Code Analysis  

To inspect the assembly language output of a compiled program, use:  
```
riscv64-unknown-elf-objdump -d sum_1ton.o | less
```
![VirtualBox_vsdworkshop_13_01_2025_20_48_01](https://github.com/user-attachments/assets/037ef66d-fc3d-4c91-9249-0eb3c95f8c07)



### Debugging RISC-V Programs with SPIKE  

Debug your programs by following these steps:  

1. Open the debugger:  
   ``` sh
   spike -d pk sum_1ton.o
   ```
2. Perform debugging tasks using the interactive terminal.  

### Compiler Optimization Levels  

Use optimization flags during compilation to observe how the output changes:  

-O1 Optimization:** Basic optimizations for improved performance without significant trade-offs. 

-Ofast Optimization:** Aggressive optimizations that maximize performance but may compromise accuracy.  

Compare the objdump outputs for different optimization levels to analyze their impact.  
![VirtualBox_vsdworkshop_13_01_2025_20_47_10](https://github.com/user-attachments/assets/3eb307b4-0284-4501-b521-34d2f4d0317e)
</details>

<details>
<summary><b>Task 3:</b> Task 3:The task is to identify the instruction type for each provided instruction and provide the corresponding 32-bit instruction codes in the correct format. </summary>   
<br>
   
# Understanding RISC-V Instruction Set Architecture (ISA)

## RISC-V Instruction Formats
In RISC-V, the instruction format specifies how machine language instructions are structured for execution. These instructions consist of binary data (0s and 1s), where different segments indicate the operation to be performed and the data location. The following are the six primary instruction formats in RISC-V:

- R-format
- I-format
- S-format
- B-format
- U-format
- J-format

Each of these formats plays a crucial role in defining how the processor interprets and executes instructions.

![Screenshot 2025-01-15 162208](https://github.com/user-attachments/assets/a9f9bf72-e753-40b6-9635-2d6cdd1737db)

---

## R-Type Instructions :
Used for register-register operations, such as arithmetic and logic operations. The format includes fields for two source registers, a destination register, and the operation type.

| **Field**  | **Bit Size** | **Description**                                                  |
|------------|--------------|------------------------------------------------------------------|
| `opcode`   | 7            | Operation code to determine the type of instruction.            |
| `rd`       | 5            | Destination register to store the result.                       |
| `func3`    | 3            | Specifies the operation category (arithmetic, logical, etc.).   |
| `rs1`      | 5            | First source register.                                          |
| `rs2`      | 5            | Second source register.                                         |
| `func7`    | 7            | Provides additional operation-specific details.                 |
| **Total**  | 32           |                                                                |


Ex : add x3, x1, x2

- Opcode: add
- Format: add rd, rs1, rs2

   - rd: Destination register (where the result is stored) – x3
   
   - rs1: First source register – x1
   
   - rs2: Second source register – x2

![R-type](https://github.com/maazm007/vsdsquadron-mini-internship/assets/83294849/4a17f03e-ae74-4809-a8d9-79924fb8b421) 
---

## I-Type Instructions : 
Used for operations involving immediate values, such as load, arithmetic, and branch instructions. It includes a 12-bit immediate, a source register, and a destination register.

| **Field**    | **Bit Size** | **Description**                                                  |
|--------------|--------------|------------------------------------------------------------------|
| `opcode`     | 7            | Operation code to determine the type of instruction.            |
| `rd`         | 5            | Destination register to store the result.                       |
| `func3`      | 3            | Specifies the operation category.                               |
| `rs1`        | 5            | Source register.                                                |
| `imm[11:0]`  | 12           | 12-bit signed immediate value.                                  |
| **Total**    | 32           |                                                                |

Ex : lw x3, 4(x1)

- Opcode: lw
- Format: lw rd, imm(rs1)

   - rd: Destination register (where the value is stored) – x3

   - imm: Immediate value (offset) – 4

   - rs1: Base register – x1
     
![I-type](https://github.com/maazm007/vsdsquadron-mini-internship/assets/83294849/4a53f5fa-d55a-4308-8f93-a0f2f3aedba0)
---

## S-Type Instructions :
Used for store instructions. It includes a 12-bit immediate (representing the offset), and two registers—one holding the data to store and the other holding the address.

| **Field**    | **Bit Size** | **Description**                                                  |
|--------------|--------------|------------------------------------------------------------------|
| `opcode`     | 7            | Operation code to determine the type of instruction.            |
| `imm[11:5]`  | 7            | Upper bits of a 12-bit signed immediate value.                  |
| `rs1`        | 5            | Base address register for memory operations.                   |
| `rs2`        | 5            | Register containing the value to store.                        |
| `imm[4:0]`   | 5            | Lower bits of a 12-bit signed immediate value.                  |
| `func3`      | 3            | Specifies data size and type.                                   |
| **Total**    | 32           |                                                                |

Ex : sw x3, 8(x1)

- Opcode: sw
- Format: sw rs2, imm(rs1)

   - rs2: Source register (the value to be stored) – x3

   - imm: Immediate value (offset) – 8

   - rs1: Base register (used for the address calculation) – x1

![s-type](https://github.com/maazm007/vsdsquadron-mini-internship/assets/83294849/fc9ddedc-4c99-4b6f-9765-c2e8c8e29302)
---

## B-Type Instructions :
Used for branch instructions that compare two registers and branch if the comparison is true. It includes a 12-bit immediate for the branch offset and two registers to compare.



| **Field**    | **Bit Size** | **Description**                                                  |
|--------------|--------------|------------------------------------------------------------------|
| `opcode`     | 7            | Operation code to determine the type of instruction.            |
| `imm[12]`    | 1            | Most significant bit of a 12-bit signed immediate value.        |
| `imm[10:5]`  | 6            | Upper middle bits of the immediate value.                       |
| `rs1`        | 5            | First source register for evaluating branch conditions.         |
| `rs2`        | 5            | Second source register for evaluating branch conditions.        |
| `func3`      | 3            | Specifies the branch condition.                                 |
| `imm[4:1]`   | 4            | Lower middle bits of the immediate value.                       |
| `imm[11]`    | 1            | Another middle bit of the immediate value.                      |
| **Total**    | 32           |                                                                |

Ex : beq x1, x2, label

- Opcode: beq
- Format: beq rs1, rs2, offset

   - rs1: First source register – x1
   
   - rs2: Second source register – x2
   
   - offset: The branch offset, calculated relative to the current PC – label

![B-type](https://github.com/maazm007/vsdsquadron-mini-internship/assets/83294849/14486f41-f3e4-4c4a-85b0-9acc56be3f46)
---

## U-Type Instructions : 
Used for upper immediate instructions that load 20-bit immediate values into the upper 20 bits of a register, such as LUI(Load Upper Immediate)and AUIPC(Add Upper Immediate to PC).

| **Field**     | **Bit Size** | **Description**                                                  |
|---------------|--------------|------------------------------------------------------------------|
| `opcode`      | 7            | Operation code to determine the type of instruction.            |
| `rd`          | 5            | Destination register to store the immediate value.              |
| `imm[31:12]`  | 20           | 20-bit upper immediate value.                                   |
| **Total**     | 32           |                                                                |

Ex : lui x5, 0x12345

- Opcode: lui
- Format: lui rd, imm[31:12]

   - rd: Destination register – x5
   
   - imm[31:12]: Upper 20 bits of the immediate value – 0x12345

![u-type](https://github.com/maazm007/vsdsquadron-mini-internship/assets/83294849/4f3df58b-8c0c-45c6-ba39-a196547dd38f)
---

## J-Type Instructions : 
Used for jump instructions, such as JAL(Jump and Link). It includes a 20-bit immediate value representing the jump address offset.

| **Field**     | **Bit Size** | **Description**                                                  |
|---------------|--------------|------------------------------------------------------------------|
| `opcode`      | 7            | Operation code to determine the type of instruction.            |
| `rd`          | 5            | Register to store the return address.                           |
| `imm[20]`     | 1            | Most significant bit of a 20-bit signed immediate value.        |
| `imm[10:1]`   | 10           | Lower middle bits of the immediate value.                       |
| `imm[11]`     | 1            | Another middle bit of the immediate value.                      |
| `imm[19:12]`  | 8            | Upper middle bits of the immediate value.                       |
| **Total**     | 32           |                                                                |

Ex : jal x1, 0x1000

- Opcode: jal
- Format: jal rd, offset

   - rd: Destination register (the return address) – x1
   
   - offset: The jump offset, relative to the current PC – 0x1000

![j-type](https://github.com/maazm007/vsdsquadron-mini-internship/assets/83294849/5dc9a9be-4048-4a35-a99e-7b4a0075caa0)
---

# RISC-V Instruction Analysis

This repository contains an analysis of 15 unique RISC-V instructions extracted from an object file. Each instruction is decoded to include its opcode, format, machine code, and binary representation.

## Overview

This project provides a breakdown of 15 RISC-V instructions. It explains their functionality and how they are encoded in machine language, making it useful for developers interested in low-level programming or CPU architecture.

## 15 Unique Instruction Details

Here are the 15 instructions analyzed in the below attached objdump file:
![objdump](https://github.com/user-attachments/assets/fd16a51e-5ece-4116-9435-bf605906d791)


### 1. `lui`
- **Description:** Load Upper Immediate - Loads a 20-bit immediate into the upper 20 bits of a register.
- **Example:** `00021537`
  - Opcode: `0110111`
  - Format: U-type
  - Binary: `00000000001000010101000000110111`

### 2. `addi`
- **Description:** Add Immediate - Adds an immediate value to a register.
- **Example:** `ff010113`
  - Opcode: `0010011`
  - Format: I-type
  - Binary: `11111111000000010000000000010011`

### 3. `li`
- **Description:** Load Immediate - Loads a small immediate into a register (pseudo-instruction for `addi`).
- **Example:** `00f00613`
  - Opcode: `0010011`
  - Format: I-type
  - Binary: `00000000111100000000000001100011`

### 4. `sd`
- **Description:** Store Doubleword - Stores a 64-bit value from a register into memory.
- **Example:** `00113423`
  - Opcode: `0100111`
  - Format: S-type
  - Binary: `00000000000100010011010000100011`

### 5. `jal`
- **Description:** Jump and Link - Jumps to a specified address and stores the return address in a register.
- **Example:** `340000ef`
  - Opcode: `1101111`
  - Format: J-type
  - Binary: `00110100000000000000000011101111`

### 6. `ld`
- **Description:** Load Doubleword - Loads a 64-bit value from memory into a register.
- **Example:** `00813083`
  - Opcode: `0000011`
  - Format: I-type
  - Binary: `00000000100000010011000010000011`

### 7. `ret`
- **Description:** Return from subroutine (pseudo-instruction for `jalr`).
- **Example:** `00008067`
  - Opcode: `1100111`
  - Format: I-type
  - Binary: `00000000000000001000000001100111`

### 8. `auipc`
- **Description:** Add Upper Immediate to PC - Adds a 20-bit immediate to the program counter.
- **Example:** `ffff0797`
  - Opcode: `0010111`
  - Format: U-type
  - Binary: `11111111111111110000011110010111`

### 9. `beqz`
- **Description:** Branch if Equal to Zero (pseudo-instruction for `beq`).
- **Example:** `00078863`
  - Opcode: `1100011`
  - Format: B-type
  - Binary: `00000000000001111000100001100011`

### 10. `sub`
- **Description:** Subtract - Subtracts the value in one register from another.
- **Example:** `40a60633`
  - Opcode: `0110011`
  - Format: R-type
  - Binary: `01000000101001100000011000110011`

### 11. `j`
- **Description:** Unconditional Jump (pseudo-instruction for `jal`).
- **Example:** `0c00006f`
  - Opcode: `1101111`
  - Format: J-type
  - Binary: `00001100000000000000000001101111`

### 12. `lw`
- **Description:** Load Word - Loads a 32-bit value from memory into a register.
- **Example:** `00012503`
  - Opcode: `0000011`
  - Format: I-type
  - Binary: `00000000000000010010010100000011`

### 13. `jalr`
- **Description:** Jump and Link Register - Jumps to an address in a register and saves the return address.
- **Example:** `f7dff0ef`
  - Opcode: `1100111`
  - Format: I-type
  - Binary: `11110111110111111111000011101111`

### 14. `slli`
- **Description:** Shift Left Logical Immediate - Shifts a register value left by an immediate value.
- **Example:** `00009613`
  - Opcode: `0010011`
  - Format: I-type
  - Binary: `00000000000010010110000001100011`

### 15. `or`
- **Description:** Bitwise OR - Performs a bitwise OR operation between two registers.
- **Example:** `00560633`
  - Opcode: `0110011`
  - Format: R-type
  - Binary: `00000000010101100000011000110011`

</details>

<details>
<summary><b>Task 4:</b> Simulator Setup and Functional Simulation. </summary>   
<br>

### Installation of Iverilog and GTKWave

The installation of Iverilog and GTKWave can be completed using the commands specified below:

```bash
sudo apt update
sudo apt install iverilog
sudo apt install gtkwave
```
A directory is created and execution of verilog and testbench code is done for waveform generation:

![waveform generation](https://github.com/user-attachments/assets/d6580e4a-de93-4f8d-8dc5-093979681fc4)

### Generated Waveform

To view the generated waveform, use the following commands:

```bash
./iiitb_rv32ib
gtkwave iiitb_rv32i.vcd
```
Waveform:
![waveform](https://github.com/user-attachments/assets/4d6d6875-875b-4380-812d-337d08b7d0d5)


### Studying the waveform behavior of different RISC-V instructions

Instruction 1: ADD R6, R2, R1 

![Image 1](https://github.com/user-attachments/assets/37299fb4-bfcf-4272-ad2b-667d042e2479)

---
Instruction 2: SUB R7, R1, R2

![Image 2](https://github.com/user-attachments/assets/4aa852c0-1640-4ebb-b14f-cc6f8fede198)

---
Instruction 3: AND R8, R1, R3

![Image 3](https://github.com/user-attachments/assets/5bb321c2-f3d0-466a-a430-65d472e0dea1)

---
Instruction 4: OR R9, R2, R5

![Image 4](https://github.com/user-attachments/assets/515a22e5-32e9-417c-900d-328b3c619f73)


---

Instruction 5: XOR R10, R1, R4

![Image 5](https://github.com/user-attachments/assets/fa1f9175-2006-4671-9fbb-d4963fc99a90)

---

Instruction 6: SLT R1, R2, R4

![Image 6](https://github.com/user-attachments/assets/55f6deda-1fb2-4fee-896b-20193b3933ec)

---

Instruction 7: ADDI R12, R4, 5

![Image 7](https://github.com/user-attachments/assets/90978298-e69f-4205-9ad3-0a9717fbf9eb)

---

Instruction 8: BEQ R0, R0, 15

![Image 8](https://github.com/user-attachments/assets/4b369951-0f2c-47ff-a2a0-f0ff381c9956)

---

Instruction 9:sw r3,r1,2

![Image 9](https://github.com/user-attachments/assets/f334403e-3a6a-404f-a4fa-66a5070c0fab)

---

Instruction 10:lw r13,r1,2

![Image 10](https://github.com/user-attachments/assets/0f547932-3d99-4a1c-a4fd-ab07e5775ce5)

---
RISCV-5stage-instruction-waveform

![Image 11](https://github.com/user-attachments/assets/99ae5b5a-0eba-4def-9152-f85ce9b87f5c)

</details>




