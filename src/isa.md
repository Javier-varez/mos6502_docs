# Instruction Set Architecture

The original NMOS version of the 6502 has 151 legal opcodes.
Out of the total number of possible opcodes, ilegal opcodes have been found
to be sometimes useful.

Let's start with the legal instructions for now. The following table summarizes all instructions with their opcodes and addressing modes.

| Nmemonic | Opcode        | Addressing mode       | Modified Flags | Description                                                                     |
|----------|---------------|-----------------------| ---------------|---------------------------------------------------------------------------------|
| ADC      | 69'h          | Immediate             | N, Z, C, V     | Add with carry: A + M + C -> A, C.                                              |
|          | 65'h          | Zeropage              |                |                                                                                 |
|          | 75'h          | Zeropage, X-Indexed   |                |                                                                                 |
|          | 6D'h          | Absolute              |                |                                                                                 |
|          | 7D'h          | Absolute, X-Indexed   |                |                                                                                 |
|          | 79'h          | Absolute, Y-Indexed   |                |                                                                                 |
|          | 61'h          | X-Indexed, Indirect   |                |                                                                                 |
|          | 71'h          | Indirect, Y-Indexed   |                |                                                                                 |
| AND      | 29'h          | Immediate             | N, Z           | And mem with Accumulator: A AND M -> A                                          |
|          | 25'h          | Zeropage              |                |                                                                                 |
|          | 35'h          | Zeropage, X-Indexed   |                |                                                                                 |
|          | 2D'h          | Absolute              |                |                                                                                 |
|          | 3D'h          | Absolute, X-Indexed   |                |                                                                                 |
|          | 39'h          | Absolute, Y-Indexed   |                |                                                                                 |
|          | 21'h          | X-Indexed, Indirect   |                |                                                                                 |
|          | 31'h          | Indirect, Y-Indexed   |                |                                                                                 |
| ASL      | 0A'h          | Accumulator           | N, Z, C        | Shift left one bit (Memory or accumulator)                                      |
|          | 06'h          | Zeropage              |                |                                                                                 |
|          | 16'h          | Zeropage, X-Indexed   |                |                                                                                 |
|          | 0E'h          | Absolute              |                |                                                                                 |
|          | 1E'h          | Absolute, X-Indexed   |                |                                                                                 |
| BCC      | 90'h          | Relative              |                | Branch if carry is clear                                                        |
| BCS      | B0'h          | Relative              |                | Branch if carry is set                                                          |
| BEQ      | F0'h          | Relative              |                | Branch if Z flag is set                                                         |
| BIT      | 24'h          | Zeropage              | N, Z, V        | M7 -> N, M6 -> V, (M AND A == 0) -> Z                                           |
|          | 2C'h          | Absolute              |                |                                                                                 |
| BMI      | 30'h          | Relative              |                | Branch if N is set                                                              |
| BNE      | D0'h          | Relative              |                | Branch if Z is not set                                                          |
| BPL      | 10'h          | Relative              |                | Branch if N is not set                                                          |
| BRK      | 00'h          | Implied               | I              | Triggers a software interrupt. Pushes the PC+2 and SP to the stack              |
| BVC      | 50'h          | Relative              |                | Branch if V is not set                                                          |
| BVS      | 70'h          | Relative              |                | Branch if V is set                                                              |
| CLC      | 18'h          | Implied               |                | Clear Carry Flag                                                                |
| CLD      | D8'h          | Implied               |                | Clear Decimal mode                                                              |
| CLI      | D8'h          | Implied               |                | Clear Interrupt disable bit                                                     |
| CLV      | 58'h          | Implied               |                | Clear overflow flag                                                             |
| CMP      | C9'h          | Immediate             | N, Z, C        | Compare memory with accumulator (A-M). Result is not stored.                    |
|          | C5'h          | Zeropage              |                |                                                                                 |
|          | D5'h          | Zeropage, X-Indexed   |                |                                                                                 |
|          | CD'h          | Absolute              |                |                                                                                 |
|          | DD'h          | Absolute, X-Indexed   |                |                                                                                 |
|          | D9'h          | Absolute, Y-Indexed   |                |                                                                                 |
|          | C1'h          | X-Indexed, Indirect   |                |                                                                                 |
|          | D1'h          | Indirect, Y-Indexed   |                |                                                                                 |
| CPX      | E0'h          | Immediate             | N, Z, C        | Compare memory and Index X (X - M). The result is not stored.                   |
|          | E4'h          | Zeropage              |                |                                                                                 |
|          | EC'h          | Absolute              |                |                                                                                 |
| CPY      | C0'h          | Immediate             | N, Z, C        | Compare memory and Index Y (Y - M). The result is not stored.                   |
|          | C4'h          | Zeropage              |                |                                                                                 |
|          | CC'h          | Absolute              |                |                                                                                 |
| DEC      | C6'h          | Zeropage              | N, Z           | Decrement memory by one (M - 1) -> M.                                           |
|          | D6'h          | Zeropage, X-Indexed   |                |                                                                                 |
|          | CE'h          | Absolute              |                |                                                                                 |
|          | DE'h          | Absolute, X-Indexed   |                |                                                                                 |
| DEX      | CA'h          | Implied               | N, Z           | Decrement X by one (X - 1) -> X.                                                |
| DEY      | 88'h          | Implied               | N, Z           | Decrement Y by one (Y - 1) -> Y.                                                |
| EOR      | 49'h          | Immediate             | N, Z           | Exclusive or Acc with Memory (A XOR M) -> A.                                    |
|          | 45'h          | Zeropage              |                |                                                                                 |
|          | 55'h          | Zeropage, X-Indexed   |                |                                                                                 |
|          | 4D'h          | Absolute              |                |                                                                                 |
|          | 5D'h          | Absolute, X-Indexed   |                |                                                                                 |
|          | 59'h          | Absolute, Y-Indexed   |                |                                                                                 |
|          | 41'h          | X-Indexed, Indirect   |                |                                                                                 |
|          | 51'h          | Indirect, Y-Indexed   |                |                                                                                 |
| INC      | E6'h          | Zeropage              | N, Z           | Increment memory by one (M + 1) -> M.                                           |
|          | F6'h          | Zeropage, X-Indexed   |                |                                                                                 |
|          | EE'h          | Absolute              |                |                                                                                 |
|          | FE'h          | Absolute, X-Indexed   |                |                                                                                 |
| INX      | E8'h          | Implied               | N, Z           | Increment X by one (X + 1) -> X.                                                |
| INY      | C8'h          | Implied               | N, Z           | Increment Y by one (Y + 1) -> Y.                                                |
| JMP      | 4C'h          | Absolute              |                | Jump to the memory location                                                     |
|          | 6C'h          | Indirect              |                |                                                                                 |
| JSR      | 20'h          | Absolute              |                | Jump to subrutine (Saves return address in the stack)                           |
| LDA      | A9'h          | Immediate             | N, Z           | Loads the accumulator with memory.                                              |
|          | A5'h          | Zeropage              |                |                                                                                 |
|          | B5'h          | Zeropage, X-Indexed   |                |                                                                                 |
|          | AD'h          | Absolute              |                |                                                                                 |
|          | BD'h          | Absolute, X-Indexed   |                |                                                                                 |
|          | B9'h          | Absolute, Y-Indexed   |                |                                                                                 |
|          | A1'h          | X-Indexed, Indirect   |                |                                                                                 |
|          | B1'h          | Indirect, Y-Indexed   |                |                                                                                 |
| ORA      | 01'h          | X-Indexed, Indirect   | N,Z            | Or memory with Accumulator. A OR M -> A.                                        |
|          | 05'h          | Zeropage              |                |                                                                                 |
|          | 09'h          | Immediate             |                |                                                                                 |
|          | 0D'h          | Absolute              |                |                                                                                 |
|          | 11'h          | Indirect, Y-Indexed   |                |                                                                                 |
|          | 15'h          | Zeropage, X-Indexed   |                |                                                                                 |
|          | 19'h          | Absolute, Y-Indexed   |                |                                                                                 |
|          | 1D'h          | Absolute, X-Indexed   |                |                                                                                 |
