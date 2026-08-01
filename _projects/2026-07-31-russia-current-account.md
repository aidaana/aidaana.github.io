---
title: "The Intertemporal Approach to the Current Account: Testing the Consumption-Smoothing Hypothesis"
subtitle: "Evidence from Russia, 1995–2025"
layout: post
category: data-analysis
---
<script>
MathJax = {
  tex: {
    tags: 'ams',
    inlineMath: [['$', '$'], ['\\(', '\\)']]
  }
};
</script>
<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

#### Table of Contents

- [1. Introduction](#1-introduction)
- [2. Theoretical Framework](#2-theoretical-framework)
  - [2.1 Present Value Model of the Current Account](#21-present-value-model-of-the-current-account)
  - [2.2 VAR-Based Predicted Current Account](#22-var1-based-predicted-current-account)
- [3. Empirical Analysis](#3-empirical-analysis)
  - [3.1 Data](#31-data)
  - [3.2 VAR Estimation](#32-var-estimation)
  - [3.3 Predicted Current Account](#33-predicted-current-account)
  - [3.4 Wald Test](#34-wald-test)
- [4. Conclusion](#4-conclusion)
- [References](#references)
- [Data Sources](#data-sources)

### 1. Introduction

This report examines the empirical validity of the stochastic intertemporal current 
account model presented by Obstfeld and Rogoff (1996, Ch. 2), applied to Russia. 
Following their derivation, I first present the model's key theoretical results: the 
stochastic current account identity, which expresses the current account as the gap 
between actual and expected present-value net output (eq. 42), and the predicted 
current account, based on a VAR in net output changes and the current account 
(eq. 45). I then estimate this VAR using quarterly data on GDP, government spending, 
investment, and the current account for Russia over the period 1995Q2–2025Q1, 
construct the model-implied predicted current account \(\small \widehat{CA}_t\(, and test 
the model using a Wald test. The results reject the 
model's restriction that \(\small \Phi_{\Delta Z}=0\( and \(\Phi_{CA}=1\( (\(W=9.28\(, 
$p<0.01$), indicating that Russia's current account does not conform exactly to 
the consumption-smoothing hypothesis, although the model-predicted series 
tracks the direction and timing of actual current account movements 
reasonably well throughout the sample.

### 2. Theoretical framework
#### 2.1 Present value model of the current account

Following Obstfeld and Rogoff (1996, ch. 2), the current account identity under 
certainty is (eq. 18 in the original):

$$
\small
CA_t = B_{t+1} - B_t = (Y_t - \tilde{Y}_t) - (I_t - \tilde{I}_t) - (G_t - \tilde{G}_t),
\tag{1}
$$

where the tilde ($\small \tilde{X}_t$) denotes the permanent value of a variable, based on 
the present discounted value of its future path (eq. 17 in the original):

$$
\small
\tilde{X}_t \equiv \frac{r}{1+r} \sum_{s=t}^{\infty} \left(\frac{1}{1+r}\right)^{s-t} X_s.
\tag{2}
$$

To derive the current account identity in a stochastic setting, we start from the 
individual's optimization problem under uncertainty, in which a representative 
consumer maximizes the expected value of lifetime utility subject to the 
intertemporal budget constraint. The resulting stochastic Euler equation is 
(eq. 29 in the original):

$$
\small
u'(C_t) = (1+r)\beta \, \mathrm{E}_t\{u'(C_{t+1})\}
\tag{3}
$$

Assuming a quadratic utility function (eq. 30 in the original), $\small u(C) = C - \frac{a_0}{2}C^2$, and imposing $\small \beta(1+r) = 1$, the Euler equation (3) reduces to (eq. 31 in the 
original):

$$
\small
\mathrm{E}_t C_{t+1} = C_t,
\tag{4}
$$

so that consumption follows a random walk.

Intertemporal budget constraint in expectation is as follows:

$$
\small
\mathrm{E}_t \left\{ \sum_{s=t}^{\infty} \left(\frac{1}{1+r}\right)^{s-t} (C_s + I_s) \right\}
= \mathrm{E}_t \left\{ (1+r)B_t + \sum_{s=t}^{\infty} \left(\frac{1}{1+r}\right)^{s-t} (Y_s - G_s) \right\}.
\tag{5}
$$

Under quadratic utility, the random-walk result (4) implies $\small \mathrm{E}_t C_s = C_t$ 
for all $\small s > t$. Substituting $C_t$ for $\mathrm{E}_t C_s$ inside the sum on the 
left-hand side of (5) and using the geometric-sum formula 
$\small \sum_{s=t}^{\infty}(1/(1+r))^{s-t} = (1+r)/r$, yields the 
certainty-equivalence consumption function (eq. 32 in the original), which is 
the expected-value version of the permanent-income consumption function 
(eq. 10 in the original):

$$
\small
C_t = \frac{r}{1+r} \left[ (1+r)B_t + \sum_{s=t}^{\infty} \left(\frac{1}{1+r}\right)^{s-t} \mathrm{E}_t\{Y_s - G_s - I_s\} \right].
\tag{6}
$$

Using the definition of the permanent (annuity) value of a variable $\small X$,

$$
\small
\mathrm{E}_t \tilde{X}_t \equiv \frac{r}{1+r} \sum_{s=t}^{\infty} \left(\frac{1}{1+r}\right)^{s-t} \mathrm{E}_t X_s,
\tag{7}
$$

equation (6) can be rewritten compactly as

$$
\small
C_t = rB_t + \mathrm{E}_t \tilde{Y}_t - \mathrm{E}_t \tilde{I}_t - \mathrm{E}_t \tilde{G}_t.
\tag{8}
$$

Finally, substituting the certainty-equivalence consumption function (8) into the 
definition of the current account, $\small CA_t = rB_t + (Y_t - I_t - G_t - C_t)$, 
gives an equation parallel to the deterministic identity (1), with the 
present discounted sums replaced by their expected values. This is the 
stochastic current account identity (eq. 42 in the original), the first key result in this paper:

$$
\small
CA_t = B_{t+1} - B_t = (Y_t - \mathrm{E}_t\tilde{Y}_t) - (I_t - \mathrm{E}_t\tilde{I}_t) - (G_t - \mathrm{E}_t\tilde{G}_t).
\tag{9}
$$

Next, we'll derive the Campbell (1987) representation (eq. 43 in the original) in order to derive testable prediction equations.

Defining net output $\small Z_t$ as $\small Z_t \equiv Y_t - G_t - I_t$ and substituting it into the stochastic current account identity (9) leads to a compact form:

$$
\small
CA_t = Z_t - \mathrm{E}_t \tilde{Z}_t,
\tag{10}
$$

where

$$
\small
\mathrm{E}_t \tilde{Z}_t = \frac{r}{1+r} \sum_{s=t}^{\infty} \left(\frac{1}{1+r}\right)^{s-t} \mathrm{E}_t Z_s. 
\tag{11}
$$

It is convenient to introduce the lag operator $\small L$, defined by $\small L^k Z_t \equiv Z_{t-k}$, 
so that the lead operator is $ \small L^{-k} Z_t \equiv Z_{t+k}$.

Relabeling index and using $\small L^{-1}$, the forecast sum (11) can be written compactly as a geometric series in the lead operator:
$$
\small
\begin{aligned}
\mathrm{E}_t \tilde{Z}_t &= \frac{r}{1+r}\sum_{k=0}^{\infty}\left(\frac{1}{1+r}\right)^{k}\mathrm{E}_t Z_{t+k} \\
&= \frac{r}{1+r} \sum_{k=0}^{\infty} \left(\frac{L^{-1}}{1+r}\right)^k Z_t \\
&= \frac{r}{1+r} \left(1 - \frac{L^{-1}}{1+r}\right)^{-1} Z_t
\end{aligned}
$$


Substituting the result into (10):

$$
\small
CA_t = Z_t - \frac{r}{1+r}\left(1 - \frac{L^{-1}}{1+r}\right)^{-1} Z_t.
$$

Premultiplying both sides by $\small \left(1 - \frac{L^{-1}}{1+r}\right)$ removes the 
inverse operator on the right-hand side:

$$
\small
\begin{aligned}
\left(1 - \frac{L^{-1}}{1+r}\right) CA_t &= \left(1 - \frac{L^{-1}}{1+r}\right) Z_t - \frac{r}{1+r} Z_t \\
&= Z_t - \frac{Z_{t+1}}{1+r} - \frac{r}{1+r}Z_t \\
&= -\frac{\Delta Z_{t+1}}{1+r} 
\end{aligned}
$$

where $\small \Delta Z_{t+1} \equiv Z_{t+1} - Z_t$. <br>
Inverting the lag-operator expression back onto $\small CA_t$ and expanding the operator as a geometric series gives:

$$
\small
\begin{aligned}
CA_t &= -\left(1 - \frac{L^{-1}}{1+r}\right)^{-1} \frac{\Delta Z_{t+1}}{1+r} \\
&= -\sum_{k=0}^{\infty} \left(\frac{L^{-1}}{1+r}\right)^k \frac{\Delta Z_{t+1}}{1+r}.
\end{aligned}
$$

Applying the lead operator to each summation results in: 

$$
\small
\begin{aligned}
CA_t &= -\frac{1}{1+r} \sum_{k=0}^{\infty} \left(\frac{1}{1+r}\right)^k \mathrm{E}_t \Delta Z_{t+1+k} \\
&= - \sum_{k=0}^{\infty} \left(\frac{1}{1+r}\right)^{k+1} \mathrm{E}_t \Delta Z_{t+1+k}. 
\end{aligned}
$$

Finally, relabeling the index with $\small s = t + 1 + k$ yields:
$$
\small
CA_t = -\sum_{s=t+1}^{\infty} \left(\frac{1}{1+r}\right)^{s-t} \mathrm{E}_t \Delta Z_s,
\tag{12}
$$

which is the Campbell (1987) representation of the current account (eq. 43 in the original). Equation (12) represents the present value model of the current account. It shows the inverse relationship between the present discounted value of expected future net output changes and today's current account.

#### 2.2 VAR(1)-based predicted current account

Since (12) shows that the current account depends on expected future net output 
changes, the model requires a way to forecast $\small \Delta Z_s$. 
Following Campbell (1987), Obstfeld and Rogoff assume that consumers form 
forecasts of future net output changes, $\small \Delta Z_s$ for $s > t$, using not only 
the univariate history of $\small \Delta Z$ but also the history of the current account 
itself. This additional information is incorporated by modeling $\small \Delta Z_t$ and 
$\small CA_t$ as a first-order vector autoregression (VAR), expressed as 
deviations from their unconditional means:

$$
\small
\begin{bmatrix} \Delta Z_s \\ CA_s \end{bmatrix}
= \begin{bmatrix} \psi_{11} & \psi_{12} \\ \psi_{21} & \psi_{22} \end{bmatrix}
\begin{bmatrix} \Delta Z_{s-1} \\ CA_{s-1} \end{bmatrix}
+ \begin{bmatrix} \epsilon_{1s} \\ \epsilon_{2s} \end{bmatrix},
\tag{13}
$$

where $\epsilon_1$ and $\epsilon_2$ are shocks with conditional mean zero. Defining 
$\small \Psi \equiv \begin{bmatrix} \psi_{11} & \psi_{12} \\ \psi_{21} & \psi_{22} \end{bmatrix}$, 
the $s$-period-ahead forecast implied by (13) is obtained by iterating the VAR 
forward:

$$
\small
\mathrm{E}_t \begin{bmatrix} \Delta Z_s \\ CA_s \end{bmatrix}
= \Psi^{s-t} \begin{bmatrix} \Delta Z_t \\ CA_t \end{bmatrix}.
$$

Premultiplying by the row vector $\small \begin{bmatrix} 1 & 0 \end{bmatrix}$ isolates $\small \Delta Z_s$:

$$
\small
\mathrm{E}_t \Delta Z_s = \begin{bmatrix} 1 & 0 \end{bmatrix} \Psi^{s-t}
\begin{bmatrix} \Delta Z_t \\ CA_t \end{bmatrix}.
\tag{14}
$$

Substituting (14) into the Campbell representation (12) of $\small CA_t$ gives:

$$
\small
CA_t = -\begin{bmatrix} 1 & 0 \end{bmatrix}
\left[ \sum_{s=t+1}^{\infty} \left(\frac{1}{1+r}\right)^{s-t} \Psi^{s-t} \right]
\begin{bmatrix} \Delta Z_t \\ CA_t \end{bmatrix}
\tag{15}.
$$

The term in brackets is a matrix geometric series. Using $\small j = s-t$ and factoring out $\frac{\Psi}{1+r}$:

$$
\small
\begin{aligned}
\sum_{s=t+1}^{\infty} \left(\frac{\Psi}{1+r}\right)^{s-t}
&= \sum_{j=1}^{\infty} \left(\frac{\Psi}{1+r}\right)^{j} \\
&= \frac{\Psi}{1+r} \sum_{j=0}^{\infty} \left(\frac{\Psi}{1+r}\right)^{j} \\
&= \frac{\Psi}{1+r} \left(\mathbf{I} - \frac{\Psi}{1+r}\right)^{-1},
\end{aligned}
\tag{16}
$$

where $\small \mathbf{I}$ is the $\small 2\times2$ identity matrix, and the last equality uses the 
matrix analogue of the scalar geometric series.

Substituting (16) into (15) gives the VAR-based prediction of the current account
(eq. 45 in the original):

$$
\small 
\begin{aligned}
\widehat{CA}_t &= -\begin{bmatrix} 1 & 0 \end{bmatrix}
\left(\frac{1}{1+r}\Psi\right)
\left(\mathbf{I} - \frac{1}{1+r}\Psi\right)^{-1}
\begin{bmatrix} \Delta Z_t \\ CA_t \end{bmatrix} \\
&\equiv \begin{bmatrix} \Phi_{\Delta Z} & \Phi_{CA} \end{bmatrix}
\begin{bmatrix} \Delta Z_t \\ CA_t \end{bmatrix},
\end{aligned}
\tag{17}
$$

where $\small \begin{bmatrix} \Phi_{\Delta Z} & \Phi_{CA} \end{bmatrix}$ collects the entire 
matrix expression into a single row vector of reduced-form coefficients.

Equation (17) expresses the model's predicted current account, $\small \widehat{CA}_t$, 
as a function of the currently observable variables $\small \Delta Z_t$ and $\small CA_t$. It converts the infinite-horizon forecast in eq. (12) into a quantity that can be computed directly from current data, making the model's 
forward-looking prediction empirically testable. If consumers behave according to the consumption-smoothing hypothesis, the actual current account, $\small CA_t$, should match the model's prediction, $\small \widehat{CA}_t$, allowing researchers to test the model by checking if the row vector $\small \begin{bmatrix} \Phi_{\Delta Z} & \Phi_{CA} \end{bmatrix}$ statistically equals $\small \begin{bmatrix} 0 & 1 \end{bmatrix}$.

### 3. Empirical analysis

Having derived the model's key theoretical predictions in Section 2, I now turn to 
testing them empirically for Russia. This section proceeds in three parts. 
Section 3.1 describes the data used, their sources, and the transformations 
required for the model. Section 3.2 presents the estimated 
VAR in net output changes and the current account. Section 3.3 uses these 
estimates to construct the model-implied predicted current account, $\widehat{CA}_t$, 
and formally tests the model using a Wald test.

#### 3.1 Data

For testing the model, I constructed quarterly time-series spanning 1995Q2–2025Q1 for the change in net output, $\small \Delta Z_t$, and the  current account, $\small CA_t$, both expressed in real, seasonally adjusted, per-capita, 
demeaned terms.

The following four data sources are used:

- National accounts (nominal and real GDP and its components — government consumption 
  and gross capital formation) are obtained from [Rosstat (Federal State 
  Statistics Service), *National Accounts*](https://rosstat.gov.ru/statistics/accounts), covering 1995Q1–2026Q1. 
- Current account data, in millions of US dollars, are obtained from the 
  [Central Bank of Russia, *External Sector Statistics*](https://www.cbr.ru/statistics/macro_itm/external_sector/pb/), covering 1994Q1–2026Q1.
- Exchange rate data (RUB per USD, average of daily rates) are obtained from 
  the [OECD via FRED](https://fred.stlouisfed.org/series/CCUSMA02RUQ618N), and are used to convert the current 
  account into rubles.
- Population data (annual estimates as of January 1, with 2002 and 2010 
  reported as of census dates in October) are obtained from [Rosstat, *Demography*](https://rosstat.gov.ru/folder/12781), 
  covering 1995–2025.

To construct the real net output series, I use Rosstat's constant-price 
series for GDP, government consumption expenditure, and gross capital formation. 
Since Rosstat periodically rebases these series to a new base year (2003, 2008, 
2011, 2016, and 2021 prices), with each vintage covering a different, overlapping 
window, I splice the vintages into one continuous series in 2021 prices. I anchor 
on the most recent (2021-price) vintage and extend it backward to 1995 using the 
period-on-period growth rates, since growth rates computed within a single vintage 
remain valid even though price levels are different. The resulting real series for GDP, 
government spending, and investment are seasonally adjusted. Net output is defined as $\small Z_t \equiv Y_t - G_t - I_t$, and its 
first difference, $\small \Delta Z_t$, is computed from the seasonally adjusted 
real series.

To construct the real current account series, the current account, originally reported 
in millions of US dollars, is converted to rubles using the quarterly average 
RUB/USD exchange rate. The nominal ruble series is then deflated using the 
implicit price index $\small P_t$, computed as the ratio of nominal to real GDP.
The series is then seasonally adjusted. It is worth noting that RUB/USD exchange rate 
used to convert the current account to rubles is volatily and may introduce noise into the real current account.

Both $\small \Delta Z_t$ and $\small CA_t$ are divided by population to obtain per-capita terms. 
As Rosstat's population series is reported annually, it is interpolated to quarterly frequency 
by linear interpolation.

Finally, both per-capita series are expressed as deviations from their respective 
sample means.

<div align="center">
<img src="/assets/images/figures/fig_real_gdp.png" width="700">
<p>Figure 1. Real, seasonally adjusted GDP, government spending, and investment (billion RUB, 2021 prices)</p>
</div>
<br>

<div align="center">
<img src="/assets/images/figures/fig_net_output.png" width="700">
<p>Figure 2. Net output and net output changes (billion RUB, 2021 prices)<p>
</div>
<br>

<div align="center">
<img src="/assets/images/figures/fig_ca.png" width="700">
<p>Figure 3. Real current account (billion RUB, 2021 prices)<p>
</div>
<br>

<div align="center">
<img src="/assets/images/figures/fig_per_capita.png" width="700">
<p>Figure 4. Per-capita raw vs demeaned net output change and current account <p>
</div>
<br>

<div align="center">
Table 1. Descriptive statistics for net output, change in net output, and the current account

|                                |   N |     Mean |   Std. Dev. |     Min |     Max |
|:-------------------------------|----:|---------:|------------:|--------:|--------:|
| Z_t (billion RUB, real, SA)    | 121 | 13724.3  |     5258.75 | 3540.7  | 21423.2 |
| ΔZ_t (thousand RUB per capita) | 120 |     0.95 |        7.68 |  -17.48 |    23   |
| CA_t (thousand RUB per capita) | 121 |     9.82 |        6.88 |   -6.92 |    32   |

</div>

##### 3.1.1 Stationarity check. The Augmented Dickey-Fuller (ADF) test
Before estimating the VAR, I test $\small \Delta Z_t$ and $CA_t$ for stationarity using 
the Augmented Dickey-Fuller (ADF) test. The ADF test's null hypothesis is that a 
series contains a unit root, i.e. the series has no fixed mean to revert to, and the alternative that it 
is stationary. $\small \Delta Z_t$ strongly rejects the null at the 5% level 
(ADF = -6.02, $\small p<0.001$). $CA_t$ shows weaker evidence against a unit root 
(ADF = -2.80, $\small p=0.058$): the null is not rejected at the 5% level, though it is 
rejected at the 10% level. Consequetly, 
$CA_t$'s VAR estimates should be interpreted with some caution regarding the 
underlying stationarity assumption.

#### 3.2 VAR estimation

Following the specification in eq. (13), I estimate VAR(1) in $\small \Delta Z_t$ and $CA_t$, using their real, per-capita, 
seasonally adjusted, and demeaned counterparts constructed in Section 3.1. Since 
both series are expressed as deviations from their sample means, the VAR is 
estimated without a constant term. The system is estimated by ordinary least squares (OLS)
using Python's `statsmodels` package. The resulting coefficient matrix, 
$\small \hat\Psi = \begin{bmatrix}\hat\psi_{11} & \hat\psi_{12}\\ \hat\psi_{21} & 
\hat\psi_{22}\end{bmatrix}$, is reported in Table 2 below. Descriptive statistics and model fit summary are given in Tables 3 and 4, respectively.


<div align="center">
Table 2. Estimated VAR(1) coefficients

|          | ΔZ_t             | CA_t             |
|:---------|:-----------------|:-----------------|
| ΔZ_{t-1} | -0.197** (0.090) | 0.044 (0.050)    |
| CA_{t-1} | -0.228** (0.099) | 0.808*** (0.055) |

<small>Notes: Standard errors in parentheses. Estimated by OLS, no constant. 
N = 119. *** p<0.01, ** p<0.05, * p<0.10. </small>
</div>

<br>

<div align="center">
<img src="/assets/images/figures/fig_var_fitted.png" width="700">
<p>Figure 5. Actual vs VAR(1)-fitted net output change and current account <p>
</div>
<br>

<div align="center">
Table 3. Descriptive statistics for VAR coefficients

| Equation   | Regressor   |   Coefficient |   Std. Error |   t-stat |   p-value |
|:-----------|:------------|--------------:|-------------:|---------:|----------:|
| ΔZ_t       | ΔZ_{t-1}    |       -0.1975 |       0.0904 |  -2.1849 |    0.0289 |
| ΔZ_t       | CA_{t-1}    |       -0.2282 |       0.0991 |  -2.3022 |    0.0213 |
| CA_t       | ΔZ_{t-1}    |        0.0445 |       0.0501 |   0.8869 |    0.3751 |
| CA_t       | CA_{t-1}    |        0.8084 |       0.055  |  14.6976 |    0      |

</div>

<br>
<div align="center">
Table 4. Modle fit summary

|      |     R² |   Std. Dev. of Residuals |
|:-----|-------:|-------------------------:|
| ΔZ_t | 0.0747 |                   7.4307 |
| CA_t | 0.6487 |                   4.1226 |

</div>

Figure 5 plots actual versus VAR(1)-fitted values for both equations. 
The fitted values for $\Delta Z_t$ poorly captur the actual series and especially miss 
its sharpest swings, consistent with the equation's low R² of 0.075. The bottom 
panel shows a much closer correspondence between actual and fitted $CA_t$ 
throughout the sample, consistent with its higher R² of 0.649.

Overall, the VAR(1) estimates indicate that the current account is highly 
persistent and reasonably well explained by its own lag and, to a lesser extent, 
by lagged net output changes, while net output changes themselves are largely 
unpredictable from either variable's one-quarter-lagged history. Higher order VAR estimates produce better estimates but 
their use requires a more generalized version of model-predicted current account equation (17). 

#### 3.3. Predicted current account

Using the estimated VAR coefficient matrix $\small \hat\Psi$, I construct the model's 
predicted current account, $\small \widehat{CA}_t$, following eq. (17). Setting the discount rate to $r = 0.01$ per quarter, I 
compute the implied reduced-form coefficients $\small \hat\Phi_{\Delta Z}$ and 
$\small \hat\Phi_{CA}$ from $\small \hat\Psi$ and construct the fitted series as $\small \widehat{CA}_t = \hat\Phi_{\Delta Z}\Delta Z_t + \hat\Phi_{CA}CA_t$. Standard errors for $\small \hat\Phi_{\Delta Z}$ and $\hat\Phi_{CA}$ 
are obtained via the delta method, since both are nonlinear functions of the 
estimated VAR coefficients $\small \hat\Psi$. I then test the model's implied joint 
restriction, $\small H_0: \Phi_{\Delta Z} = 0,\ \Phi_{CA} = 1$, using a Wald test. 

The computed implied coefficients are reported in Table 5. $\hat\Phi_{\Delta Z}$ 
is estimated at 0.197 with a relatively small standard error (0.066), placing it 
notably above its predicted value of zero with reasonable precision. 
$\hat\Phi_{CA}$ is estimated at 0.909 — close to its predicted value of one — but 
with a much larger standard error (0.417), reflecting substantial uncertainty in 
this estimate.

<div align="center">
Table 5. Implied coefficients

|      |   Estimate |   Std. Error |   H0 value |
|:-----|-----------:|-------------:|-----------:|
| Φ_ΔZ |     0.197  |       0.066  |          0 |
| Φ_CA |     0.9092 |       0.4165 |          1 |

</div>

<br>
<div align="center">
<img src="/assets/images/figures/fig_final.png" width="700">
<p> Figure 6. Actual and model-predicted current account <p>
</div>

Figure 6 shows that the model-predicted current account tracks the actual series 
closely in both timing and magniture throughout the sample. 

#### 3.4 Wald test

The Wald test evaluates whether a set of parameter restrictions is consistent 
with the data, using the estimated parameters and their covariance matrix. For a 
parameter vector $\small \hat\theta$ and a hypothesized restriction $\small H_0: g(\theta) = 0$, 
the Wald statistic is

$$
\small
W = g(\hat\theta)' \left[\widehat{\mathrm{Var}}(g(\hat\theta))\right]^{-1} g(\hat\theta),
$$

which is asymptotically distributed $\small \chi^2$ with degrees of freedom equal to the 
number of restrictions tested. $W$ measures how far the estimates 
deviate from the hypothesized values, scaled by how precisely those estimates 
were obtained.

In this emprirical study, $\small g(\Psi) = \begin{bmatrix}\Phi_{\Delta Z}\\ \Phi_{CA}-1
\end{bmatrix}$, a nonlinear function of the VAR coefficients $\Psi$. 
Since $\small \hat\Phi_{\Delta Z}$ and $\small \hat\Phi_{CA}$ are derived from $\hat\Psi$, 
their covariance matrix is obtained using the delta method. If $\Phi = f(\Psi)$ for some differentiable 
function $f$, then

$$
\small 
\widehat{\mathrm{Var}}(\hat\Phi) \approx J \, \widehat{\mathrm{Var}}(\hat\Psi) \, J',
$$

where $J = \partial f/\partial \Psi$ is the Jacobian of $f$ evaluated at 
$\hat\Psi$, computed numerically here, and $\widehat{\mathrm{Var}}(\hat\Psi)$ is 
the covariance matrix of the estimated VAR coefficients.

To formally assess whether the deviations of $\hat\Phi_{\Delta Z}$ and 
$\hat\Phi_{CA}$ from their theoretical values are jointly significant, I test 
$H_0: \Phi_{\Delta Z}=0,\ \Phi_{CA}=1$ using this Wald statistic, with 2 degrees 
of freedom corresponding to the two restrictions being tested jointly. The 
results are reported in Table 6.

<div align="center">
Table 6. Wald test results

|                           |   Statistic |   Degrees of Freedom |   p-value |
|:--------------------------|------------:|---------------------:|----------:|
| Wald Test: Φ_ΔZ=0, Φ_CA=1 |      9.2827 |                    2 |    0.0096 |

</div>

The Wald statistic of 9.28 ($p < 0.01$) leads to a rejection of the null 
hypothesis. This indicates that the current account does not move exactly as the 
stochastic intertemporal current account model predicts. This finding is 
consistent with the broader empirical literature testing this model, which has 
frequently rejected the same restriction in applications to other countries. This 
result may reflect features of the Russian economy not captured by the baseline 
model such as dependence on oil and gas exports, periods of restricted access to 
international capital markets, and the structural breaks associated with the 
1998, 2008–09, 2014–15, and 2022 episodes.

### 4. Conclusion

Estimating a VAR(1) in net output changes and the current account, I 
found that the current account is highly persistent and reasonably well explained 
by its own lag, while net output changes are very noisy and largely 
unpredictable from either variable's history, at least in lag order of one quarter. 
The resulting model-predicted current account tracked the actual series closely in 
both timing and magnitude 
throughout most of the sample. Formally, a Wald test of the model's implied 
restriction, $\small \Phi_{\Delta Z}=0$ and $\Phi_{CA}=1$, was rejected 
($W=9.28$, $p<0.01$), indicating that the pure consumption-smoothing hypothesis 
does not hold exactly for Russia over this period, although the implied 
coefficients — particularly $\hat\Phi_{CA}=0.91$ — lie considerably closer to 
their theoretical values.

This rejection is expected considering many simplifying assumptions of the model such as a 
constant real interest rate, unconstrained access to borrowing and lending, and no 
role for oil price shocks, capital account restrictions, or exchange rate regime 
changes. The results suggest that the consumption-smoothing mechanism only partially captures 
the dynamics of Russia's current account.

<div style="page-break-after: always;"></div>

### References

Campbell, J. Y. (1987). Does saving anticipate declining labor income? An 
alternative test of the permanent income hypothesis. *Econometrica*, 55(6), 
1249–1273.

Obstfeld, M., & Rogoff, K. (1996). *Foundations of International Macroeconomics*. 
Cambridge, MA: MIT Press.

### Data Sources

Federal State Statistics Service of the Russian Federation (Rosstat). *GDP by Quarter, Expenditure Approach, since 1995*.National Accounts. Retrieved from https://rosstat.gov.ru/statistics/accounts

Federal State Statistics Service of the Russian Federation (Rosstat). *Population 
Size*. Demography. Retrieved fromhttps://rosstat.gov.ru/folder/12781

Central Bank of the Russian Federation. *Balance of Payments of the Russian Federation (Standard Components)*. Retrieved from https://www.cbr.ru/statistics/macro_itm/external_sector/pb/

Organization for Economic Co-operation and Development, Currency Conversions: *US Dollar Exchange Rate: Average of Daily Rates: National Currency: USD for Russia* [CCUSMA02RUQ618N], retrieved from FRED, Federal Reserve Bank of St. Louis; https://fred.stlouisfed.org/series/CCUSMA02RUQ618N, July 27, 2026.
