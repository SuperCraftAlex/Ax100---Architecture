# Ax100 Base ISA

## Instructions

### Basic instructions
| hex | opcode | name | args | pa[^1] | desc | arg desc |
| --- | ------ | -----| ---- | --- | ---- | -------- |
| 0x000 | nop | no operation |  |  | does nothing |  |
| 0x010 | mov | move | a o |  | move | a = from; b = to |
| 0x020 | not | bitwise not | a o |  |  | a = from; o = to |
| 0x020 | and | bitwise and | a b o |  |  | a, b = from; o = to |
| 0x030 | or | bitwise or | a b o |  |  | a, b = from; o = to |
| 0x040 | nor | bitwise nor | a b o |  |  | a, b = from; o = to |
| 0x050 | nand | bitwiae nand | a b o |  |  | a, b = from; o = to |
| 0x060 | xor | bitwise xor | a b o |  |  | a, b = from; o = to |
| 0x070 | xnor | bitwise xnor | a b o |  |  | a, b = from; o = to |
| 0x080 | neg | negate | a o |  |  | a = from; o = to |
| 0x090 | add | add | a b o |  |  | a, b = from; o = to |
| 0x0A0 | sub | subtract | a b o |  |  | a, b = from; o = to |
| 0x0B0 | mul | multiply | a b o |  |  | a, b = from; o = to |
| 0x0C0 | shl | shift left | a b o |  |  | a, b = from; o = to |
| 0x0D0 | shr | shift right | a b o |  |  | a, b = from; o = to |
| 0x0E0 | asl | arithmetic shift left | a b o |  |  | a, b = from; o = to |
| 0x0F0 | asr | arithmetic shift right | a b o |  |  | a, b = from; o = to |
| 0x100 | rg1 | Ram get bank 1 | a o |  | outputs the value of a 64 bit value in ram bank 1 to o | a = addres; o = to |
| 0x110 | rs1 | Ram set bank 1 | a b |  | sets the value of a element in ram bank 1 to b | a = addres; b = value |
| 0x120 | rg2 | Ram get bank 2 | a o |  | outputs the value of a 64 bit value in ram bank 1 to o | a = addres; o = to |
| 0x130 | rs2 | Ram set bank 2 | a b |  | sets the value of a element in ram bank 2 to b | a = addres; b = value |
| 0x140 | jmp | jump | a | COND | jumps to a programm addres | a = programm addres to jump to |
| 0x150 | jsr | jump to subroutine | a | COND; ARGPS | jumps to a programm addres with pushing the last position to stack | a = programm addres to jump to |
| 0x160 | jck | jump kernal | a | COND; ARGPS |  | a = programm addres to jump to |
| 0x170 | ret | return | | ARGPS | returns from subroutine | |
| 0x180 | hlt | halt (core) | | | halts the core | |
| 0x190 | hlp | halt (cpu) | | | halts the whole cpu | |
| 0x1A0 | xchg[^2] | exchange | a b | | exchanges two positions | a, b = things to exchange 
|

### Advanced & Compatibility & Multi core instructions
| hex | opcode | name | args | pa* | desc | arg desc |
| --- | ------ | -----| ---- | --- | ---- | -------- |
| 0x400 | cmsg | core message send | a b | | sends a message to a core of the same cpu | a = core id of the reciever core; b = message |
| 0x410 | pmsg | cpu message send | a b | | sends a message to a other cpu | a = id of the reciever cpu; b = message |
| 0x420 | wafc | wait (core) | a | COND | waits untill a specific condition is met (halts the core until met) continues when the condition of the COND pa is met | a = register / argument... |
| 0x430 | wafp | wait (cpu) | a | COND | waits untill a specific condition is met (halts the cpu until met) continues when the condition of the COND pa is met | a = register / argument... |
| 0x440 | seti | set interrupt | a | | starts listening on the interrupt condition (needed to use if you want to check if the interrupt condition is met without using setij) | a = interrupt condition |
| 0x450 | setij | set interrupt with jump | a b | | starts listening on the interrupt condition and jumps if the condition is met | a = interrupt condition; b = addres to jump to |
| 0x460 | unsi | unset interrupt | a | | stops listening on the interrupt condition | a = interrupt condition |
| 0x470 | cep | change core instruction load position | a b | | jumps to an specified addres from a different programm source | a = programm source; b = addres |

[^1]: possible arg sets
[^2]: cant be implemented in a single tick

## commom instruction arguments

### register
| hex | name | desc |
| - | - | - |
| 0x000 | pc | General Programm counter |
| 0x010 | res | ALU result register A |
| 0x020 | reb | ALU result register B |
| 0x030 | fla | ALU flag register A |
| 0x040 | -| Reserved |
| 0x050 to 0x0F0 | - | reserved |
| 0x100 to 0x2F0 | r0 - r31 | General purpose register |
| 0x300 to 0xFF0 | (r32 - ?) | optional general purpose register |

### ram as arguments
| hex | name | desc|
| - | - | - |
| 0x1000 | ra1 | Ram accses for bank 1 |
| 0x1010 | ra2 | Ram accses for bank 2 |

### I/O devices as arguments
