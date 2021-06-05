

# Diagram

```
         CPU z80
|-----------------------|                    RAM (64KB) = 65536 Bytes
|                       |                  |-------------------------|
|   General Registers   |                  |0000...    OS     ...0FFF|
|  |--------|--------|  |<================>|1000...    OS     ...1FFF|
|  |    A   |  Flags |  |<=== DATA BUS ===>|2000...    OS     ...2FFF|
|  |--------|--------|  |<===  8 BITS  ===>|3000...    OS     ...3FFF|
|  |    B   |    C   |  |<================>|4000...  PROGRAM  ...4FFF| OUR PROGRAM starts at 4000 fowards
|  |--------|--------|  |                  |5000...  PROGRAM  ...5FFF|
|  |    D   |    E   |  |                  |6000...  PROGRAM  ...6FFF|
|  |--------|--------|  |=================>|7000...     ~     ...7FFF|
|  |    H   .    L   |  |=================>|8000...     ~     ...8FFF|
|  |--------|--------|  |=================>|9000...     ~     ...9FFF|
|                       |== ADRESS BUS ===>|A000...   STACK   ...AFFF|
|  |-----------------|  |==   16 BITS  ===>|B000...   STACK   ...BFFF| STACK starts at BFFF backwards
|  | Program Counter |  |=================>|C000...   VIDEO   ...CFFF| VIDEO starts at C000 fowards
|  |-----------------|  |=================>|D000...   VIDEO   ...DFFF|
|  |  Stack Pointer  |  |=================>|E000...   VIDEO   ...EFFF|
|  |-----------------|  |                  |F000...   VIDEO   ...FFFF|
|                       |                  |-------------------------|
|-----------------------|
```

> Z80 is LITTLE ENDIAN: Bytes are saved in reverse order in memory
> 
> Bytes 45 67 FA -----> Memory FA 67 45


# Instruction Set

There are 256 different instrucctions

### Write CPU registers

| Opcode   | Instruction  | Description         | Bytes | Number of cycles |
|:---------|:-------------|---------------------|:-----:|------------------|
| 3E __    | LD A, n      | A = 8BITS_VALUE     |   2   |                  |
| 06 __    | LD B, n      | B = 8BITS_VALUE     |   2   |                  |
| 26 __    | LD H, n      | H = 8BITS_VALUE     |   2   |                  |
| 21 __ __ | LD LH, nn    | LH = 16BITS_VALUE   |   3   |                  |
| 3A __ __ | LD A, (ADR)  | A = *ADR            |   3   |                  |


### Math operations in CPU

| Opcode   | Instruction  | Description         | Bytes | Number of cycles |
|:---------|:-------------|---------------------|:-----:|------------------|
| 3C       | INC A        | A = A + 1           |   1   |                  |
| 3D       | DEC A        | A = A - 1           |   1   |                  |
| 23       | INC HL       | HL = HL + 1         |   1   |                  |
| 76       | HALT         | Wait 0.003 secs     |   2   |                  |


### ↪️ Jumps

> - **Jump Absolute**: Change the **`PC`** (Program Counter) to a given memory adress.
> - **Jump Relative**: Sum to the current **`PC`** (Program Counter) a ±128 value.

| Opcode   | Instruction  | Description                    | Bytes | Notes 1   | Notes 2       |
|:---------|:-------------|--------------------------------|:-----:|-----------|---------------|
| C3 __ __ | JP ____      | Jump Absolute                  |   3   | Big jump  | Infinite loop |
| 18 __    | JR __        | Jump Relative                  |   2   | ±128 jump | Infinite loop |
| C2 __ __ | JP NZ ____   | Jump Absolute If Not Zero      |   3   | Big jump  | In range loop |
| 20 __    | JR NZ, __    | Jump Relative If Not Zero      |   2   | ±128 jump | In range loop |
| CD __ __ | CALL ____    | Jump & save next addr on stack |   3   |           |               |
| C9       | RET          | Jump back to last stack addr   |   1   |           |               |


### Write in memory

| Opcode   | Instruction  | Description         | Bytes | Number of cycles |                             |
|:---------|:-------------|---------------------|:-----:|------------------|-----------------------------|
| 32 __ __ | LD (ADR), A  | *ADR = A            |   3   |                  | Used for write video memory |
| 22 __ __ | LD (ADR), LH | *ADR = LH           |   3   |                  |                             |
| 36 __    | LD (HL), n   | *LH = VALUE         |   2   |                  |                             |



# Assembly automatization extras

There are several things from assembly language that **Dont exists in machine code**:

- `$` Dollar sign to compute current memery psition of the program
- Function labels





