# samsung-riscv
## C Language Based Lab

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

