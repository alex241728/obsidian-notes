# Element Constraints
#circuit #electrical-device 
A **circuit** is a collection of interconnected electrical devices.

An **electrical device** is a component that is treated as a separate entity. 

A two-terminal device is described by its **$i-v$ characteristic**, that is, by the relationship between the voltage across and current through the device.
## The Linear Resistor
#linear-resistor #ohms-Law #resistance #conductance #linear #nonlinear #bilateral #power 
The equations describing the **linear resistor** element are $v = Ri$ or $i = Gv$ (**Ohm's Law**) where $R$ and $G$ are positive constants that are reciprocally related: $G = \frac{1}{R}$. The parameter $R$ is called **resistance** and has the unit **ohms, $\Omega$**. The parameter $G$ is called **conductance**, with the unit **siemens, $S$**.I n earlier times, the unit of conductance was cleverly called the **mho**, with the unit abbreviation symbol $\mho$ (“ohm” spelled backward and the ohm symbol upside down).

The $i-v$ characteristic for the Ohm’s law model defines a circuit element that is said to be **linear and bilateral**. **Linear** means that the defining characteristic is a straight line through the origin. Elements whose characteristics do not pass through the origin or are not a straight line are said to be **nonlinear**. **Bilateral** means that the $i-v$ characteristic curve has odd symmetry about the origin. With a bilateral resistor, reversing the polarity of the applied voltage reverses the direction but not the magnitude of the current, and vice versa. The net result is that we can connect a bilateral resistor into a circuit without regard to which terminal is which.

The **power** associated with the resistor can be found from $p=vi$. 

Under Ohm's law model, $p = i^2R = \frac{i^2}{G}$ or $p = v^2G = \frac{v^2}{R}$. 

Since the parameter R is positive, these equations tell us that the power is always nonnegative. Under the **passive sign convention**, this means that the resistor always absorbs or consumes power.

Note: **passive sign convention** is a standard in electrical engineering where power is defined as positive when flowing _into_ a component (dissipated) and negative when flowing _out_ (generated).

## Open And Short Circuits
#open-circuit #short-circuit
If $v = 10V$ and $R = 1 \Omega$, using Ohm’s law we readily find that $i = 10A$. If we increase the resistance to $100 \Omega$, we find i has decreased to $0.1 A$ or 100 mA. If we continue to increase R to 1 MΩ, i becomes a very small 10 μA. Continuing this process, we arrive at a condition where R is very nearly infinite and i just about zero. When the current i = 0, we call the special value of resistance (i.e., R = ∞Ω) an open circuit. Similarly, if we reduce R until it approaches zero, we find that the voltage is very nearly zero. When υ = 0, we call the special value of resistance (i.e., R = 0 Ω) a short circuit.
## Fuses
#fuse 
Figure 2–4(a) shows the circuit symbol for a fuse, whereas Figure 2–4(b) shows a photo of a simple fuse as might be used in an electric circuit.
## The Ideal Switch
#ideal-switch
The ideal switch can be modeled as a combination open- and short-circuit element.

When the switch is open or OFF, $i = 0 \text{ and } v = \text{any value}$$.
When it is closed or ON, $v = 0 \text{ and } i = any$. 

When the switch is closed, the voltage across the element is zero and the element will pass any current that may result. When open, the current is zero and the element will withstand any voltage across its terminals. The power is always zero for the ideal switch, since the product $vi = 0$ when the switch is either open $i = 0$ or closed $v = 0$.
## Ideal Sources

