# Module 3 Study Guide  
**Topic:** Power, Optimal Tests, and Comparing Means  

---

## 1. Review: Hypothesis Tests, Type I & Type II Errors

We still frame tests as:

- Null: $H_0$ (status quo or "no effect")
- Alternative: $H_1$ (new claim / effect)

For a test built from some statistic $T(X)$:

- **Type I error**: Reject $H_0$ when $H_0$ is true  
  - Probability = $\alpha$, the **size** or **level of significance** of the test.
- **Type II error**: Fail to reject $H_0$ when $H_1$ is true  
  - Probability = $\beta$.  
- **Power** of a test at parameter value $\theta$:  
  $$
  \text{power}(\theta) = P(\text{reject }H_0 \mid \theta) = 1 - \beta(\theta).
  $$

For a simple vs simple normal-mean test with known variance:
$$
H_0:\mu=\mu_0,\quad H_1:\mu=\mu_1,\quad \sigma^2 \text{ known}
$$
one (right-tailed) rejection rule is of the form
$$
\bar X > \mu_0 + z_{1-\alpha}\frac{\sigma}{\sqrt{n}}.
$$
The constant $c = \mu_0 + z_{1-\alpha}\sigma/\sqrt{n}$ is chosen so that $P(\text{Type I error}) = \alpha$.  

Given this rule, the **Type II error at $\mu_1$** is
$$
\beta = P_{\mu_1}\Big(\bar X \le \mu_0 + z_{1-\alpha}\frac{\sigma}{\sqrt{n}}\Big),
$$
which can be computed using a normal CDF after standardizing.  

---

## 2. Composite Hypotheses & the Power Function

Now we move beyond simple vs simple tests and allow **composite hypotheses**:

- $H_0: \theta \in \Theta_0$
- $H_1: \theta \in \Theta_1 = \Theta \setminus \Theta_0$  

### 2.1 Power Function

The **power function** of a test is
$$
\gamma(\theta) = P_\theta(\text{reject } H_0),
$$
defined for **all** $\theta$ in the parameter space $\Theta$.  

Key facts:

- For $\theta \in \Theta_0$, $\gamma(\theta)$ is the Type I error probability at that $\theta$.
- For $\theta \in \Theta_1$, $1 - \gamma(\theta)$ is the Type II error probability at that $\theta$.
- The **size** of the test is
  $$
  \alpha = \max_{\theta \in \Theta_0} \gamma(\theta), 
  $$
  i.e., the worst-case Type I error over all parameter values allowed by $H_0$.  
- A (worst-case) **Type II error bound** is
  $$
  \beta = \max_{\theta \in \Theta_1} \big[1 - \gamma(\theta)\big].
  $$

**Comparing tests:**  
Given two tests with power functions $\gamma_1(\theta)$ and $\gamma_2(\theta)$:

- If they have the same size $\alpha$, the test with **larger power** $\gamma(\theta)$ for all $\theta$ in $\Theta_1$ is **better**.  
- On the power-function graph, the "better" test lies **above** the other in the region where $H_0$ is false.

---

## 3. One-Sided Test for a Normal Mean (Known \(\sigma\)), Composite \(H_0\)

Example setup:  
$$
H_0: \mu \ge \mu_0 \quad\text{vs}\quad H_1: \mu < \mu_0,
$$
with $X_1,\dots,X_n \sim N(\mu,\sigma^2)$, $\sigma^2$ known.  

### 3.1 Deriving a Level-\(\alpha\) Test

We choose the statistic $\bar X$ and consider rejection regions of the form:
$$
\text{Reject }H_0\ \text{if }\ \bar X < c.
$$

To make this a **size $\alpha$** test:

$$
\alpha = \max_{\mu \ge \mu_0} P_\mu(\bar X < c).
$$

Because $P_\mu(\bar X < c)$ is **decreasing** in $\mu$, the maximum occurs at $\mu = \mu_0$, so
$$
\alpha = P_{\mu_0}(\bar X < c).
$$  

Standardizing:
$$
P_{\mu_0}(\bar X < c) = P\left(Z < \frac{c-\mu_0}{\sigma/\sqrt{n}}\right)
  = \alpha,
$$
so
$$
\frac{c-\mu_0}{\sigma/\sqrt{n}} = z_\alpha
\quad\Rightarrow\quad
c = \mu_0 + z_\alpha\frac{\sigma}{\sqrt{n}}.
$$  

**Final test:**
$$
\boxed{\text{Reject }H_0 \text{ in favor of } H_1 \text{ if } \bar X < \mu_0 + z_\alpha\frac{\sigma}{\sqrt{n}}.}
$$  

### 3.2 Power Function for This Test

For any \(\mu\), the power is
\[
\gamma(\mu) = P_\mu\left(\bar X < \mu_0 + z_\alpha\frac{\sigma}{\sqrt{n}}\right).
\]

Standardizing:
\[
\gamma(\mu) = 
P\left(
Z < 
\frac{\mu_0 + z_\alpha\frac{\sigma}{\sqrt{n}} - \mu}{\sigma/\sqrt{n}}
\right)
=
\Phi\left(
\frac{\mu_0 - \mu}{\sigma/\sqrt{n}} + z_\alpha
\right).
\]  

Graphically (see slides):

- On the horizontal axis: \(\mu\).
- On the vertical axis: \(\gamma(\mu)\).
- At \(\mu = \mu_0\), \(\gamma(\mu_0) = \alpha\) (this is where you “locate” \(\alpha\) on the power function).  
- For \(\mu < \mu_0\) (where \(H_1\) is true), power increases toward 1 as \(\mu\) moves farther from \(\mu_0\).

---

## 4. Size, Power, and “Best” Tests

For composite hypotheses, the slides define formally:

- **Size**:
  \[
  \alpha = \max_{\mu \in \Theta_0} P_\mu(\text{reject }H_0).
  \]
- **Worst-case Type II error**:
  \[
  \beta = \max_{\mu \in \Theta_1} P_\mu(\text{fail to reject }H_0).
  \]
- **Power** (function): \(\gamma(\mu) = P_\mu(\text{reject }H_0)\).  

Intuition from graphs on the slides:

- In the region where \(H_0\) is **true**, we want the curve near **0** (low chance of rejecting).
- In the region where \(H_0\) is **false**, we want the curve near **1** (high probability of rejecting).  
- Among tests with the same size, a test whose power function is “higher” for all \(\mu\) in \(\Theta_1\) is **more powerful** / **better**.  

---

## 5. Distributions of p-values (Notebook ideas)

The notebooks for this module explore **distributions of p-values** through simulation:

- Under a **true** null hypothesis (continuous test statistic), p-values are approximately **Uniform(0,1)**.
- Under a **false** null (i.e., \(H_1\) true), p-values tend to be **concentrated near 0**; the distribution is skewed with more small values.
- If you mix some proportion of true nulls and false nulls (e.g., multiple tests), the p-value histogram will be a mix of:
  - A flat component (from true nulls),
  - A spike near 0 (from false nulls).

Typical notebook steps:

1. Fix a test (e.g., z-test for a mean).
2. Simulate many samples under \(H_0\), compute p-values, and plot a histogram.
3. Simulate many samples under \(H_1\), compute p-values, and compare histograms.
4. Note how **smaller p-values correspond to higher power** and how **larger sample size** makes p-values move closer to 0 when \(H_1\) is true (power increases).

These simulations reinforce:

- A single p-value tells you how extreme your data are under \(H_0\).
- The **distribution** of p-values across repeated experiments reflects the power properties of the test.

---

## 6. Two-Sample Problems: Independent Samples, Unequal Variances (Welch’s t-test)

We now move to comparing **two populations**, with data:

- \(X_1,\dots,X_{n_1} \sim N(\mu_1,\sigma_1^2)\)  
- \(Y_1,\dots,Y_{n_2} \sim N(\mu_2,\sigma_2^2)\)  

Samples are independent, and both \(\sigma_1^2\) and \(\sigma_2^2\) are **unknown and not assumed equal**.  

We want to test:
\[
H_0: \mu_1 = \mu_2 \quad \text{vs}\quad H_1: \mu_1 \ne \mu_2
\]
(or one-sided versions).  

Because variances are unequal, the classic pooled-variance t-test is not appropriate. This is the **Behrens–Fisher problem**. The standard solution is **Welch’s t-test**.:contentReference[oaicite:17]{index=17}  

### 6.1 Welch’s t Statistic

Let

- \(\bar X, s_1^2\): sample mean and variance of group 1
- \(\bar Y, s_2^2\): sample mean and variance of group 2

Welch’s test uses
\[
T = \frac{\bar X - \bar Y - (\mu_1-\mu_2)_0}{\sqrt{\_
