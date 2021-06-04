

# Diagram

```
|-----|
|     |    Data bus    |-----|
|     |<===/8 bits/===>|     |
|     |                |     |
| z80 |                | RAM |
|     |   Adress bus   |     |
|     |===/16 bits/===>|     |
|     |                |-----|
|-----|
```

# z80 Registers










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
| 76       | HALT         | Wait 0.003 secs     |   2   |                  |


### Jumps

> - **Jump Absolute**: Change the **`PC`** (Program conter) to a given memory adress.
> - **Jump Relative**: Sum to the current **`PC`** (Program conter) a ±128 value.

| Opcode   | Instruction  | Description               | Bytes | Notes 1   | Notes 2       |
|:---------|:-------------|---------------------------|:-----:|-----------|---------------|
| C3 __ __ | JP ____      | Jump Absolute             |   3   | Big jump  | Infinite loop |
| 18 __    | JR __        | Jump Relative             |   2   | ±128 jump | Infinite loop |
| C2 __ __ | JP NZ ____   | Jump Absolute If Not Zero |   3   | Big jump  | In range loop |
| 20 __    | JR NZ, __    | Jump Relative If Not Zero |   2   | ±128 jump | In range loop |


### From CPU back to memory

| Opcode   | Instruction  | Description         | Bytes | Number of cycles |                             |
|:---------|:-------------|---------------------|:-----:|------------------|-----------------------------|
| 32 __ __ | LD (ADR), A  | *ADR = A            |   3   |                  | Used for write video memory |
| 22 __ __ | LD (ADR), LH | *ADR = LH           |   3   |                  |                             |
| 36 __    | LD (HL), n   | *LH = VALUE         |   2   |                  |                             |







