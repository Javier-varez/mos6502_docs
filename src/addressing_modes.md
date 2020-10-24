# Addressing modes

Available addressing modes are listed below.

* **Accumulator**. The operand is the Accumulator.
* **Absolute**. The operand is located at a given absolute address (16-bit addressing-space).
* **Absolute, X-Indexed**. The operand is located at the absolute address + the X index value.
* **Absolute, Y-Indexed**. The operand is located at the absolute address + the Y index value.
* **Immediate**. The operand is encoded with the instruction.
* **Implied**. The operand is implicit in the context of the instruction (not provided by the user).
* **Indirect**. The address field in the instruction contains the memory location where the effective address of the operand is present.
* **X-indexed, indirect**. The value at the address field in the instruction plus the X register points to the memory location where the effective address of the operand is present.
* **Indirect, Y-indexed**. The operand is the same as in an indirect access, except the obtained value is added with the Y register.
* **Relative**. The operand is the PC + a signed offset (used for branching).
* **Zeropage**. The operand is a zeropage address (single byte).
* **Zeropage X-indexed**. The operand is a zeropage address incremented by X.
* **Zeropage Y-indexed**. The operand is a zeropage address incremented by Y.
