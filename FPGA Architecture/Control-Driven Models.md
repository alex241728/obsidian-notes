# Finite-State Machine with Datapath (FSMD)

![[fsmd.png]]

- Like a custom, hard-wired microprocessor
- Suitable for rare/not highly parallel operators

---
# Very Long Instruction Word (VLIW)

![[vliw.png]]

- Uses **one extra-wide instruction** (Extra-wide, e.g. 128 to 256 bits) packed with multiple _different_ operations to drive multiple _different_ execution units simultaneously.
- Instruction-Level Parallelism (ILP)
- Software burden is extremely high: The compiler must schedule operations and insert no operations (NOPs) when dependencies exist.
- Slots are wasted on NOPs if compiler can't find enough independent instructions.

---

# Single Instruction, Multiple Data (SIMD)

![[simd.png]]

- Many parallel execution units, all the same
- Share control (instructions or FSM)

- Uses **one standard instruction** broadcast to multiple _identical_ execution units to perform the exact _same_ operation across a batch of data.
- Data-Level Parallelism (DLP)
- Software burden is low: The compiler only needs to emit a single vector instruction.
- Conditional statements (if-else) force hardware masking, causing execution stalls.

---

