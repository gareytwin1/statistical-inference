# Module 2: Fundamental Concepts of Hypothesis Testing 

## 1. Core Terminology

- **Population**: entire group of interest.  
- **Sample**: observed data from the population.  
- **Random sample (iid)**: $X_1, \, \dots, \, X_n$ are **independent** and **identically distributed** from the same population.

---

## 2. Normal Distribution & Sample Mean

- If $X \sim N(\mu, \sigma^2)$:
  - Mean: $E[X] = \mu$  
  - Variance: $\operatorname{Var}(X) = \sigma^2$

- If $X_1, \dots, X_n$ are iid $N(\mu, \sigma^2)$, the **sample mean**

$$
\bar X = \frac{1}{n} \sum_{i=1}^n X_i
$$

has distribution

$$
\bar X \sim N\left(\mu, \frac{\sigma^2}{n}\right).
$$

So the mean is $\mu$ and the variance shrinks by a factor of $n$.

---

## 3. Standardization and Z

- **Standard normal**: $Z \sim N(0, 1)$.  
- If $X \sim N(\mu, \sigma^2)$, then

$$
Z = \frac{X - \mu}{\sigma} \sim N(0, 1).
$$

- For the **sample mean**,

$$
Z = \frac{\bar X - \mu}{\sigma / \sqrt{n}}.
$$

In R:

- `pnorm(z)` gives $P(Z \le z)$.  
  - **Example**: `pnorm(1.96)` ≈ 0.975, meaning $P(Z \le 1.96) = 0.975$
  - **Example**: `pnorm(-1.5)` ≈ 0.067, meaning $P(Z \le -1.5) = 0.067$
 
- `qnorm(p)` gives the value $z_p$ with $P(Z \le z_p) = p$.
  - **Example**: `qnorm(0.95)` ≈ 1.645, meaning the 95th percentile of standard normal is 1.645

---

## 4. Testing a Mean ($\sigma$ known, one-sided z-test)

Setup: observe $\bar X$ from iid $N(\mu, \sigma^2)$.

### Right-tailed test (mean too big)

- **Hypotheses**:  
  - $H_0: \mu = \mu_0$  
  - $H_1: \mu > \mu_0$

- **Test statistic**:

$$
Z = \frac{\bar X - \mu_0}{\sigma / \sqrt{n}}.
$$

- For significance level $\alpha$: critical value  
  $z_\alpha = \texttt{qnorm}(1 - \alpha)$.

- **Rejection rule**: reject $H_0$ if $Z > z_\alpha$, or equivalently if

$$
\bar X > \mu_0 + z_\alpha \cdot \frac{\sigma}{\sqrt{n}}.
$$

### Left-tailed test (mean too small)

- **Hypotheses**:  
  - $H_0: \mu = \mu_0$  
  - $H_1: \mu < \mu_0$

- Same test statistic $Z$.

- Critical value: $z_\alpha = \texttt{qnorm}(\alpha)$ (a negative number for small $\alpha$).

- **Rejection rule**: reject $H_0$ if $Z < z_\alpha$, or equivalently if

$$
\bar X < \mu_0 + z_\alpha \cdot \frac{\sigma}{\sqrt{n}}.
$$

---

## 5. Type I & Type II Errors

- **Type I error**: reject $H_0$ when $H_0$ is true.  
  - Probability = $\alpha$ (the significance level).
- **Type II error**: fail to reject $H_0$ when $H_0$ is false.  
  - Probability = $\beta$ (depends on the true $\mu$, $n$, $\sigma$, and the decision rule).
- **Which is worse?** There is **no universal answer**. The relative severity of Type I vs Type II is **problem-dependent**.

---

## 6. Key Examples (Concept Check)

### (a) 40-amp fuses – interpreting errors

- $H_0: \mu = 40$: mean amperage OK.  
- $H_1: \mu > 40$: mean amperage too high.

- **Type I error**: mean really is OK, but the manufacturer concludes it is too high and launches an unnecessary recall.  
- **Type II error**: mean really is too high, but the manufacturer concludes it is acceptable, increasing liability risk.

---

### (b) Horses / ketamine – left-tailed z-test

- $n = 73$, $\bar x = 18.86$, $\sigma = 8.6$, $\alpha = 0.10$.  
- Hypotheses:
  - $H_0: \mu = 20$  
  - $H_1: \mu < 20$

1. **Critical z**: $z_{0.10} \approx -1.28$.  
2. **Test statistic**:

   $$
   Z = \frac{18.86 - 20}{8.6/\sqrt{73}} \approx -1.13.
   $$

3. **Decision**: since $-1.13 > -1.28$, we **fail to reject $H_0$**.  
   - Interpretation: Data do not provide strong enough evidence that the mean recumbency time is less than 20 minutes.

---

### (c) Zinc intake – find cutoff for $\bar x$

- $n = 12$, variance $\sigma^2 = 6.43$ (so $\sigma = \sqrt{6.43}$), $\alpha = 0.05$, left-tailed.  
- Hypotheses:
  - $H_0: \mu = 15$  
  - $H_1: \mu < 15$

We want a critical value $c$ for $\bar x$ such that we reject $H_0$ when $\bar x < c$.

- Use

$$
c = \mu_0 + z_\alpha \cdot \frac{\sigma}{\sqrt{n}},
$$

with $z_{0.05} \approx -1.645$ and $\sigma = \sqrt{6.43}$.

- Result: $c \approx 13.80$.

**Rule**: reject $H_0$ if $\bar x < 13.80$.

---

### (d) Training program – largest $\bar x$ that still leads to switching

- $n = 15$, $\sigma = 3.2$, $\alpha = 0.01$, left-tailed.  
- Hypotheses:
  - $H_0: \mu = 50$ (current average training time)  
  - $H_1: \mu < 50$ (new program shorter)

We want the **largest** sample mean $\bar x$ for which we still **reject** $H_0$.

- Critical mean:

$$
c = 50 + z_{0.01} \cdot \frac{\sigma}{\sqrt{n}},
$$

with $z_{0.01} \approx -2.33$.

- Result: $c \approx 48.08$.

**Rule**: the company switches to the online program if $\bar x < 48.08$ days.

---
