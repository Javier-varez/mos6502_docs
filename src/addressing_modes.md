# Addressing modes

Available addressing modes are listed below.

## Accumulator

The argument is provided automatically from the accumulator.

## Absolute

The argument is provided at the given absolute address.

## Absolute, X-Indexed

The argument is provided at the given address + the X index value.

## Absolute, Y-Indexed

The argument is provided at the given address + the Y index value.

## Immediate

The argument is an immediate value provided as part of the instruction. Single byte.

## Implied

The operand is already implied by the opcode itself (not specified externally).

## Indirect

The operand is located at the address located at the address provided in the instruction (2 dereferences).

## X-indexed, indirect

Zeropage absolute address indexed by the X index value. Effective address is (00LL + X)

## Indirect, Y-indexed

Zeropage absolute address. Dereferenced and added to the value of the Y index. Effective address is (00LL) + Y

## Relative

PC + signed offset (used for branching)

## Zeropage

Operand is a zeropage address. Argument is 00LL.

## Zeropage X-indexed

Operand is a zeropage address incremented by X. Argument is 00LL + X.

## Zeropage Y-indexed

Operand is a zeropage address incremented by Y. Argument is 00LL + Y.
