
# 📦 Inventory Management Lecture Notes (Comprehensive)

---

## 1. Inventory Dynamics

Inventory update rule:
$$
x_{k+1} = x_k + u_k - w_k
$$

---

## 2. Cost Function of State \( x \)

Total cost function:
$$
r(x) = p \cdot \max\{0, -x\} + h \cdot \max\{0, x\}
$$

- \( p \): backlog cost per unit
- \( h \): holding cost per unit

---

## 3. Objective

Minimize total expected cost:
$$
\mathbb{E} \left[\sum_{k=0}^{N} \left( c u_k + r(x_k) \right) \right]
$$

---

## 4. Bellman Recursion (Base Form)

Terminal condition:
$$
J_N(x_N) = 0
$$

Recursive step:
$$
J_k(x_k) = \min_{u_k \geq 0} \mathbb{E} \left[
c u_k + r(x_k + u_k - w_k) + J_{k+1}(x_k + u_k - w_k)
\right]
$$

---

## 5. Change of Variable: Post-Replenishment Inventory

Let:
$$
y_k = x_k + u_k \quad \Rightarrow \quad u_k = y_k - x_k
$$

Then:
$$
x_{k+1} = y_k - w_k
$$

---

## 6. Reformulated Cost Function

Define:
$$
H(y) = \mathbb{E}[r(y - w_k)] = p \cdot \mathbb{E}[(w_k - y)^+] + h \cdot \mathbb{E}[(y - w_k)^+]
$$

Define:
$$
G_k(y) = c y + H(y) + \mathbb{E}[J_{k+1}(y - w_k)]
$$

Then:
$$
J_k(x_k) = \min_{y_k \geq x_k} \left[ G_k(y_k) - c x_k \right]
$$

---

## 7. Final Period \( k = N - 1 \)

At \( J_N(x_N) = 0 \), then:
$$
G_{N-1}(y) = c y + H(y)
$$

Thus:
$$
J_{N-1}(x_{N-1}) = \min_{y \geq x_{N-1}} \left[ G_{N-1}(y) - c x_{N-1} \right]
$$

---

## 8. Derivative Insight

From:
$$
H(y) = G_k(y) - c y
\Rightarrow \frac{d}{dy} G_k(y) = c + \frac{d}{dy} H(y)
$$

At optimal \( y = S_k \):
$$
\frac{d}{dy} G_k(S_k) = 0 \Rightarrow \frac{d}{dy} H(S_k) = -c
$$

---

## 9. Assumptions

- \( J_{k+1}(x) \) is convex
- \( H(y) \) is convex
- \( G_k(y) \) is convex
- \( \lim_{|y|\to \infty} G_k(y) = \infty \)
- \( \lim_{|x|\to \infty} J_k(x) = \infty \)

---

## 10. Optimal Policy (Base-stock)

Base-stock level:
$$
S_k = \arg\min_y G_k(y)
$$

Then:
$$
u_k^*(x_k) = 
\begin{cases}
S_k - x_k, & x_k < S_k \\
0, & x_k \geq S_k
\end{cases}
$$

---

## 11. With Fixed Ordering Cost \( K > 0 \)

Ordering cost function:
$$
C(u) = 
\begin{cases}
K + c u, & u > 0 \\
0, & u = 0
\end{cases}
$$

Modified Bellman equation:
$$
J_k(x_k) = \min \left\{
G_k(x_k), \min_{y_k > x_k} \left[ K + G_k(y_k) \right]
\right\} - c x_k
$$

---

## 12. Policy Becomes (s, S) Type

There exists reorder point \( s_k \) and order-up-to level \( S_k \) such that:
$$
u_k^*(x_k) =
\begin{cases}
S_k - x_k, & x_k \leq s_k \\
0, & x_k > s_k
\end{cases}
$$

---

## 13. Non-Convexity Note

When \( K > 0 \), the value function:
$$
J_k(x_k) = \min\{G_k(x_k), K + G_k(y_k)\} - c x_k
$$

may not be convex.

---

## 14. Optimal Ordering Policy with Fixed Cost \( K > 0 \)

Consider the function \( G_k(y) \) when fixed ordering cost \( K > 0 \). The value function may be non-convex, and the ordering decision depends on the comparison between:
- \( G_k(x_k) \): cost of not ordering
- \( K + G_k(y_k) \): cost of placing an order up to \( y_k \)

We divide the state space into four regions based on this comparison:

### Zone I: Ordering is strictly better
If \( x_k \in \text{Zone I} \), then:
$$
G_k(x_k) > G_k(s), \quad \forall x_k < s
$$
So the optimal order-up-to level is \( y_k = S \), and:
$$
u_k^* = S - x_k
$$
Clearly, \( G_k(S) + K < G_k(x_k) \), so ordering is optimal.

---

### Zone II: Not ordering is better
If \( x_k \in \text{Zone II} \), we distinguish two sub-cases:

- If \( s < x_k < S \), and \( u > 0 \Rightarrow y_k > x_k \), then:
  $$
  K + G_k(y_k) > G_k(x_k)
  $$

- If \( S < x_k < y' \), and \( u > 0 \Rightarrow y_k > x_k \), then:
  $$
  K + G_k(y_k) > G_k(x_k)
  $$

In both cases, ordering is suboptimal, so:
$$
u_k^* = 0
$$

---
### Zone III: Order up to a higher level $\tilde{S}$
If \( x_k \in \text{Zone III} \), then:
$$
G_k(x_k) > K + G_k(\tilde{S}) \quad \text{for some } \tilde{S} > x_k
$$
Thus, ordering up to \( \tilde{S} \) is optimal:
$$
u_k^* = \tilde{S} - x_k
$$

---

### Zone IV: No order region
If \( x_k \in \text{Zone IV} \), then for all \( y_k > x_k \),
$$
K + G_k(y_k) > G_k(x_k)
$$
Thus, not ordering is optimal:
$$
u_k^* = 0
$$

---

### Summary of the (s, S) Policy

The optimal policy can be summarized as:
- Order up to \( S \) if \( x_k \leq s \)
- Otherwise, do not order

Formally:
$$
u_k^*(x_k) =
\begin{cases}
S - x_k, & x_k \leq s \\
0, & x_k > s
\end{cases}
$$

This structure generalizes the base-stock policy when a fixed cost \( K \) is present. Even though \( G_k \) may not be convex, it exhibits a form of piecewise convexity known as **\( K \)-convexity**, which still guarantees threshold-type policies.

## 15. Value Function Structure and K-Convexity

We now analyze the structure of the cost function \( G_k(y) \) when fixed ordering cost \( K > 0 \) is present.

The figure shows that \( G_k(y) \) is not necessarily convex. Instead, it has a "valley" followed by a "hill", giving rise to multiple decision zones. This leads to the well-known \((s, S)\) structure.

### Bellman Equation with Fixed Cost

Recall the cost-to-go function becomes:
$$
J_k(x_k) = \min \left\{
G_k(x_k), \min_{y_k > x_k} \left[ K + G_k(y_k) \right]
\right\} - c x_k
$$

Where:
- \( G_k(x_k) \): cost of **not ordering**
- \( K + G_k(y_k) \): cost of **ordering up to \( y_k \)**

The comparison determines whether it is optimal to place an order.

### When \( K > 0 \): Value Function May Not Be Convex

We highlight:
- \( G_k(y) \) may have a local minimum at \( s \), but increasing afterward.
- Due to fixed cost \( K \), \( K + G_k(y) \) creates a discontinuity in marginal cost of ordering.
- This creates four **distinct zones** (as marked I, II, III, IV on the figure).

This leads to the observed ordering behavior:
- **Zone I**: Always order up to \( S \)
- **Zone II and IV**: Do not order
- **Zone III**: Order up to a new higher point \( \tilde{S} \)

Thus, while \( J_k(x_k) \) is not convex in general, the policy derived from it has a **threshold structure**, and the function \( G_k \) satisfies a weaker property called **\( K \)-convexity**.

This justifies the optimality of \((s, S)\)-type policies in such inventory control settings.

## 16. \( K \)-Convexity and its Role in Inventory Control

To understand the structure of the optimal ordering policy under positive fixed ordering cost \( K > 0 \), we introduce the concept of **\( K \)-convex functions**.

---

### Definition: \( K \)-Convex Function

A function \( g(y) \) is said to be \( K \)-convex if for all \( z \geq 0 \), \( b > 0 \), and \( y \in \mathbb{R} \), it satisfies:

$$
K + \frac{g(z + y) - g(z)}{y} \geq \frac{g(y) - g(y - b)}{b}
$$

Or equivalently:

$$
g(y) \leq g(z) + K, \quad \text{for } y \geq z
$$

This condition weakens standard convexity and still supports threshold-based decisions, even when the function is **not smooth or continuous**.

---

### Lemma 3.1.1: Properties of $K$-convex functions:

**(a)** A real-valued convex function $g$ is $0$-convex and hence also $K$-convex for all $K > 0$.

**(b)** If $g_1(y)$ and $g_2(y)$ are $K$-convex and $L$-convex respectively, then $\alpha g_1(y) + \beta g_2(y)$ is $(\alpha K + \beta L)$-convex, for all $\alpha, \beta > 0$.

**(c)** If $g(y)$ is $K$-convex and $w$ is a random variable, then $\mathbb{E}_w[g(y - w)]$ is also $K$-convex, provided $\mathbb{E}_w[|g(y - w)|] < \infty$, for all $y$.

**(d)** If $g$ is a continuous $K$-convex function and $g(y) \to \infty$ as $|y| \to \infty$, then there exist scalars $s$ and $S$, with $s \leq S$, such that
   
   **(i)** $g(S) \leq g(y), \forall y$ (i.e., $S$ is a global minimum).

   **(ii)** $g(S) + K = g(s) < g(y), \forall y < s$.
   
   **(iii)** $g(y)$ is decreasing on $(-\infty, s)$.
   
   **(iv)** $g(y) \leq g(z) + K, \forall y, z$, with $s \leq y \leq z$.

Using part (d) of Lemma 3.1.1, we will show that the optimal policy is of the form...
---

### Geometric Interpretation

From the figures and board derivations:

- \( f_1 \): satisfies \( K \)-convexity (slopes bounded by \( K \))
- \( f_2, f_3 \): violate the condition due to jumps or wrong slopes

Therefore:
- \( K \)-convex functions may not be differentiable or continuous
- They cannot exhibit a **positive jump**, nor can they have **a local minimum lower than the \( K \)-adjusted envelope**

---

### Optimal Policy Characterization

Using property (d) of Lemma 3.1.1, the optimal policy is shown to be of the form:

$$
\mu_k^*(x_k) =
\begin{cases}
S_k - x_k, & \text{if } x_k < s_k \\
0, & \text{if } x_k \geq s_k
\end{cases}
$$

Where:

- \( S_k \): minimizes \( G_k(y) \)
- \( s_k \): smallest \( y \) such that \( G_k(y) = K + G_k(S_k) \)

This is known as the **\((s, S)\) multiperiod policy**, and it arises naturally from the **\( K \)-convexity of the cost function \( G_k(y) \)**.

---

### Summary

- The optimal inventory control policy under fixed cost follows a threshold structure because the cost function is \( K \)-convex.
- The \((s, S)\) policy is not arbitrary, but a mathematically justified response to this structure.
- \( K \)-convexity provides enough structure to guarantee global minima and supports backward induction in dynamic programming.


## 17. Optimal Stopping and Scheduling Problems

## 3.3 Optimal Stopping and Scheduling Problems

In this section, we focus on two other types of problems with perfect state information: optimal stopping problems (mainly) and discuss few ideas on scheduling problems.

---

### 3.3.1 Optimal Stopping Problems

We assume the following:
- At each state, there is a control available that stops the system.
- At each stage, you observe the current state and decide either to **stop** or **continue**.
- Each policy consists of a partition of the set of states $x_k$ into two regions: the **stop region** and the **continue region**.
- Domain of states remains the same throughout the process.

---

#### Application: Asset Selling Problem
- Consider a person owning an asset for which she is offered an amount of money from period to period, across $N$ periods.
- Offers are random and independent, denoted $w_0, w_1, \ldots, w_{N-1}$, with $w_i \in [0, \bar{w}]$.

Figure 3.3.1:  
Each policy consists of a partition of the state space into the stop and the continue regions.

---

Let's solve this problem:
- **Control**:  
  $$
  \mu_k(x_k) = 
  \begin{cases}
  u_1: \text{Sell} \\
  u_2: \text{Wait}
  \end{cases}
  $$
  
- **State**:  
  $$
  x_k \in \mathbb{R}_+ \cup \{T\}
  $$
  
- **System Equation**:  
  $$
  x_{k+1} = 
  \begin{cases}
  T, & \text{if } x_k = T \text{ or } (x_k \neq T \text{ and } \mu_k = u_1) \\
  w_k, & \text{otherwise}
  \end{cases}
  $$
  
- **Reward Function**:  
  $$
  \mathbb{E}_{w_0, \ldots, w_{N-1}} \left[ g_N(x_N) + \sum_{k=0}^{N-1} g_k(x_k, \mu_k, w_k) \right]
  $$
  
  where:
  $$
  g_N(x_N) = 
  \begin{cases}
  x_N, & \text{if } x_N \neq T \\
  0, & \text{if } x_N = T
  \end{cases}
  $$
  (i.e., the seller must accept the offer by time N)

  and for $k = 0, 1, \ldots, N-1$:
  $$
  g_k(x_k, \mu_k, w_k) = 
  \begin{cases}
  (1 + r)^{N-k} x_k, & \text{if } x_k \neq T \text{ and } \mu_k = u_1 \\
  0, & \text{otherwise}
  \end{cases}
  $$

**Note**:  
Once the seller accepts an offer, she gets the compound interest for the rest of the horizon all together, and from then onwards, she gets zero reward.



### Problem Formulation
- We consider an asset selling problem as an optimal stopping problem
- Assume offers are i.i.d., with distribution $w \sim F(\cdot)$

### DP Formulation
Terminal value function:
$$
J_N(x_N) =
\begin{cases}
x_N, & \text{if } x_N \neq T \\
0, & \text{if } x_N = T
\end{cases}
$$

Backward recursion for $k = 0, 1, \dots, N-1$:
$$
J_k(x_k) =
\begin{cases}
\max \left\{ (1 + r)^{N - k} x_k, \mathbb{E}[J_{k+1}(w_k)] \right\}, & x_k \neq T \\
0, & x_k = T
\end{cases}
$$

### Optimal Policy
Accept offer only if:
$$
x_k > \alpha_k \triangleq \frac{\mathbb{E}[J_{k+1}(w_k)]}{(1 + r)^{N - k}}
$$

This defines a threshold-type policy. At each time $k$, accept if offer $x_k$ exceeds $\alpha_k$, otherwise wait.

### Proposition 3.3.1
Assume offers $w_k$ are i.i.d., with distribution $w \sim F(\cdot)$. Then the threshold satisfies:
$$
\alpha_k \geq \alpha_{k+1}, \quad \text{for } k = 0, 1, \dots, N - 1, \quad \text{with } \alpha_N = 0
$$

### Proof
For now, let's disregard the terminal condition, and define:
$$
V_k(x_k) \triangleq \frac{J_k(x_k)}{(1 + r)^{N - k}}, \quad x_k \neq T
$$

We can rewrite the recursion equations as follows:
$$
V_N(x_N) = x_N
$$
$$
V_k(x_k) = \max \left\{ x_k, (1 + r)^{-1}\mathbb{E}[V_{k+1}(w)] \right\}, \quad k = 0, \dots, N - 1
$$

From this, we define:
$$
\alpha_k = \frac{\mathbb{E}[V_{k+1}(w)]}{1 + r}, \quad k = 0, 1, ..., N - 1
$$

Hence, defining $\alpha_N = 0$ (since we have to accept no matter what in the last period), we get:
$$
\alpha_k = \frac{\mathbb{E}[V_{k+1}(w)]}{1 + r}, \quad k = 0, 1, ..., N - 1
$$

Next, we compare the value function at periods $N-1$ and $N$: For $k = N$ and $k = N - 1$, we have:
$$
V_N(x) = x
$$
$$
V_{N-1}(x) = \max\{x, (1 + r)^{-1}\mathbb{E}[V_N(w)]\} \geq V_N(x)
$$

Given that we have a stationary system, from the monotonicity of DP, we know that:
$$
V_1(x) \geq V_2(x) \geq ... \geq V_N(x), \quad \forall x
$$

Since $\alpha_k = \frac{\mathbb{E}[V_{k+1}(w)]}{1 + r}$ and $\alpha_{k+1} = \frac{\mathbb{E}[V_{k+2}(w)]}{1 + r}$, we have $\alpha_k \geq \alpha_{k+1}$.