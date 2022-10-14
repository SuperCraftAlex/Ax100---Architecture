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
| 0x130 | rs2 | Ram set bank 2 |  |  |  |  |
| 0x140 | jmp | jump |  |  |  |  |
| 0x150 | jsr | jump to subroutine |  |  |  |  |
| 0x160 | jck | jump kernal |  |  |  |  |

## commom instruction arguments

### register
| hex | name | desc |
| - | - | - |
| 0x000 | pc | General Programm counter |
| 0x010 | res | ALU result register A |
| 0x020 | reb | ALU result register B |
| 0x030 | fla | ALU flag register A |
| 0x040 | flb | ALU flag register B |
| 0x050 | - | Reserved |
| 0x060 | - | Reserved |
| 0x070 | - | Reserved |
| 0x080 | - | Reserved |
| 0x090 | - | Reserved |
| 0x0A0 | - | Reserved |
| 0x0B0 | - | Reserved |
| 0x0C0 | - | Reserved |
| 0x0D0 | - | Reserved |
| 0x0E0 | - | Reserved |
| 0x0F0 | - | Reserved |
