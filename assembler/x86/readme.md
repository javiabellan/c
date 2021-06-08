x86 assembly language has two main syntaxs: Intel and AT&T.

|            | Intel syntax                     | AT&T syntax           |
|------------|----------------------------------|-----------------------|
| OS         | Windows and DOS                  | Linux, Unix and MacOS |
| Assemblers | NASM, FASM, MASM, TASM, and YASM | GNU Assembler (GAS)   | 



- By defoult `-S` generates 64bits assembly using AT&T syntax.
- And we want intel syntax, so `-masm=intel`
- And we want 32 bits, so `-m32`


```


                                  
                                  gcc program.c   -o program.o
                                  gcc program.cpp -o program.o
          _________________________________________________________________________________
         /                                                                                 \
        /                                       ______                                      \
       /                                       /      |                                      \
      /   gcc program.c   -S -o program.s     | AT&T  |                                       \
  ___/__  g++ program.cpp -S -o program.s     |  x86  |                                      __V__
 /      | ----------------------------------> | asemb | objdump -S program.o                /     |
| C/C++ |                                     |_______| <--------------------------------  | Obj  | gcc program.o -m32 -o program
| file  |                                       ______                                     | file | ld program.o -m elf_i386 -o program
| .c    | gcc program.c   -S -masm=intel -m32  /      | nasm -f elf program.s  (for linux) |  .o  |------------------------------------
| .cpp  | g++ program.cpp -S -masm=intel -m32 | Intel | nasm -f exe program.s  (for win)   |______|
|_______| ----------------------------------> |  X86  | --------------------------------->
                                              | asemb | 
                                              |  .s   | objdump -S -M intel program.o
                                              |_______| <---------------------------------

 .c/.cpp  --------------COMPILER-------------->  .s  ------------ASSEMBLER---------------->  .o   --------------LINKER---------------> EXEC  

```





# Memory sections
                                                                       Can write during execution
|-----------------|--------------------------------------------------|---------
| `section .text` | Memory space for the **code of the program**     | no
| `section .data` | Memory space for the **initialized variables**   | yes
| `section .bss`  | Extra future memory space that the program needs | yes


# Diagram

```
               CPU x86 32bits
|------------------------------------------------------------|
|                                                            |
|     32bits General Purpose Registers     16bits Status     |
|  |----------------|--------|--------|  |----------------|  |
|  |              [EAX] AH  (AX) AL   |  |                |  |
|  |----------------|--------|--------|  |----------------|  |
|  |              [EBX] BH  (BX) BL   |                      |
|  |----------------|--------|--------|    16bits Segments   |
|  |              [ECX] CH  (CX) CL   |  |----------------|  |
|  |----------------|--------|--------|  |       CS       |  |
|  |              [EDX] DH  (DX) DL   |  |----------------|  |
|  |----------------|--------|--------|  |       DS       |  |
|                                        |----------------|  |
|         32bits Index Registers         |       ES       |  |
|  |----------------------------------|  |----------------|  |
|  |              [ESI]               |  |       FS       |  |
|  |----------------------------------|  |----------------|  |
|  |              [EDI]               |  |       GS       |  |
|  |----------------------------------|  |----------------|  |
|  |       [ESP] Stack Pointer        |  |       SS       |  |
|  |----------------------------------|  |----------------|  |
|  |       [EBP] Base Pointer         |                      |
|  |----------------------------------|                      |
|                                                            |
|  |----------------------------------|                      |
|  |       [EIP] Program Counter      |                      |
|  |----------------------------------|                      |
|                                                            |
|------------------------------------------------------------| 

32bits address bus for up to 4GB of flat addresable RAM.
```





# Hello world


```asm
section .data

   my_message db "hola",0x0A,0    # Define bytes "hola\n"  0x0A=\n  0=End of String in C

section .text
   

