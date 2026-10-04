---
tags:
  - compute-models
  - system-architectures
  - streaming
  - dataflow
---

# General Compute Model

## Example: Communicating Sequential Processes (CSP)

![[csp.png]]
- Sequential Processes (Clouds in the diagram): 
	- Like standard pieces of serial software
- Events/Channels (Arrows in the diagram):
	- No shared memory
	- Only interaction is communication and synchronization through the sending and receiving of discrete events or channel messages

- Very powerful
	- Unifies computation and concurrency: It can scale down to a single process or scale up to hundreds or thousands of concurrent processes
	- The behaviour of Verilog and VHDL is essentially a variant of CSP
		- Each `always` block acts as a sequential process
		- Sensitivity lists and signal transmissions function as events
- Problems:
	- Little guidance in reasoning about or implementing design: 
		- The model is too flexible to specify constraints such as data arrival rates, buffer size requirements, or deadlock avoidance mechanisms.
	- Optimization is impossible: 
		- Compilers and CAD tools struggle to perform aggressive static scheduling or optimizations for area and clock speed.
		- Lead to bloated, highly inefficient hardware; Impossible to render formal verification within polynomial time
- **Use most restrictive compute/system model as you can**

---

# Dataflow Models - Streaming

[[Dataflow Models|Check Explanations]]

---

# Control-Driven Models

[[Control-Driven Models|Check Explanations]]
