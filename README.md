# samsung-riscv
## C Language Based Lab
## Basic Details:
Name: B M Vikas

College: Vidyavardhaka College of Engineering

Email ID: bmvikas25@gmail.com

GitHub Profile: VIKAS2504
<details>
<summary><b>Task 1:</b> Task 1: To compile C code, use the GCC compiler for the native architecture, or utilize a cross-compiling toolchain to target the RISC-V architecture. simulator</summary>   
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
<summary><b>Task 2:</b> Task 2: The task is to review the C-based and RISC-V-based lab videos and perform the compilation of C code using both the GCC and RISC-V compilers.. simulator</summary>   
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
<summary><b>Task 3:</b> Task 3:The task is to identify the instruction type for each provided instruction and provide the corresponding 32-bit instruction codes in the correct format.simulator</summary>   
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
</details>

