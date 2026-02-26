# Refresher
1. What does it mean for L to be in NP? Verifiable in polytime
2. Any $L_{0}$ in $NP$ that can be reduced to $L$.
	- If we have a machine that can solve $L$, then we can make a machine that solves $L_{0}$.
	- (For this context, machine for $L$ and $L_{0}$ should run in polytime.)
3. $L$ is in NP and $L$ is NP-hard.
# Question 2
1. It means $P=NP$. (Every $L_0$ in NP reduces to $L$, so we can solve $L_{0}$ in polytime using the polytime machine for $L$.)
2. It means $L \not\in P$. (If it were, then we would need $P=NP$.) This is a contrapositive.
# Question3
# Question 4
# Definition 5
- What is $1^t$?
	- $1^t$ is the string $1$ repeated $t$ times. Example: $1^5 = 11111$.
- What is the meaning of this language?
	- If I tell you that $(\langle M \rangle, x, 1^t)$ is in $L_{t}$, then there is some witness $w$ of length up to $t$ for which we accept $x$ in $t$ steps.
# Theorem 6
1. **Show $L$ is in $NP$**
Our goal is to construct a polytime verifier $V$ for $L$.
- Given $(\langle M \rangle, x, 1^t)$ and a witness $w$ of length at most $t$,
	- Run $M(x,w)$ for $t$ steps, and accept iff $M(x,w)=1$.
- If it didn't finish in $t$ steps, or if we got invalid inputs, we should reject.

Need to show it runs in polytime and it is a verifier for $L$.
"Runs in polytime" means that when $V$ gets an input of length $n$, its runtime is $n^c$ for some $c > 0$.
Proof of runtime: the input is length at least $t$, and our runtime is $ploy(t)$ to simulate $M$. So, our runtime is polynomial in the input length.
Prove $V$ is a verifier for $L$:
Need to show:
- If $x \in L$, then there is a $w$ such that $V(x,w)=1$.
- If $x \not\in L$, then for all $w$, $V(x,w)=0$.
This is by definition.
2. **Show $L$ is NP-hard**
Consider an arbitrary $L_{0}$ in $NP$. We need to show $L_{0}$ reduces to $L$.
(Normally we would need to construct a machine, but Roei wants to be fancy):
- It is enough if we can, given any $x$, efficiently construct a string $y$ such that $x \in L_{0} \Leftrightarrow y \in L$.

Since $L \in NP$, we have a verifier $V$ for $L_0$ that runs in polytime ($n^c$)
Recall: The "real" way to do it would be : Assume we have a polytime decider for $L$. Use that to construct a polytime decider for $L_{0}$.

