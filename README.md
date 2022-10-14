# Ax100---Architecture
Overcomplicated, extendable ISA implemented in the game "Turing Complete".

()[base ISA]

## Goals 
- 64 bit
- complex instructions for doing much things in only one clock cycle
- Easy to create a CPU with using the base core
- Extandability of the base ISA wich can be implemented in the CPU
- Reduced I/O usage
- Easy to create a system wich contains 1 - 8 CPUs wich should run 80% in parralel
- Implementation in TC
- Emulator written in Python
- Custom Asembler
- CPUs can have things like cache, fpus and other extensions

## Turing Complete Hardware
- [InPlanning] Xtc100c10 Core rev 1
- [InPlanning] Xtc101f11 FPU 1 Rev 1
- [InPlanning] Xtc102mc11 Memory Controler (CPU) and Cache rev1
- [InPlanning] Xtc103io11 I/O controler 1 rev 1
- [InPlanning] Xtc104m11 Memory controler 1 rev 1
- [InPlanning] Xtcc00 simple CPU

## Extensions
- Ax101 Cache system
- Ax102 Multi stream RAM
- Ax103 Register Blocks
- Ax104 Datatypes 1
- Ax105 FPU operations 1
- Ax106 Multi stream IO 
