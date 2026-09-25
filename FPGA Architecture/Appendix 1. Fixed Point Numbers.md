---
tags:
  - fixed-point
  - floating-point
---
**16-bit signed integer**
- Range: -32768 to 32767
- Precision: 1
**Can be re-interpret as fixed point**
E.g. 2 integer bits, 14 fraction (Q2.14):
	- Range: ~-2 to +2
	- Precision: $2^{-14}$

Fixed points can add/subtract/multiply with **integer** hardware
- Efficient
- Keep track of where the implicit decimal point is when rounding, truncating or outputting data
	- Q2.14 + Q2.14 -> Q3.14 output
	- Q2.14 * Q2.14 -> Q4.28 output
	- Repeated adds and multiplies: may get more integer and fraction bits than you need

Fixed Point Numbers vs. Floating Point Numbers