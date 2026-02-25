# 1 NP
## 1.1 The basics
### Question 1
The difference between the class `R` and the class `P` is the time bound on deciding.

The difference between the class `RE` and the class `NP` is the time bound on verification.

There exists a language in `RE` but not in `R`.
There exists a language in `NP` but not in `P`.
### Question 2
Let a verifier $U$ with an input $(G,k)$ and a witness $S \subseteq V$ that
1. Checks if $S$ has a size of at least $k$. If not, returns 0.
2. Checks if the vertices in $S$ are pair-wised connected. If so, returns 1. Otherwise, returns 0.
$U$ verifies $CLIQUE$ in $O(|V|^2)$, which is a polytime. So, $CLIQUE \in NP$.

Let a verifier $V$ with an input $(x_{1}, x_{2}, \dots, x_{n}, t)$ and a witness $S \subseteq [n]$ that
1. $\forall S \in [n] \ \text{sum all the } x_{i}$.
2. Check if the sum is equal to $t$. If so, returns 1. Otherwise, returns 0.
$V$ verifies $SUBSET-SUM$ in $O(n \cdot C)$ where $C$ is the number of bits to represent $x_{1}, \dots, x_{n}$, which is a polytime. So, $SUBSET-SUM \in NP$

Let a verifier V with an input 
### Question 3
### Question 4
### Question 5
$NP \subseteq RE$ is true.
Proof:
Let $L$ be a language in $NP$, meaning that $L$ is verifiable in polytime. So, $L$ is in $RE$.

$NP \subseteq R$ is true.
Proof:
Let $L$ be a language in $NP$, meaning that $L$ is verifiable in polytime.
Let $M$ be a TM that
1. Runs the verifier of $L$ with all the possible witnesses iteratively.
2. If the verifier halts and accept, accepts. If we run out of witnesses, rejects.
$M$ decides $L$ in finite time. So, $NP \subseteq R$.
### Question 6
Prove: $NP \subseteq EXP$
Proof:
Let $L$ be a language in $NP$, meaning that $L$ is verifiable in polytime.
Note that the witness $w$ of the verifier has a length $\leq T(n) = poly(n)$. So, the number of numbers that can be represented by such a length is $2^{poly(n)}$.
Let $M$ be a TM that
1. Runs the verifier of $L$ with all the possible witnesses iteratively.
2. If the verifier halts and accept, accepts. If we run out of witnesses, rejects.
M decides L in $2^{poly(n)} \cdot O(poly(n)) \subseteq 2^{n^{O(1)}}$. So, $NP \subseteq EXP$.

I don't think $NP = EXP$. I think the time complexity gap between polynomial time and exponential time is too large.
### Question 7

Let $L'$ be a language in $PSPACE$, meaning that $L' \in SPACE[poly(n)]$.
$L' \in TIME[n \cdot 2^{O(poly(n))}] \subseteq TIME[2^{n^{O(1)}}]]$. So, $PSPACE \subseteq EXP$.
### Question 8
1. False.
2. True. $\forall L \in NP, L \in P \Rightarrow NP \subseteq P$. With $P \subseteq NP$, $P = NP$.
3. True. $\forall L \in NP, L \in P \Rightarrow NP \not\subseteq P \Rightarrow P \neq NP$
4. False.
## 1.2 Search vs decision
### Question 9
### Question 10
### Question 11