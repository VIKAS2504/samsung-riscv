# samsung-riscv
## C Language Based Lab
## Basic Details:
Name: B M Vikas

College: Vidyavardhaka College of Engineering

Email ID: bmvikas25@gmail.com

GitHub Profile: VIKAS2504

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

## RISC-V
  ```
  cat sum1ton.c
  riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
  riscv64-unknown-elf-objdump -d sum1ton.o
  ```

![riscv](https://github.com/user-attachments/assets/530c95b8-4d3d-4bdf-a3ad-286740dc4f70)

To locate main in code use `/main`
![riscvmain](https://github.com/user-attachments/assets/5ba725be-498b-4b3a-8421-e60a96e78ea3)

# RISC-V SPIKE Simulator 

This guide provides detailed instructions to install *SPIKE, a RISC-V ISA simulator, and the **Proxy Kernel (pk)* for running RISC-V programs. By following this document, you can test, debug, and analyze RISC-V applications efficiently.  

## Introduction to SPIKE  
SPIKE is an open-source simulator for the RISC-V ISA, written in C++. It models RISC-V cores and cache systems, allowing developers to test programs and operating systems like Linux without requiring actual hardware.  

## Testing SPIKE with a Sample Program  

Test your SPIKE installation using a simple program (sum_1ton.c). Compile and execute it with both GCC and the RISC-V compiler to compare results.  

### Compile and Run with GCC 
```
gcc sum_1ton.c  
./a.out
```
  
### Compile and Run with SPIKE  
```
spike pk sum_1ton.o
```
## Assembly Code Analysis  

To inspect the assembly language output of a compiled program, use:  
```
riscv64-unknown-elf-objdump -d sum_1ton.o | less
```


## Debugging RISC-V Programs with SPIKE  

Debug your programs by following these steps:  

1. Open the debugger:  
   ``` sh
   spike -d pk sum_1ton.o
   ```
2. Perform debugging tasks using the interactive terminal.  

## Compiler Optimization Levels  

Use optimization flags during compilation to observe how the output changes:  

-O1 Optimization:** Basic optimizations for improved performance without significant trade-offs. 

-Ofast Optimization:** Aggressive optimizations that maximize performance but may compromise accuracy.  

Compare the objdump outputs for different optimization levels to analyze their impact.  
