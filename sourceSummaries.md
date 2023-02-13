# General Statistics Notes
## Hypothesis Testing

When attempting to model using statistics, it is common to use hypothesis testing.

**Definition:** Null hypothesis, $H_0$, states there is no relationship between the variables being analyzed.

**Definition:** Alternative hypothesis, $H_a$ states there is a relationship between the variables being analyzed.

**In the context of radiation detection, the null hypothesis is that any measured counts are not attributable to radioactive material (radmat). The alternative hypothesis states that the measured counts are distinguishable from background radiation and are due to radmat.**

**Definition:** A priori means choosing independent of current experiments.

**Definition:** A posteriori means choosing based on information from current experiments.

There are four cases when choosing a hypothesis:

| | $H_0$ is true | $H_0$ is false|
|---|---|---|
|Fail to reject $H_0$ | Correct Inference | Type II Error: False Negative|
|Reject $H_0$ | Type I Error: False Positive | Correct Inference|

The goal is to minimize the likelihood of type 1 and type 2 error.

## Confidence Intervals

### Gaussian Interval

$$
k_\alpha = \sqrt{2}\mathrm{inverf}(2 - 2\alpha)
$$
### Z-Test

### T-Test

## Bayseian Basics
**These ideas come primarily from the bayesian statistics lectures notes given by Michael Baron and American University.**

| Concept | Definition |
|---|---|
|$\theta$ | Some parameter we wish to describe. Could be mean, variance, probability, etc|
|$\theta_0$ | True population value for parameter $\theta$. |
|$\hat{\theta}, \delta$ | Estimator for parameter $\theta$. |
|$\mathcal{A}$ | $\delta\in\mathcal{A}$ <br> Action space, space of possible estimators. |
|$\pi(\theta)$ | Prior distribution (pmf or pdf) <br> Understanding of $\theta$ prior to seeing new data. |
|$f\left(\left.\pmb{X}=\pmb{x}\right\|\theta\right)$ | Probability of measuring obtaining data $\{x_i\}$ given the prior understanding of $\theta$ |
|$m(\pmb{X}=\pmb{x})$ | Marginal distribution <br> Total probability of obtaining the data set $\{x_i\}$. 
|$\pi\left(\left.\theta\right\|\pmb{X}=\pmb{x}\right)$ | Posterior distribution <br> Updated probability distribution for $\theta$ given the current data. |

$$
\boxed{
    \pi\left(\left.\theta\right|\pmb{X}=\pmb{x}\right) = \frac{
        f\left(\left.\pmb{X}=\pmb{x}\right|\theta\right)
    }{m(\pmb{X}=\pmb{x})} \times \pi(\theta)
}
$$
$$
\begin{align*}
m(\pmb{X}=\pmb{x}) 
&= 
\sum_\theta f\left(\left.\pmb{X}=\pmb{x}\right|\theta\right) \pi(\theta) \\
&=
\int f\left(\left.\pmb{X}=\pmb{x}\right|\theta\right) \pi(\theta) d\theta
\end{align*}
$$

The general idea in Bayesian statistics is to update the probability distribution given some data. This looks at comparing the probability of the data occuring given our prior understanding, compared to the probability of the data occuring regardless of the underlying parameter. 

This can in turn be used to calculate the posterior distribution of the parameter, given what is currently known. 

### Bayesian Example
*A company produces products and claims an error rate of 5%. Their competator claims they have an error rate of 10%. When sampling 20 of their product, we find that 3 of them are defective. What can be done with this information?*

The probability of failure should follow a binomial distribution $\mathrm{Binomial}(20,p)$ in which $p$ is the parameter we wish to estimate. This is the probability of failure. In this case, we may say that our prior distribution is:

$$
\begin{align*}
\pi(p=0.05) &= 0.5 \\
\pi(p=0.10) &= 0.5 \\
\end{align*}
$$

The probability of measuring three failures if the failure rate is 5% is:

$$
\begin{align*}
f(3|p=0.05)
&=
C(20,3)\cdot \left(0.05\right)^3 \cdot (0.95)^{17}\\
&=
1140\cdot 55.265\cdot 10^{-6} \\
&=
0.0596
\end{align*}
$$

The probability of measuring three failures if the failure rate is 10% is:

$$
\begin{align*}
f(3|p=0.10)
&=
C(20,3)\cdot \left(0.1\right)^3 \cdot (0.9)^{17}\\
&=
1140\cdot 55.265\cdot 10^{-6} \\
&=
0.0596\cdot 166.77\cdot 10^{-6} \\
&=
0.19
\end{align*}
$$

The marginal probability of having three failures is:

$$
\begin{align*}
m(3)
&=
f(3|p=0.05)\cdot\pi(p=0.05) +
f(3|p=0.10)\cdot\pi(p=0.10) \\
&=
\frac{1}{2}\cdot\left[
0.0596+0.19
\right] \\ &=
0.12485
\end{align*}
$$

The probability that the failure rate is 5% is:

$$
\begin{align*}
\pi(p=0.05|3)
&=
\frac{0.0596}{0.12485} \cdot 0.5
\\ &=
23.9\%
\end{align*}
$$

The probability that the failure rate is 10% is:

$$
\begin{align*}
\pi(p=0.10|3)
&=
\frac{0.19}{0.12485} \cdot 0.5
\\ &=
76.1\%
\end{align*}
$$

This indicates that it is more likely that the failure rate is 10%.



# Frequentist Methods 
## Currie 1968

There are three detection thresholds which are used. These are the:

| Limit | Explaination |
|---|---|
| Critical Level, $L_C$ | "one may decide whether of not the result of an analysis indicates detection." <br> minimum value in which counts may be distinguished from background radiation. 
| Detection Limit, $L_D$ | "a given analytical procedure may be relied upon to lead to detection." <br> minimum level at which 
| Determination Limit, $L_Q$ |

Suppose in some period of time, $B$ counts are measured from background. In another period of time $C=S+B$ counts are measured in which $S$ is some amount of counts we wish the distinguish from background. 

| Quantity | Observed Value | True Mean | Standard Deviation |
|---|---|---|---|
Background | $B$ | $\mu_B$ | $\sigma_B = \sqrt{B}$
Gross Signal | $C$ | $\mu_{C}$ | $\sigma_C = \sqrt{C}$
Net Signal | $S=C-B$ | $\mu_S = \mu_C - \mu_B$ | $\sigma_S = \sqrt{\sigma_C^2 + \sigma_B^2}$

The goal is to take measurements $\{B,C\}$ and determine whether or not $\mu_S > 0$, and determine the minimum value of $\mu_S$ which can both reliably be said to be above zero and the minimum value which may be reliable determined quantitatively. 

The first question is a binary  qualitative decision on whether radioactive material is present and is determined *a posteriori*, ie must be decided upon after taking measurements.

The questions of the minimum signal strength which can be determined quantitatively is decied *a priori*, ie must be known about the measurement technique prior to making measurements.

The critical level $L_C$ is chosen to minimize the possibility of Type I error: stating a sample contains radioactive material when it does not. If $P[\text{Reject } H_0 | H_0\text{ is True}]=\alpha$ is the confidence interval required to minimize Type I error, and $\sigma_0$ is the standard deviation of measurements when $\mu_S=0$, then the critical level is:

$$
L_C = k_\alpha \sigma_0
$$

This is the smallest value of $S$ which may said to be above background with a probability of $1-\alpha$. 

The detection limit $L_D$ is chosen to minimize the possibility of Type II error: stating a sample does not contain radioactive material when it does. If $P[\text{Fail to Reject } H_0 | H_0\text{ is False}]=\beta$ is the confidence interval required to minimize Type II error, $\sigma_D$ is the standard deviation of measurements made at $S=L_D$, then:

$$
L_D = L_C + k_\beta \sigma_D
$$

If $S>L_D$, then 





## ISO 11929-1:2019

### Definitions

#### Measurand
$$ Y $$

Quantity subject to measurement. This value is non-negative and does not include background radiation sources.

#### Measurement Procedure
Operating procedure for measuring measurand

#### 

## EPA (MARSSIM / MARLAP)

## IUPAC

# Bayesian Methods

## Brandl 2013

## Brogan 2018

## Meengs 2018

## Meengs 2021

# Regulatory Studies of Portal Monitors

## IEEE Border Crossings

## IAEA Border Crossings