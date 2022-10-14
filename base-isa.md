# Ax100 Base ISA

## Instructions

### Basic instructions
| hex | opcode | name | args | pa* | desc | arg desc |
| --- | ------ | -----| ---- | --- | ---- | -------- |
| 0x000 | nop | nop |  |  |  |  |
| 0x010 | mov | move |  |  |  |  |
| 0x020 | not | bitwise not |  |  |  |  |
| 0x020 | and | bitwise and |  |  |  |  |
| 0x030 | or | bitwise or |  |  |  |  |
| 0x040 | nor | bitwise nor |  |  |  |  |
| 0x050 | nand | bitwiae nand |  |  |  |  |
| 0x060 | xor | bitwise xor |  |  |  |  |
| 0x070 | xnor | bitwise xnor |  |  |  |  |
| 0x080 | neg | negate |  |  |  |  |
| 0x090 | add | add |  |  |  |  |
| 0x0A0 | sub | subtract |  |  |  |  |
| 0x0B0 | mul | multiply |  |  |  |  |
| 0x0C0 | shl | shift left |  |  |  |  |
| 0x0D0 | shr | shift right |  |  |  |  |
| 0x0E0 | asl | arithmetic shift left |  |  |  |  |
| 0x0F0 | asr | arithmetic shift right |  |  |  |  |
| 0x100 | rg1 | Ram get bank 1 |  |  |  |  |
| 0x110 | rs1 | Ram set bank 1 |  |  |  |  |
| 0x120 | rg2 | Ram get bank 2 |  |  |  |  |
| 0x13 | rs2 | Ram set bank 2 |  |  |  |  |
| 0x14 | cnf | configurate |  |  |  |  |
| 0x15 | jmp | jump |  |  |  |  |
| 0x16 | jsr | jump to subroutine |  |  |  |  |
| 0x17 | jck | jump kernal |  |  |  |  |
