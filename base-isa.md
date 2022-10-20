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
Every instruction can be used with the IMM pa[^1]
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
| 0x10 | - | reserved | | | | |
| 0x11 | - | reserved | | | | |
| 0x12 | - | reserved | | | | |
| 0x13 | - | reserved | | | | |
| 0x14 | jmp | jump | a | COND | jumps to a programm addres | a = programm addres to jump to |
| 0x15 | jsr | jump to subroutine | a | COND; ARGPS | jumps to a programm addres with pushing the last position to stack | a = programm addres to jump to |
| 0x16 | jck | jump kernal | a | COND; ARGPS |  | a = programm addres to jump to |
| 0x17 | ret | return | | ARGPS; COND | returns from subroutine | |
| 0x18 | hlt | halt (core) | | | halts the core | |
| 0x19 | hlp | halt (cpu) | | | halts the whole cpu | |
| 0x1A | xchg | exchange | a b | | exchanges two positions | a, b = things to exchange |
| 0x1B | push | push to stack | a ||| a = value |
| 0x1C | pop | pop from stack | o ||| o = output addres |

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
| 0x49 | are | export arguments | a b c || exports the content of the argument registers | a, b, c = destination |
| 0x4A | ios | I/O send | a b c || sends data to an io device | a, b = source; c = destination |

[^1]: possible arg sets

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

### IMM
imediates a number
| hex | opcode | desc | args | argdesc |
| - | - | - | - | - |
| ? | i1 | immediates the first arg of the instruction | | |
| ? | i2 | immediates the second arg of the instruction | | |
| ? | i3 | immediates the third arg of the instruction | | |

## commom instruction arguments

### register
| c / p | hex | name | desc |
|-| - | - | - |
| c | 0x000 | pc | General Programm counter |
| c | 0x010 | rea | ALU result register A |
| c | 0x020 | reb | ALU result register B |
| c | 0x030 | fla | ALU flag register A |
| c | 0x040 | sp | stack pointer |
| c | 0x050 to 0x070 | ar1 to ar3 | argument registers |
| - | 0x080 to 0x0F0 | - | reserved |
| c | 0x100 to 0x2F0 | r0 to r31 | general purpose register |
| p | 0x300 to 0xFF0 | (r32 to ?) | optional general purpose register (processor located) |

p: processor located
c: core located

### ram as arguments
| hex | name | desc|
| - | - | - |
| ? | ra1 | Ram accses for bank 1 |
| ? | ra2 | Ram accses for bank 2 |
If you want to write/read to/from a specific ram address use the hex code of the ram bank combined with the addres

### I/O devices as arguments
IO devices can be used as argument for instruction.

See section "I/O devices" for more information

## Interrupts

### possible interrupt conditions
| hex | name | desc | arguments it sets |
| - | - | - | - |

## I/O Devices
IO has nothing to do with ram! In this section only IO is described
the hex value of the list of io ports can also be used as artument.
| hex | port | desc |
| - | - | - |
| 0x2000 | reserved ||
| 0x2010 | gpio 1 ||
| 0x2020 | gpio 2 ||
| 0x2030 to 0x20F0 | * gpio 3 to 16 | optional gpio |

### I/O bus layout
Per i/o device:
2x 64 bit line (cpu -> device)
1x 64 bit line (device -> cpu)
1x 1 bit line (cpu sending status)
1x 1 bit line (decice sending status)
1x 1 bit line (device sending not enabled)

## RAM
Every cpu gets its own bus connected to a ram controller connected to the ram storage.
Every ram bank has its own controller. All cpus are connected to the ram controller via an own bus

### ram bus layout

### Stack
The stack is in the same ram bank as the ram bank, code gets ececutes from.
If code gets ececuted from a different place than ram, stack will be automatically in ram bank 1

It gets controlled internally by the SP register but you should acces it with push and pop.
