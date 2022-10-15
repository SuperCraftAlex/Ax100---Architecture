# Ax100 Base ISA

### op:

0 arg -> INSTR

1 arg -> INSTR ARG

2 arg -> INSTR ARG ARG

3 arg -> INSTR ARG ARG ARG

### Instruction Layout (INSTR):

INSTR = 64 bit:
| pa[^1] | Instruction | instruction length |
| - | - | - |
| 0001 - FFFF | 00 - FF | 0-F |

= 0xCCCCBBA

A = arg length

BB = instruction

CCCC = pa[^1]

## Instructions

### Basic instructions
| hex | opcode | name | args | pa[^1] | desc | arg desc |
| --- | ------ | -----| ---- | --- | ---- | -------- |
| 0x00 | nop | no operation |  |  | does nothing |  |
| 0x01 | mov | move | a o |  | move | a = from; b = to |
| 0x02 | not | bitwise not | a o |  |  | a = from; o = to |
| 0x02 | and | bitwise and | a b o |  |  | a, b = from; o = to |
| 0x03 | or | bitwise or | a b o |  |  | a, b = from; o = to |
| 0x04 | nor | bitwise nor | a b o |  |  | a, b = from; o = to |
| 0x05 | nand | bitwiae nand | a b o |  |  | a, b = from; o = to |
| 0x06 | xor | bitwise xor | a b o |  |  | a, b = from; o = to |
| 0x07 | xnor | bitwise xnor | a b o |  |  | a, b = from; o = to |
| 0x08 | neg | negate | a o |  |  | a = from; o = to |
| 0x09 | add | add | a b o |  |  | a, b = from; o = to |
| 0x0A | sub | subtract | a b o |  |  | a, b = from; o = to |
| 0x0B | mul | multiply | a b o |  |  | a, b = from; o = to |
| 0x0C | shl | shift left | a b o |  |  | a, b = from; o = to |
| 0x0D | shr | shift right | a b o |  |  | a, b = from; o = to |
| 0x0E | - | reserved | | | | |
| 0x0F | asr | arithmetic shift right | a b o |  |  | a, b = from; o = to |
| 0x10 | rg1 | Ram get bank 1 | a o |  | outputs the value of a 64 bit value in ram bank 1 to o | a = addres; o = to |
| 0x11 | rs1 | Ram set bank 1 | a b |  | sets the value of a element in ram bank 1 to b | a = addres; b = value |
| 0x12 | rg2 | Ram get bank 2 | a o |  | outputs the value of a 64 bit value in ram bank 1 to o | a = addres; o = to |
| 0x13 | rs2 | Ram set bank 2 | a b |  | sets the value of a element in ram bank 2 to b | a = addres; b = value |
| 0x14 | jmp | jump | a | COND | jumps to a programm addres | a = programm addres to jump to |
| 0x15 | jsr | jump to subroutine | a | COND; ARGPS | jumps to a programm addres with pushing the last position to stack | a = programm addres to jump to |
| 0x16 | jck | jump kernal | a | COND; ARGPS |  | a = programm addres to jump to |
| 0x17 | ret | return | | ARGPS; COND | returns from subroutine | |
| 0x18 | hlt | halt (core) | | | halts the core | |
| 0x19 | hlp | halt (cpu) | | | halts the whole cpu | |
| 0x1A | xchg[^2] | exchange | a b | | exchanges two positions | a, b = things to exchange |

### Advanced & Compatibility & Multi core instructions
| hex | opcode | name | args | pa* | desc | arg desc |
| --- | ------ | -----| ---- | --- | ---- | -------- |
| 0x40 | cmsg | core message send | a b | | sends a message to a core of the same cpu | a = core id of the reciever core; b = message |
| 0x41 | pmsg | cpu message send | a b | | sends a message to a other cpu | a = id of the reciever cpu; b = message |
| 0x42 | wafc | wait (core) | a | COND | waits untill a specific condition is met (halts the core until met) continues when the condition of the COND pa is met | a = register / argument... |
| 0x43 | wafp | wait (cpu) | a | COND | waits untill a specific condition is met (halts the cpu until met) continues when the condition of the COND pa is met | a = register / argument... |
| 0x44 | seti | set interrupt | a | | starts listening on the interrupt condition (needed to use if you want to check if the interrupt condition is met without using setij) | a = interrupt condition |
| 0x45 | setij | set interrupt with jump | a b | | starts listening on the interrupt condition and jumps if the condition is met | a = interrupt condition; b = addres to jump to |
| 0x46 | unsi | unset interrupt | a | | stops listening on the interrupt condition | a = interrupt condition |
| 0x47 | cli | clear interupt | a || clears the "triggered" flag of the specifies interrupt | a = interrupt|
| 0x48 | cep | change core instruction load position | a b | | jumps to an specified addres from a different programm source | a = programm source; b = addres |
| 0x49 | are | export arguments | a b c || exports the content of thw argument registers | a, b, c = destination |

[^1]: possible arg sets
[^2]: can't be implemented in a single tick

## instruction addition sets

instruction extensions get added to the instruction

args of the pa will be added after the args of the normal instruvtions

### COND
Normally: Executes instruction only if condition is met
condotions:
| hex | opcode | desc | args | argdesc |
| - | - | - | - | - |
| 0x0001 | eq | equals || a b ||
| 0x0002 | neq | not equal || a b ||
| 0x0003 | ls | less || a b ||
| 0x0004 | lseq | less or equal || a b ||
| 0x0005 | gr | greater || a b ||
| 0x0006 | greq | greater or equal || a b ||
| 0x0007 | zr | zero | if arg is zero | a | a = to check|
| 0x0008 | cr | carry | checks for the carry flag |||
| 0x0009 | nz | not zero | if arg is not zero | a | a = to check|
| 0x000A | nc | no carry | checks for the carry flag|||
| 0x000B | itr | interrupt | checks for a specific interrupt to be triggered | a | a = interrupt |

### ARGPS
passes args to the target

| hex | opcode | desc | args | argdesc |
| - | - | - | - | - |
| 0x0010 | ap1 | pass 1 arg | a | a = arg to pass|
| 0x0020 | ap2 | pass 2 arg | a b | a, b = args to pass|
| 0x0030 | ap3 | pass 3 arg | a b c | a, b, c = args to pass|

## commom instruction arguments

### register
| hex | name | desc |
| - | - | - |
| 0x000 | pc | General Programm counter |
| 0x010 | res | ALU result register A |
| 0x020 | reb | ALU result register B |
| 0x030 | fla | ALU flag register A |
| 0x040 | -| Reserved |
| 0x050 to 0x070 | ar1 to ar3 | argument registers |
| 0x080 to 0x0F0 | - | reserved |
| 0x100 to 0x2F0 | r0 to r31 | General purpose register |
| 0x300 to 0xFF0 | (r32 to ?) | optional general purpose register |

### ram as arguments
| hex | name | desc|
| - | - | - |
| 0x1000 | ra1 | Ram accses for bank 1 |
| 0x1010 | ra2 | Ram accses for bank 2 |

### I/O devices as arguments

## Interrupts

### possible interrupt conditions
| hex | name | desc | arguments it sets |
| - | - | - | - |
