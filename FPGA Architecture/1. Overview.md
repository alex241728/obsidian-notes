---
tags:
  - fpga
  - overview
  - asic
---

# Why FPGAs? Why Not Processors for Everything?

> [!info] Microprocessor
> 
> **Definition**
> A programmable computing unit based on an **ISA (Instruction Set Architecture)**.
> 
> ---
> 
> **Operating Mechanism**
>1. **Minimal Shared Hardware**:
>	* Contains a few fixed, universal Arithmetic Logic Units (ALUs) and a centralized Register File.
>2. **Instructions as Hardware Control Switches**:
>	* Assembly code (e.g., `add $t2, $t1, $t0`) translates into a binary instruction word (32-bit or 64-bit)].
>	* The control unit decodes these bits into hardware control signals that configure multiplexers (MUXes), set ALU opcodes, and trigger register write-enables.
> 3. **PC-Driven Sequential Execution**:
>	* The Program Counter (PC) holds the memory address of the current instruction.
>	* Cycle by cycle, it fetches, decodes, and executes instructions sequentially, updating the processor's state step by step.

## I/O
A processor's physical interfaces are permanently fixed at chip fabrication.
FPGAs have highly configurable I/O, allowing for flexible adaptation to various voltage levels, timing requirements, protocols, and even high-speed serial standards

--- 

## Performance
### Processors
- Temporal Calculation $\to$ Sequential
- Data Storage $\to$ Global/Centralized State: All data are stored in the register file
	- Bottleneck: In every calculation, data are needed to be read from the registers and sent to the ALU; After calculation, data are needed to be written from the ALU to the registers. (Delays)
 - Processors can extract limited "instruction" parallelism but needs lots of Hardware
![[microprocessor_performance_example.png]]

### FPGAs: 
- Intrinsically parallel
- Spatial computation $\to$ No central state
- Can replace some parts to specialized operators $\to$ Smaller and Faster e.g. change ALU to +

> [!note]
> - May not be much faster for 1 computation as critical path still goes through all operators -> adds delay/time
> - Some speed gain by removing register accesses

![[fpga_performance _example.png]]

---

# FPGA vs. ASIC (custom chip)

If we want hardware, build custom or use FPGA?
- FPGA: Buy it, program it, test it, and sell it
- ASIC: Design, test, manufacture, test more, sell
- ASIC cheaper in high volume (smaller, faster), but needs custom manufacturing (more money, late to market)

**Time to market**
![[fpga_vs_asic.png]]
