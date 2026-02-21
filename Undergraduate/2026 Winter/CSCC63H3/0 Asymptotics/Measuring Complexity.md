# Big-O And Small-O Notations (Asymptotic Analysis)
## Big-O notation
### Definition
Let $f$ and $g$ be functions $f,g: N \to R^+$.
$f(n) = O(g(n))$ iff $\exists c \in R^+ \text{ and } n_0 \in N \text{ such that } \forall n \ge n_0 \ f(n) \le c \cdot g(n)$ 
If $f(n) = O(g(n))$, then we say that $g(n)$ is an **upper bound** for $f(n)$, or more precisely, that $g(n)$ is an **asymptotic upper bound** for $f(n)$.
### Polynomial bounds
#### Definition
Polynomial bounds are the bounds of the form $n^{c} \text{ for } c > 0$.
### Exponential bounds
#### Definition
Exponential bounds are the bounds of the form $2^{n^\delta} \text{ for } \delta \in R^+$.
## Small-O notation
### Definition
Let $f$ and $g$ be functions $f,g: N \to R^+$.
- $f(n) = o(g(n))$ iff $\forall c \in R^+ \ \exists n_0 \in N \text{ such that } \forall n \ge n_0 \ f(n) < c \cdot g(n)$ .
- $f(n) = o(g(n))$ iff $\lim_{ n \to \infty } \frac{f(n)}{g(n)} = 0$
