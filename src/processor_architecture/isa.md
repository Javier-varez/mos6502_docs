# Instruction Set Architecture

The original NMOS version of the 6502 has 151 legal opcodes.
Out of the total number of possible opcodes, ilegal opcodes have been found to be sometimes useful.

The ISA included in this page will cover the legal opcodes. Ilegal opcodes may be added in the future as an extension to this page.

The instructions can be categorized according to the type of operation they perform. We can distinguish between the following categories:

* **Logical and bit manipulation operations**. Operations such as AND, OR, XOR, etc.
* **Arithmetic operations**. Operations such as ADD, SUBSTRACT, INCREMENT, etc.
* **Data shifting instructions**. Shift values in registers. Can be either logical, arithmetic or rotation instructions.
* **Program control flow operations**. Control the flow of the program. They allow to set/modify the value of the program counter.
* **Memory transfer operations**. Transfers memory between different parts of the system (Mainly processor and main memory).

## Logical and bit manipulation operations

### Logical operations

| Mnemonic | Opcode        | Addressing mode       | Modified Flags | Description                                                                     |
|----------|---------------|-----------------------| ---------------|---------------------------------------------------------------------------------|
| **AND**  | `29'h`        | Immediate             | `N, Z`         | And `M` with `A`: `A AND M -> A`                                                |
|          | `25'h`        | Zeropage              |                |                                                                                 |
|          | `35'h`        | Zeropage, X-Indexed   |                |                                                                                 |
|          | `2D'h`        | Absolute              |                |                                                                                 |
|          | `3D'h`        | Absolute, X-Indexed   |                |                                                                                 |
|          | `39'h`        | Absolute, Y-Indexed   |                |                                                                                 |
|          | `21'h`        | X-Indexed, Indirect   |                |                                                                                 |
|          | `31'h`        | Indirect, Y-Indexed   |                |                                                                                 |
| **ORA**  | `09'h`        | Immediate             | `N, Z`         | Or `M` with `A`. `A OR M -> A.`                                                 |
|          | `05'h`        | Zeropage              |                |                                                                                 |
|          | `15'h`        | Zeropage, X-Indexed   |                |                                                                                 |
|          | `0D'h`        | Absolute              |                |                                                                                 |
|          | `1D'h`        | Absolute, X-Indexed   |                |                                                                                 |
|          | `19'h`        | Absolute, Y-Indexed   |                |                                                                                 |
|          | `01'h`        | X-Indexed, Indirect   |                |                                                                                 |
|          | `11'h`        | Indirect, Y-Indexed   |                |                                                                                 |
| **EOR**  | `49'h`        | Immediate             | `N, Z`         | Exclusive or `A` with `M`. `(A XOR M) -> A.`                                    |
|          | `45'h`        | Zeropage              |                |                                                                                 |
|          | `55'h`        | Zeropage, X-Indexed   |                |                                                                                 |
|          | `4D'h`        | Absolute              |                |                                                                                 |
|          | `5D'h`        | Absolute, X-Indexed   |                |                                                                                 |
|          | `59'h`        | Absolute, Y-Indexed   |                |                                                                                 |
|          | `41'h`        | X-Indexed, Indirect   |                |                                                                                 |
|          | `51'h`        | Indirect, Y-Indexed   |                |                                                                                 |

### Comparison operations

| Mnemonic | Opcode        | Addressing mode       | Modified Flags | Description                                                                     |
|----------|---------------|-----------------------| ---------------|---------------------------------------------------------------------------------|
| **CMP**  | `C9'h`        | Immediate             | `N, Z, C`      | Compare `M` with `A`. `(A-M)`. Result is not stored.                            |
|          | `C5'h`        | Zeropage              |                |                                                                                 |
|          | `D5'h`        | Zeropage, X-Indexed   |                |                                                                                 |
|          | `CD'h`        | Absolute              |                |                                                                                 |
|          | `DD'h`        | Absolute, X-Indexed   |                |                                                                                 |
|          | `D9'h`        | Absolute, Y-Indexed   |                |                                                                                 |
|          | `C1'h`        | X-Indexed, Indirect   |                |                                                                                 |
|          | `D1'h`        | Indirect, Y-Indexed   |                |                                                                                 |
| **CPX**  | `E0'h`        | Immediate             | `N, Z, C`      | Compare `M` and `X`. `(X - M)`. The result is not stored.                       |
|          | `E4'h`        | Zeropage              |                |                                                                                 |
|          | `EC'h`        | Absolute              |                |                                                                                 |
| **CPY**  | `C0'h`        | Immediate             | `N, Z, C`      | Compare `M` and `Y`. `(Y - M)`. The result is not stored.                       |
|          | `C4'h`        | Zeropage              |                |                                                                                 |
|          | `CC'h`        | Absolute              |                |                                                                                 |
| **NOP**  | `EA'h`        | Implied               |                | NOP.                                                                            |

### Bit manipulation operations

| Mnemonic | Opcode        | Addressing mode       | Modified Flags | Description                                                                     |
|----------|---------------|-----------------------| ---------------|---------------------------------------------------------------------------------|
| **BIT**  | `24'h`        | Zeropage              | `N, Z, V`      | `M7 -> N`, `M6 -> V`, `(M AND A == 0) -> Z`.                                    |
|          | `2C'h`        | Absolute              |                |                                                                                 |
| **CLC**  | `18'h`        | Implied               |                | Clear `C` flag.                                                                 |
| **CLD**  | `D8'h`        | Implied               |                | Clear `D` flag.                                                                 |
| **CLI**  | `58'h`        | Implied               |                | Clear `I` flag.                                                                 |
| **CLV**  | `B8'h`        | Implied               |                | Clear `O` flag.                                                                 |
| **SEC**  | `38'h`        | Implied               | `C`            | Set `C` flag.                                                                   |
| **SED**  | `F8'h`        | Implied               | `D`            | Set `D` flag.                                                                   |
| **SEI**  | `78'h`        | Implied               | `I`            | Set `I` flag.                                                                   |

## Arithmetic Operations

### Add/substract

| Mnemonic | Opcode        | Addressing mode       | Modified Flags | Description                                                                     |
|----------|---------------|-----------------------| ---------------|---------------------------------------------------------------------------------|
| **ADC**  | `69'h`        | Immediate             | `N, Z, C, V`   | Add with carry: `A + M + C -> A, C`.                                            |
|          | `65'h`        | Zeropage              |                |                                                                                 |
|          | `75'h`        | Zeropage, X-Indexed   |                |                                                                                 |
|          | `6D'h`        | Absolute              |                |                                                                                 |
|          | `7D'h`        | Absolute, X-Indexed   |                |                                                                                 |
|          | `79'h`        | Absolute, Y-Indexed   |                |                                                                                 |
|          | `61'h`        | X-Indexed, Indirect   |                |                                                                                 |
|          | `71'h`        | Indirect, Y-Indexed   |                |                                                                                 |
| **SBC**  | `E9'h`        | Immediate             | `N, Z, C, V`   | Subtract `M` from `A` with borrow. `(A - M - Cbar) -> A`.                       |
|          | `E5'h`        | Zeropage              |                |                                                                                 |
|          | `F5'h`        | Zeropage, X-Indexed   |                |                                                                                 |
|          | `ED'h`        | Absolute              |                |                                                                                 |
|          | `FD'h`        | Absolute, X-Indexed   |                |                                                                                 |
|          | `F9'h`        | Absolute, Y-Indexed   |                |                                                                                 |
|          | `E1'h`        | X-Indexed, Indirect   |                |                                                                                 |
|          | `F1'h`        | Indirect, Y-Indexed   |                |                                                                                 |

### Increment/Decrement

| Mnemonic | Opcode        | Addressing mode       | Modified Flags | Description                                                                     |
|----------|---------------|-----------------------| ---------------|---------------------------------------------------------------------------------|
| **INC**  | `E6'h`        | Zeropage              | `N, Z`         | Increment `M` by one. `(M + 1) -> M`.                                           |
|          | `F6'h`        | Zeropage, X-Indexed   |                |                                                                                 |
|          | `EE'h`        | Absolute              |                |                                                                                 |
|          | `FE'h`        | Absolute, X-Indexed   |                |                                                                                 |
| **INX**  | `E8'h`        | Implied               | `N, Z`         | Increment `X` by one. `(X + 1) -> X`.                                           |
| **INY**  | `C8'h`        | Implied               | `N, Z`         | Increment `Y` by one. `(Y + 1) -> Y`.                                           |
| **DEC**  | `C6'h`        | Zeropage              | `N, Z`         | Decrement `M` by one. `(M - 1) -> M`.                                           |
|          | `D6'h`        | Zeropage, X-Indexed   |                |                                                                                 |
|          | `CE'h`        | Absolute              |                |                                                                                 |
|          | `DE'h`        | Absolute, X-Indexed   |                |                                                                                 |
| **DEX**  | `CA'h`        | Implied               | `N, Z`         | Decrement `X` by one. `(X - 1) -> X`.                                           |
| **DEY**  | `88'h`        | Implied               | `N, Z`         | Decrement `Y` by one. `(Y - 1) -> Y`.                                           |

## Data shifting instructions

| Mnemonic | Opcode        | Addressing mode       | Modified Flags | Description                                                                     |
|----------|---------------|-----------------------| ---------------|---------------------------------------------------------------------------------|
| **LSR**  | `4A'h`        | Accumulator           | `N(0), Z, C`   | Logical shift right (1 bit).                                                    |
|          | `46'h`        | Zeropage              |                |                                                                                 |
|          | `56'h`        | Zeropage, X-Indexed   |                |                                                                                 |
|          | `4E'h`        | Absolute              |                |                                                                                 |
|          | `5E'h`        | Absolute, X-Indexed   |                |                                                                                 |
| **ASL**  | `0A'h`        | Accumulator           | `N, Z, C`      | Arithmetic shift left by one bit (`M` or `A`).                                  |
|          | `06'h`        | Zeropage              |                |                                                                                 |
|          | `16'h`        | Zeropage, X-Indexed   |                |                                                                                 |
|          | `0E'h`        | Absolute              |                |                                                                                 |
|          | `1E'h`        | Absolute, X-Indexed   |                |                                                                                 |
| **ROL**  | `2A'h`        | Accumulator           | `N, Z, C`      | Rotate one bit left (Circular rotation, including `C` bit).                     |
|          | `26'h`        | Zeropage              |                |                                                                                 |
|          | `36'h`        | Zeropage, X-Indexed   |                |                                                                                 |
|          | `2E'h`        | Absolute              |                |                                                                                 |
|          | `3E'h`        | Absolute, X-Indexed   |                |                                                                                 |
| **ROR**  | `6A'h`        | Accumulator           | `N, Z, C`      | Rotate one bit left (Circular rotation, including `C` bit).                     |
|          | `66'h`        | Zeropage              |                |                                                                                 |
|          | `76'h`        | Zeropage, X-Indexed   |                |                                                                                 |
|          | `6E'h`        | Absolute              |                |                                                                                 |
|          | `7E'h`        | Absolute, X-Indexed   |                |                                                                                 |

## Program control flow operations

### Jump instructions (Absolute Address)

| Mnemonic | Opcode        | Addressing mode       | Modified Flags | Description                                                                     |
|----------|---------------|-----------------------| ---------------|---------------------------------------------------------------------------------|
| **JMP**  | `4C'h`        | Absolute              |                | Jump to the `M` location.                                                       |
|          | `6C'h`        | Indirect              |                |                                                                                 |

### Branch instructions (Relative to PC)

| Mnemonic | Opcode        | Addressing mode       | Modified Flags | Description                                                                     |
|----------|---------------|-----------------------| ---------------|---------------------------------------------------------------------------------|
| **BCS**  | `B0'h`        | Relative              |                | Branch if `C` is set.                                                           |
| **BCC**  | `90'h`        | Relative              |                | Branch if `C` is clear.                                                         |
| **BEQ**  | `F0'h`        | Relative              |                | Branch if `Z` is set.                                                           |
| **BNE**  | `D0'h`        | Relative              |                | Branch if `Z` is clear                                                          |
| **BMI**  | `30'h`        | Relative              |                | Branch if `N` is set                                                            |
| **BPL**  | `10'h`        | Relative              |                | Branch if `N` is clear                                                          |
| **BVS**  | `70'h`        | Relative              |                | Branch if `V` is set                                                            |
| **BVC**  | `50'h`        | Relative              |                | Branch if `V` is clear                                                          |

### Subroutines

| Mnemonic | Opcode        | Addressing mode       | Modified Flags | Description                                                                     |
|----------|---------------|-----------------------| ---------------|---------------------------------------------------------------------------------|
| **JSR**  | `20'h`        | Absolute              |                | Jump to subrutine (Saves return address in the stack)                           |
| **RTS**  | `60'h`        | Implied               |                | Returns from subroutine. Pulls `PC` from `SP`                                   |

### Interrupts

| Mnemonic | Opcode        | Addressing mode       | Modified Flags | Description                                                                     |
|----------|---------------|-----------------------| ---------------|---------------------------------------------------------------------------------|
| **BRK**  | `00'h`        | Implied               | I              | Triggers a software interrupt. Pushes the `PC+2` and `SP` to the stack          |
| **RTI**  | `40'h`        | Implied               | From `SP`      | Returns from the current ISR. Pulls `P` and `PC`                                |

## Memory transfer operations

### Load/Store from/to memory

| Mnemonic | Opcode        | Addressing mode       | Modified Flags | Description                                                                     |
|----------|---------------|-----------------------| ---------------|---------------------------------------------------------------------------------|
| **LDA**  | `A9'h`        | Immediate             | `N, Z`         | Loads the `A` with `M`.                                                         |
|          | `A5'h`        | Zeropage              |                |                                                                                 |
|          | `B5'h`        | Zeropage, X-Indexed   |                |                                                                                 |
|          | `AD'h`        | Absolute              |                |                                                                                 |
|          | `BD'h`        | Absolute, X-Indexed   |                |                                                                                 |
|          | `B9'h`        | Absolute, Y-Indexed   |                |                                                                                 |
|          | `A1'h`        | X-Indexed, Indirect   |                |                                                                                 |
|          | `B1'h`        | Indirect, Y-Indexed   |                |                                                                                 |
| **STA**  | `85'h`        | Zeropage              |                | Stores the `A` in `M`.                                                          |
|          | `95'h`        | Zeropage, X-Indexed   |                |                                                                                 |
|          | `8D'h`        | Absolute              |                |                                                                                 |
|          | `9D'h`        | Absolute, X-Indexed   |                |                                                                                 |
|          | `99'h`        | Absolute, Y-Indexed   |                |                                                                                 |
|          | `81'h`        | X-Indexed, Indirect   |                |                                                                                 |
|          | `91'h`        | Indirect, Y-Indexed   |                |                                                                                 |
| **LDX**  | `A2'h`        | Immediate             | `N, Z`         | Loads the `X` register with `M`.                                                |
|          | `A6'h`        | Zeropage              |                |                                                                                 |
|          | `B6'h`        | Zeropage, Y-Indexed   |                |                                                                                 |
|          | `AE'h`        | Absolute              |                |                                                                                 |
|          | `BE'h`        | Absolute, Y-Indexed   |                |                                                                                 |
| **STX**  | `86'h`        | Zeropage              |                | Stores the `X` register in `M`.                                                 |
|          | `96'h`        | Zeropage, Y-Indexed   |                |                                                                                 |
|          | `8E'h`        | Absolute              |                |                                                                                 |
| **LDY**  | `A0'h`        | Immediate             | `N, Z`         | Loads the `Y` register with `M`.                                                |
|          | `A4'h`        | Zeropage              |                |                                                                                 |
|          | `B4'h`        | Zeropage, X-Indexed   |                |                                                                                 |
|          | `AC'h`        | Absolute              |                |                                                                                 |
|          | `BC'h`        | Absolute, X-Indexed   |                |                                                                                 |
| **STY**  | `84'h`        | Zeropage              |                | Stores the `Y` register in `M`.                                                 |
|          | `94'h`        | Zeropage, X-Indexed   |                |                                                                                 |
|          | `8C'h`        | Absolute              |                |                                                                                 |

### Register data transfer operations

| Mnemonic | Opcode        | Addressing mode       | Modified Flags | Description                                                                     |
|----------|---------------|-----------------------| ---------------|---------------------------------------------------------------------------------|
| **TAX**  | `AA'h`        | Implied               |                | Transfer `A` to `X`. `A -> X`.                                                  |
| **TXA**  | `8A'h`        | Implied               |                | Transfer `X` to `A`. `X -> A`.                                                  |
| **TAY**  | `A8'h`        | Implied               |                | Transfer `A` to `Y`. `A -> Y`.                                                  |
| **TYA**  | `98'h`        | Implied               |                | Transfer `Y` to `A`. `Y -> A`.                                                  |
| **TSX**  | `BA'h`        | Implied               |                | Transfer `SP` to `X`. `SP -> X`.                                                |
| **TXS**  | `9A'h`        | Implied               |                | Transfer `X` to `SP`. `X -> SP`.                                                |

### Stack operations

| Mnemonic | Opcode        | Addressing mode       | Modified Flags | Description                                                                     |
|----------|---------------|-----------------------| ---------------|---------------------------------------------------------------------------------|
| **PHA**  | `48'h`        | Implied               |                | Push `A` to the stack.                                                          |
| **PLA**  | `68'h`        | Implied               |                | Pull `A` from the stack.                                                        |
| **PHP**  | `08'h`        | Implied               |                | Push `P` to the stack.                                                          |
| **PLP**  | `28'h`        | Implied               |                | Pull `P` from the stack.                                                        |
