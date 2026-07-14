# Shift Operations
- Left Shift: $x \ll y$
	- Shift bit-vector x left y positions
		- Throw away extra bits on left
	- Fill with 0's on right
- Right Shift: $x \gg y$
	- Shift bit-vector x right y positions
		- Throw away extra bits on right
	- Logical shift
		- Fill with o's on left
	- Arithmetic shift
		- Replicate most significant bit on left
- Undefined Behaviour
	- **Shift amount < 0 or word size**
		- Modulo shifting: 为了提高硬件执行效率，移位指令并不会直接支持无限大小的移位。硬件在处理移位位数时，会自动对**数据类型的位数**取模（求余数）。
# Numeric Ranges
![[Pasted image 20260714144127.png]]
![[Pasted image 20260714144226.png]]
# Values for Different Word Sizes
![[Pasted image 20260714144704.png]]
# Unsigned & Signed Numeric Values
![[Pasted image 20260714144824.png]]
# Conversion Visualised
![[Pasted image 20260714145358.png]]
# Signed vs. Unsigned in C
![[Pasted image 20260714152946.png]]
# Casting Surprises
![[Pasted image 20260714153444.png]]
# Summary Casting Signed $\leftrightarrow$ Unsigned: Basic Rules
- Bit pattern is maintained
- But reinterpreted
- Can have unexpected effects: adding or subtracting $2^w$

- Expression containing signed and unsigned int
	- `int` is cast to `unsigned` !!
# Sign Extension
![[Pasted image 20260714155112.png]]
# Summary: Expanding, Truncating: Basic Rules

- Expanding (e.g., short int to int)
	- Unsigned: zeros added
	- Signed: sign extension
	- Both yield expected result

- Truncating (e.g., unsigned to unsigned short)
	- Unsigned/signed: bits are truncated
	- Result reinterpreted
	- Unsigned: mod operation
	- Signed: similar to mod
	- For small numbers yields expected behaviour
# Unsigned Addition
![[Pasted image 20260714160558.png]]
## Visualising (Mathematical Integer Addition)
![[Pasted image 20260714160834.png]]
## Visualising Unsigned Addition
![[Pasted image 20260714161032.png]]
# Two's Complement Addition
![[Pasted image 20260714161230.png]]
## TAdd Overflow
![[Pasted image 20260714162132.png]]
## Visualising 2's Complement Addition
![[Pasted image 20260714162232.png]]
# Unsigned Multiplication in C
![[Pasted image 20260714162351.png]]
# Signed Multiplication in C
![[Pasted image 20260714163658.png]]