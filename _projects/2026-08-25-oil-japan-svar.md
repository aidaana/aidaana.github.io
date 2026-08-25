---
title: "Pass-through analysis of oil price and exchnage rate shocks to Japanese prices through Choleski ordering of SVAR"
subtitle: ""
layout: post
category: data-analysis
---

<style>
  html {
    scroll-padding-top: 140px !important;
    scroll-behavior: smooth; /* Optional: adds a smooth transition effect */
  }
  /* Automatically add an empty line gap below all paragraphs */
  p { 
    margin-bottom: 25px !important; 
  }
  
  /* Automatically add an empty line gap below all markdown tables */
  table { 
    display: table !important;           /* Overrides theme structural box locks */
    max-width: 75% !important;           /* Adjusts target size layout footprint */
    margin-left: auto !important;        /* Computes centered alignment blocks */
    margin-right: auto !important;       /* Computes centered alignment blocks */
    margin-bottom: 35px !important;      /* Keeps the empty line gap below the table */
    font-size: 0.9em !important;
  }
  
   /* Unbolds the top row headers */
  table th {
    font-weight: normal !important;      /* Changes text from bold to standard weight */
  }
  
  /* Automatically add spacing above and below section headers */
  h3, h4, h5 { 
    margin-top: 40px !important;
    margin-bottom: 20px !important; 
  }
</style>

<script>MathJax = { tex: { tags: 'ams', inlineMath: [['$', '$'], ['\\(', '\\)']] }};</script><script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script><script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

<div style="margin-top: 15px; margin-bottom: 30px;">
  <a href="https://github.com/aidaana/present-value-current-account.git" target="_blank" style="display: inline-flex; align-items: center; gap: 6px; padding: 5px 12px; border: 1px solid light-dark(#ccc, #444); border-radius: 4px; color: light-dark(#333, #ccc); font-size: 0.85em; text-decoration: none; background: transparent; font-weight: 500;">
    📁 Code & Data on GitHub →
  </a>
</div>

#### Table of Contents

- [1. Introduction](#1-introduction)
- [2. Theoretical framework](#2-theoretical-framework)
  - [2.1 Structural VAR and identification problem](#21-structural-var-and-identification-problem)
  - [2.2 Cholesky ordering](#22-cholesky-ordering)
  - [2.3 Impulse response functions and pass-through rates](#23-impulse-response-functions-and-pass-through-rates)
- [3. Methodology](#3-methodology)
  - [3.1 Data](#31-data)
  - [3.2 Model](#32-model)
  - [3.3 Estimation](#33-estimation)
  - [3.4 Comparison accross periods](#34-comparison-accross-periods)
- [4. Results](#4-results)
  - [4.1 Baseline estimation results (1987–2026)](#41-baseline-estimation-results-1987-2026)
  - [4.2 Oil, exchange rate, and monetary policy pass-through](#42-oil-exchange-rate-and-monetary-policy-pass-through)
  - [4.3 Pass-through: regime comparison](#44-pass-through-regime-comparison)
- [5. Conclusion](#5-conclusion)
- [References](#references)
- [Data sources](#data-sources)
- [Appendices](#appendices)


### 1. Introduction

The dramatic developments in oil supply since the start of the war in the Middle East in February 2026, drew a lot of public attention to the oil prices and their implications for the broader economy, including inflation, growth slowdown, and exchnage rates. For Japan, which imports almost all of its energy consumption, the question of the extent of impact of oil prices on import prices and domestic inflation is of great importance. Coupled with it, unprecedented yen depreciation in the last several years calls for understanding the effects and pass-through of exchange rate changes onto domestic prices. 

In this study, I use Cholesky ordering of the SVAR model to identify structural shocks (oil price shocks and exchange rate shocks) and the responses of import prices of crude oil and Japan's headline CPI to these shocks and to estimate magnitude and speed of pass-through rates along the presented chain of variables. I conduct the analysis on the full sample spanning 1987 through 2026. In order to find whether there have been any structural breaks in economics effects and pass-through rates, I conduct the analysis on three different periods the sample, roughly corresponding to domestic monetayr policy regimes: a pre-ZIRP period (May 1987 – January 1999), a ZIRP/deflation period (February 1999 – March 2013, spanning the near-zero interest rate era preceding quantitative and qualitative easing), and a QQE-to-normalization period (April 2013 – July 2026).

This report finds that transmission from oil prices and the exchange rate to Japan's import costs is strong and fast, but transmission into consumer prices is much weaker and varies substantially across monetary-policy regimes. Since the introduction of QQE, the FX and monetary-policy channels have become more important for CPI, while the direct oil-to-CPI channel has weakened.

This report is structured as follows. In Section 2, I present theoretial framework concerning SVAR model, identification strategies, impulse response functions. In Section 3, I specify the model, present the data and stationarity transformations, and econometrics methods. Finally in Section 4, I present results of VAR estimation and pass-through analysis obtained from impulse response functions through Cholesky ordering. 

### 2. Theoretical framework

One of the main goals of this report is to estimate how shocks to the price of crude oil and to the yen-dollar exchange rate propagate through Japan's import prices of crude petroleum and CPI. Because we need to isolate the causal response of each variable to a real shock, the structural vector autoregression (SVAR) framework, developed by Sims (1980) and widely applied in the oil-macroeconomy literature (e.g., Kilian, 2009), will be used for this purpose. In this section, I present some theoretical background on SVAR models, identification problem and Cholesky decomposition, impulse response functions to obtain information on pass-through rates.

The notation and derivation in this section largely follow Enders, W. (2015). *Applied Econometric Time Series* (4th ed.), Chapter 5: "Multiequation Time-Series Models," extended here to a general $k$-variable, $p$-lag case.

#### 2.1 Structural VAR and identification problem

The structural VAR of order p lets each variable be affected by contemporaneous values of other variables, $p$ lags of all variables, and a structural shock, which we assume to be uncorrelated with other shocks. Here we consider a system of five endogenous variables, $y_{1,t}, y_{2,t}, y_{3,t}, y_{4,t}, y_{5,t}$:

$$
\begin{aligned}
y_{1,t} &= b_{10} - b_{12}y_{2,t} - b_{13}y_{3,t} - b_{14}y_{4,t} - b_{15}y_{5,t} + \sum_{i=1}^{p}\big(\gamma^{(i)}_{11}y_{1,t-i} + \gamma^{(i)}_{12}y_{2,t-i} + \gamma^{(i)}_{13}y_{3,t-i} + \gamma^{(i)}_{14}y_{4,t-i} + \gamma^{(i)}_{15}y_{5,t-i}\big) + \varepsilon_{1,t} \\[6pt]
y_{2,t} &= b_{20} - b_{21}y_{1,t} - b_{23}y_{3,t} - b_{24}y_{4,t} - b_{25}y_{5,t} + \sum_{i=1}^{p}\big(\gamma^{(i)}_{21}y_{1,t-i} + \gamma^{(i)}_{22}y_{2,t-i} + \gamma^{(i)}_{23}y_{3,t-i} + \gamma^{(i)}_{24}y_{4,t-i} + \gamma^{(i)}_{25}y_{5,t-i}\big) + \varepsilon_{2,t} \\[6pt]
&\ \ \vdots \\[6pt]
y_{5,t} &= b_{50} - b_{51}y_{1,t} - b_{52}y_{2,t} - b_{53}y_{3,t} - b_{54}y_{4,t} + \sum_{i=1}^{p}\big(\gamma^{(i)}_{51}y_{1,t-i} + \gamma^{(i)}_{52}y_{2,t-i} + \gamma^{(i)}_{53}y_{3,t-i} + \gamma^{(i)}_{54}y_{4,t-i} + \gamma^{(i)}_{55}y_{5,t-i}\big) + \varepsilon_{5,t}
\end{aligned}
\tag{1}
$$

We can succinctly represent this system in the following way:

$$
B\,x_t = \Gamma_0 + \Gamma_1 x_{t-1} + \Gamma_2 x_{t-2} + \cdots + \Gamma_p x_{t-p} + \varepsilon_t
\tag{2}
$$

where

$$
B = \begin{bmatrix}
1 & b_{12} & b_{13} & b_{14} & b_{15} \\
b_{21} & 1 & b_{23} & b_{24} & b_{25} \\
b_{31} & b_{32} & 1 & b_{34} & b_{35} \\
b_{41} & b_{42} & b_{43} & 1 & b_{45} \\
b_{51} & b_{52} & b_{53} & b_{54} & 1
\end{bmatrix}, \qquad
x_t = \begin{bmatrix} y_{1,t} \\ y_{2,t} \\ y_{3,t} \\ y_{4,t} \\ y_{5,t} \end{bmatrix}, \qquad
\Gamma_0 = \begin{bmatrix} b_{10} \\ b_{20} \\ b_{30} \\ b_{40} \\ b_{50} \end{bmatrix}, \qquad
\varepsilon_t = \begin{bmatrix} \varepsilon_{1,t} \\ \varepsilon_{2,t} \\ \varepsilon_{3,t} \\ \varepsilon_{4,t} \\ \varepsilon_{5,t} \end{bmatrix}
$$

and each $\Gamma_i$ ($i=1,\ldots,p$) is a $5\times5$ matrix of lag-$i$ coefficients.

Equation (2) is the structural VAR because the off-diagonal elements of matrix B let the variables be contemporaneosly affected by other variables.

Pre-multiplying (2) by $B^{-1}$ leads to the reduced-form VAR:

$$
x_t = A_0 + A_1 x_{t-1} + A_2 x_{t-2} + \cdots + A_p x_{t-p} + u_t
\tag{3}
$$

where

$$
A_0 = B^{-1}\Gamma_0, \qquad A_i = B^{-1}\Gamma_i \ \ (i=1,\ldots,p),
$$

and most importantly 

$$
\qquad u_t = B^{-1}\varepsilon_t
\tag{4}
$$

Relationship (3) can be estimated directly from the data by ordinary least squares, with $A_0$ the vector of intercepts, each $A_i$ a $5\times5$ matrix of reduced-form coefficients, and $u_t$ the vector of reduced-form residuals.

Each residual in $u_t$ is a composite of all five structural/economical shocks $\varepsilon_t$: $u_t = B^{-1}\varepsilon_t$, or in matrix form:

$$
\begin{bmatrix} u_{1,t} \\ u_{2,t} \\ u_{3,t} \\ u_{4,t} \\ u_{5,t} \end{bmatrix} = B^{-1}
\begin{bmatrix} \varepsilon_{1,t} \\ \varepsilon_{2,t} \\ \varepsilon_{3,t} \\ \varepsilon_{4,t} \\ \varepsilon_{5,t} \end{bmatrix}
$$

Therefore, reduced-form residuals are usually correlated with each other. Because the structural model (1) allows variables to affect each other within the same period, any shock that hits one variable immediately spills over into the other, so that residuals in each equation end up being correlated with each other. Therefore, variance-covariance matrix of residuals:

$$
\Sigma_u = \text{Var}(u_t) = \text{Var}(B^{-1}\varepsilon_t) = B^{-1}\Sigma_\varepsilon (B^{-1})'
$$


is generally not diagonal. For the 5-variable system, assuming the second moments of $u_t$ are time-independent and using the notation $\sigma_i^2 = \text{Var}(u_{it})$ and $\sigma_{ij} = \text{Cov}(u_{it}, u_{jt})$, vriance-covariance matrix is:

$$
\Sigma_u =
\begin{bmatrix}
\sigma_1^2 & \sigma_{12} & \sigma_{13} & \sigma_{14} & \sigma_{15} \\
\sigma_{21} & \sigma_2^2 & \sigma_{23} & \sigma_{24} & \sigma_{25} \\
\sigma_{31} & \sigma_{32} & \sigma_3^2 & \sigma_{34} & \sigma_{35} \\
\sigma_{41} & \sigma_{42} & \sigma_{43} & \sigma_4^2 & \sigma_{45} \\
\sigma_{51} & \sigma_{52} & \sigma_{53} & \sigma_{54} & \sigma_5^2
\end{bmatrix}
$$

We can obtain consistent estimates of of $A_0, A_1, \ldots, A_p$, the residuals $u_t$ and their variance-covariance matrix $\Sigma_u$ by applying OLS to the reduced-form VAR, $x_t = A_0 + A_1 x_{t-1} + \cdots + A_p x_{t-p} + u_t$. However, if our goal is to recover the structural shocks $\varepsilon_t$ from the observed $u_t$ in order to estimate the response of each variable to a well-defined, economically meaningful shock, we need to recover $B^{-1}$. But it cannot be recovered from the data alone because the system (1) is under-identified. To see why, we can compare the number of unknown and known parameters.

$\Sigma_u$, a $k \times k$ matrix, contains only $\frac{k(k+1)}{2}$ unique elements ($k$ variances on the diagonal annd $\binom{k}{2} = \frac{k(k-1)}{2}$ unique covariances off the diagonal). The unknown parameters are the off-diagonal elements of $B$, $k(k-1)$ of them, plus the $k$ variances of the structural shocks (the diagonal of $\Sigma_\varepsilon$, left unrestricted). This gives a total of $k(k-1) + k = k^2$ unknown parameters. Therefore, the number of unidentified parameters are:

$$
\text{unknowns} - \text{knowns} = k^2 - \frac{k(k+1)}{2} = \frac{k(k-1)}{2}
$$

For $k=5$ variables, 15 of the 25 parameters can be estimated from the data, leaving 10 parameters under-identified. To resolve it, $\frac{k(k-1)}{2}$ independent restrictions must be imposed on $B$, typically motivated by economic or real-world assumptions. The SVAR literature offers different identification strategies, each of which depends on the assumptions made by the researcher:

- Short-run restrictions approach formalized by Sims (1980) assumes that certain variables do not respond contemporaneously to shocks in certain other variables, but they may be affected with a lag. It is commonly implemented via a recursive (Cholesky) ordering.

- Long-run restrictions following Blanchard and Quah (1989), instead restrict the cumulative, or long-horizon effect of a shock. 

- Sign restrictions (Faust, 1998; Uhlig, 2005) require only that the sign of certain impulse responses match theoretical or usual real-world responses over some horizon. 

- External-instrument (proxy) identification (Stock and Watson, 2012) identifies a structural shock using an outside variable correlated with the shock of interest but uncorrelated with the other shocks.

There are many empirical studies that use recursive structure to trace the pass-through of global and macroeconomic shocks into domestic prices. In a foundational paper, McCarthy (2007) established a Cholesky-based VAR framework to analyze how supply, demand, and exchange rate shocks propagate sequentially through a domestic pricing chain (import prices, producer prices, and consumer prices). Ito and Sato (2008) utilized a structural VAR with a Cholesky decomposition to examine the pass-through effects of oil price shocks and exchange rate fluctuations on domestic prices in East Asian economies. Similarly, Kilian (2009) has relied on recursive ordering. For Japan specifically, Fukunaga, Hirakata, and Sudo (2011) apply Kilian-style oil shock decompositions to the Japanese economy, while Shioji (2012, 2014, 2015) documents the time-varying nature of exchange rate pass-through into Japanese prices. 

This report's five-variable ordering (oil price, long-term government bond yield, exchange rate, crude petroleum import price, CPI) follows the same recursive logic as this literature, treating the global oil price as contemporaneously exogenous to the Japanese variables, the long-term yield as reflecting the monetary policy stance ahead of the exchange rate it helps drive, and the exchange rate as prior to its transmission through import prices into CPI.

#### 2.2 Cholesky ordering

The Cholesky (recursive) identification strategy imposes the required number of restrictions by setting the $\frac{k(k-1)}{2}$ elements above (or below) the diagonal of $B^{-1}$ to zero, which imposes the causal ordering assumption to our system. Specificially, it assumes that variable 1 may affect variables 2, 3, 4, and 5 contemporaneously, but is not contemporaneously affected by any of them; variable 2 may affect variables 3, 4, and 5 contemporaneously, but not variable 1, and so on.

Rewriting (4), the relationship between the reduced-form residuals and the structural shocks is:

$$
u_t = P\,\varepsilon_t, \qquad \varepsilon_t \sim (0, I_5)
\tag{5}
$$

where $P$ is a $5\times5$ matrix satisfying $\Sigma_u = PP'$. The Cholesky decomposition of the positive-definite matrix $\Sigma_u$ constructs $P$ as the lower-triangular matrix satisfying this factorization:

$$
P = \begin{bmatrix}
p_{11} & 0 & 0 & 0 & 0 \\
p_{21} & p_{22} & 0 & 0 & 0 \\
p_{31} & p_{32} & p_{33} & 0 & 0 \\
p_{41} & p_{42} & p_{43} & p_{44} & 0 \\
p_{51} & p_{52} & p_{53} & p_{54} & p_{55}
\end{bmatrix}
$$

The relationships between structural shocks and reduced-form residuals become:

$$
\begin{aligned}
u_{1,t} &= p_{11}\,\varepsilon_{1,t} \\
u_{2,t} &= p_{21}\,\varepsilon_{1,t} + p_{22}\,\varepsilon_{2,t} \\
u_{3,t} &= p_{31}\,\varepsilon_{1,t} + p_{32}\,\varepsilon_{2,t} + p_{33}\,\varepsilon_{3,t} \\
u_{4,t} &= p_{41}\,\varepsilon_{1,t} + p_{42}\,\varepsilon_{2,t} + p_{43}\,\varepsilon_{3,t} + p_{44}\,\varepsilon_{4,t} \\
u_{5,t} &= p_{51}\,\varepsilon_{1,t} + p_{52}\,\varepsilon_{2,t} + p_{53}\,\varepsilon_{3,t} + p_{54}\,\varepsilon_{4,t} + p_{55}\,\varepsilon_{5,t}
\end{aligned}
$$

Here, the assumption is that $u_{1,t}$ is driven purely by $\varepsilon_{1,t}$ (not affected contemporaneously by $\varepsilon_{2,t}, \varepsilon_{3,t}, \varepsilon_{4,t}, \varepsilon_{5,t}$); $u_{2,t}$ is contemporaneousle affected by on $\varepsilon_{1,t}$ and $\varepsilon_{2,t}$ but not by $\varepsilon_{3,t}$, $\varepsilon_{4,t}$, or $\varepsilon_{5,t}$; and so on.

Once $P$ is obtained (via Cholesky factorization of the estimated $\hat\Sigma_u$), the structural shocks are recovered by inverting the relationship:

$$
\varepsilon_t = P^{-1} u_t
$$

Because $P$ is lower-triangular, this inversion can be calculated recursively, solving forward from the first equation: $\varepsilon_{1,t} = u_{1,t}/p_{11}$, then substituting into the second equation to solve for $\varepsilon_{2,t}$, and so on.

The variable placed first in the ordering is assumed contemporaneously exogenous to the rest of the system — its shock affects everything else within the period, but nothing else affects it within the period (it may still be affected with a one-period lag, through the $A_i$ matrices). The variable placed last is assumed contemporaneously endogenous — its residual absorbs the contemporaneous influence of every other shock in the system.
```

#### 2.3 Impulse response functions and pass-through rates

Having recovered the structural shocks $\varepsilon_t$ via the Cholesky decomposition of $\Sigma_u$, the next step is to study the propagation of each shock since our goal is to isolate how much of a change in oil prices or exchange rates gets transmitted to domestic prices (e.g., import prices of oil, PPI, CPI). We can use the moving average (MA) representation of the VAR, from which we can obtain the impulse response functions (IRFs).

If the reduced-form VAR system (3), $x_t = A_0 + A_1 x_{t-1} + \cdots + A_p x_{t-p} + u_t$, is stationary, it can be inverted into an infinite moving-average representation, expressing $x_t$ as a function of current and past reduced-form residuals:

$$
x_t = \mu + \sum_{i=0}^{\infty} \Phi_i\, u_{t-i}
\tag{6}
$$

where $\mu$ is the unconditional mean of $x_t$ and each $\Phi_i$ is a $4\times4$ matrix of moving-average coefficients, computed recursively from $A_1, \ldots, A_p$ (with $\Phi_0 = I_4$). Each element $\phi_{jk}(i)$ of $\Phi_i$ measures the effect of a one-unit innovation in the residual $u_{k}$, occurring $i$ periods ago, on the current value of variable $j$, holding all other reduced-form residuals fixed. 

However, we need to express (6) in terms of the structural shocks $\varepsilon_t$ rather than the reduced-form residuals $u_t$, since $u_t$ mixes the four structural shocks together. Substituting $u_t = P\varepsilon_t$ from (5):

$$
x_t = \mu + \sum_{i=0}^{\infty} \Phi_i P\, \varepsilon_{t-i} = \mu + \sum_{i=0}^{\infty} \Theta_i\, \varepsilon_{t-i}, \qquad \Theta_i \equiv \Phi_i P
\tag{7}
$$

This is the orthogonalized (structural) moving-average representation.

Each element $\theta_{jk}(i)$ of $\Theta_i$ can be interpreted as the effect, $i$ periods after the shock, of a one-unit innovation in structural shock $\varepsilon_{k}$ on variable $j$. The elements of $\Theta_0 = P$ are the impact multipliers (instantaneous effect of each structural shock on each variable). Fixing the shock variable $k$, $IRF_j(i) \equiv \theta_{jk}(i)$ is the response of variable $j$, at horizon $i$, to the (implicitly fixed) shock $k$.

For the five-variable system used in this study, the five sets of sequences $\{\theta_{jk}(i)\}_{i=0}^{\infty}$ for each of the $5\times5=25$ shock-response pairs constitute the impulse response functions. Plotting $\theta_{jk}(i)$ against $i$ is the standard way of visually summarizing the dynamic response of each variable to each structural shock.

The total, cumulative effect of a shock over $n$ periods is obtained by summing the impulse response coefficients:

$$
\sum_{i=0}^{n} \theta_{jk}(i)
$$

Letting $n \to \infty$ gives the total, long-run cumulated effect of shock $k$ on variable $j$.

##### Pass-through rates

Pass-through rates are defined as the ratio of the **cumulative response of the output variable** to the **cumulative response of the input variable**, both attributable to the same structural shock:

$$
PT_{jk}(h) = \frac{\sum_{i=0}^{h} \theta_{jk}(i)}{\sum_{i=0}^{h} \theta_{kk}(i)} = \frac{\sum_{i=0}^{h} IRF_{j}(i)}{\sum_{i=0}^{h} IRF_{k}(i)}
$$

This ratio represents the fraction of the total move in the upstream variable $k$ itself (the denominator) as a move in the downstream variable $j$ (the numerator), by horizon $h$. $PT_{jk}(h)$ can therefore be directly interpreted as an elasticity: the percentage change in variable $j$ per one-percent change in variable $k$, cumulated through horizon $h$. If oil rises by a cumulative 10% over $h$ months following its own shock, and CPI rises by a cumulative 0.3% over the same window as a consequence of that same shock, the pass-through rate is $0.3/10 = 0.03$, or 3% — meaning roughly 3% of the oil price move is ultimately reflected in consumer prices by horizon $h$.

### 3. Methodology

#### 3.1 Data

The benchmark five-model VAR model is estimated on monthly time series spanning May 1987 to July 2026 (471 observations), all log-differenced except bond yields series, whose first difference is used: the Brent crude oil price (USD per barrel), 10-year Japanese government bonds (JGB) yields, the nominal JPY/USD exchange rate, Japan's import price index for crude petroleum (yen basis), and Japan's headline CPI. All series are non-seasonally adjusted. Table 1 summarizes the raw data sources.

<div style="text-align: center;">Table 1. Data sources</div> 

| Variable | Notes | Source | Original sample Period |
| :--- | :---: | :---: | :---: | 
| Oil price (Brent) | Europe Brent Spot Price FOB (USD/barrel), monthly average | [U.S. Energy Information Administration (EIA)](https://www.eia.gov/dnav/pet/hist/LeafHandler.ashx?n=PET&s=RBRTE&f=M) | May 1987 – Jul 2026 |
| Japan's 10-year Government Bond Yields | Monthly average % | [Ministry of Finance, Japan](https://www.mof.go.jp/english/policy/jgbs/reference/interest_rate/index.htm) | Jul 1986 – Jul 2026 |
| Exchange rate (USD/JPY) | Nominal rate, monthly average of daily rates | [OECD via FRED](https://fred.stlouisfed.org/series/CCUSMA02JPM618N) | Jan 1957 – Jul 2026 |
| Crude petroleum import price index | Corporate Goods Price Index (2020 base), Import Price Index, yen basis, Crude petroleum (commodity) | [Bank of Japan (BOJ)](https://www.stat-search.boj.or.jp/index_en.html) | Jan 1980 – Jul 2026 |
| CPI, all items (headline CPI) | Monthly index (2020 base) | [Statistics Bureau of Japan](https://www.e-stat.go.jp/en/stat-search/files?page=1&toukei=00200573&tstat=000001150147&metadata=1&data=1) | Jan 1970 – Jul 2026 |

The common time period across these time-series is from June 1987 to July 2026, which I will use in the benchmark model.

To check the time series for non-stationarity, I use both the Augmented Dickey-Fuller (ADF) test to evaluate the null hypothesis of a unit root against a stationary alternative and  the Kwiatkowski-Phillips-Schmidt-Shin (KPSS) test to evaluate the null hypothesis of trend-stationarity. As expected, all raw series fail to reject the unit-root null under ADF and reject stationarity under KPSS (Table 2), motivating the use of log or first differences of the series.

<div style="text-align: center;">Table 2. Stationarity test results (levels) </div> 

| Series | ADF statistic | ADF p-value | ADF conclusion | KPSS statistic | KPSS p-value | KPSS conclusion |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| Oil price (Brent) | -2.19 | 0.21 | Non-stationary | 2.42 | 0.01 | Non-stationary |
| JGB 10-year yields | -1.76 | 0.401 | Non-stationary | 2.69 | 0.01 | Non-stationary |
| USD/JPY | -1.54 | 0.512 | Non-stationary | 0.5 | 0.042 | Non-stationary |
| Crude petroleum | -1.08 | 0.723 | Non-stationary | 2.7 | 0.01 | Non-stationary |
| CPI - Headline | -0.31 | 0.924 | Non-stationary | 2.17 | 0.01 | Non-stationary |

Table 3 reports ADF and KPSS test results after transforming each series: log-differences for Brent, the exchange rate, the crude petroleum import price index, and CPI, and a first difference for the JGB 10-year yield. For all five series, both tests are unambiguous: ADF strongly rejects the unit-root null (p < 0.02 in all cases) and KPSS fails to reject stationarity (p ≥ 0.08).

<div style="text-align: center;">Table 3. Stationarity test results (log/first differences)</div>

| Series | ADF statistic | ADF p-value | ADF conclusion | KPSS statistic | KPSS p-value | KPSS conclusion |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| Brent - log-diff | -12.2 | 0.0 | Stationary | 0.03 | 0.1 | Stationary |
| JGB 10-year yields - first-diff | -4.17 | 0.001 | Stationary | 0.27 | 0.1 | Stationary |
| USD/JPY - log-diff | -5.33 | 0.0 | Stationary | 0.24 | 0.1 | Stationary |
| Crude petroleum - log-diff | -13.59 | 0.0 | Stationary | 0.07 | 0.1 | Stationary |
| CPI - Headline - log-diff | -3.37 | 0.012 | Stationary | 0.38 | 0.084 | Stationary |

Figures 1-5 plot raw-level time series of the model's five variables.

<div align="center">
<img src="/assets/images/figures-oil/fig_brent.png" width="700">
<p> <p>
</div>

<div align="center">
<img src="/assets/images/figures-oil/fig_jgb.png" width="700">
<p> <p>
</div>

<div align="center">
<img src="/assets/images/figures-oil/fig_yen.png" width="700">
<p> <p>
</div>

<div align="center">
<img src="/assets/images/figures-oil/fig_crude_petroleum.png" width="700">
<p> <p>
</div>

<div align="center">
<img src="/assets/images/figures-oil//fig_cpi.png" width="800">
<p> <p>
</div>


#### 3.2 Model

The empirical analysis is based on a five-variable VAR estimated on monthly data. The vector of endogenous variables is

$$
x_t = \begin{bmatrix} \Delta\ln(\text{Brent}_t) \\ \Delta(\text{JGB}_t) \\ \Delta\ln(\text{Yen}_t) \\ \Delta\ln(\text{CrudePet}_t) \\ \Delta\ln(\text{CPI}_t) \end{bmatrix}
$$

where $\text{Brent}_t$ is the Brent crude oil spot price, $\text{JGB}_t$ is Japan's 10-year government bond yield, $\text{Yen}_t$ is the nominal JPY/USD exchange rate, $\text{CrudePet}_t$ is Japan's crude petroleum import price index (yen basis), and $\text{CPI}_t$ is Japan's headline consumer price index.

**Oil price benchmark.** Brent is chosen as the global benchmark price against which the majority of internationally traded crude oil is priced. 

**Monetary policy variable.** The JGB 10-year yield, rather than the Bank of Japan's overnight policy rate, is used to capture the monetary policy. The overnight policy rate's variation was minimal during a long period of the zero and negative interest rate era, leaving too little variance for a VAR estimation.

**Import price variable.** Crude petroleum commodity, which is part of "Petroleum, coal and natural gas" group in BOJ's classification, is chosen as Japan's price index most directly related to oil prices.

**Domestic price variable.** Headline CPI (which includes both energy and food) is used as the outcome variable of interest to assess the pass-through of oil and exchange rate shocks into the broad cost of living in Japan.

The reduced-form VAR takes the form

$$
x_t = A_0 + \sum_{i=1}^{p} A_i\, x_{t-i} + B\, d_t + u_t
$$

where $p$ is the lag order; $d_t$ is a vector of exogenous varianles consisitng of eleven monthly seasonal dummies and four consumption-tax-hike dummies, included to absorb seasonal effects and known fiscal policy interventions from the CPI equation; and $u_t$ is the vector of reduced-form residuals, with variance-covariance matrix $\Sigma_u$.

To generate structural shocks from $\Sigma_u$, we use its Cholesky decomposition. The relationship between the reduced-form VAR residuals ($u_t$) and the structural shocks ($\varepsilon_t$) can be written as follows:

$$
\begin{pmatrix}
u_t^{\text{oil}} \\
u_t^{\text{jgb}} \\
u_t^{\text{fx}} \\
u_t^{\text{imp}} \\
u_t^{p}
\end{pmatrix}
=
\begin{pmatrix}
p_{11} & 0 & 0 & 0 & 0 \\
p_{21} & p_{22} & 0 & 0 & 0 \\
p_{31} & p_{32} & p_{33} & 0 & 0 \\
p_{41} & p_{42} & p_{43} & p_{44} & 0 \\
p_{51} & p_{52} & p_{53} & p_{54} & p_{55}
\end{pmatrix}
\begin{pmatrix}
\varepsilon_t^{\text{oil}} \\
\varepsilon_t^{\text{jgb}} \\
\varepsilon_t^{\text{fx}} \\
\varepsilon_t^{\text{imp}} \\
\varepsilon_t^{p}
\end{pmatrix}
\tag{8}
$$

where $\varepsilon_t^{\text{oil}}$ denotes the oil price shock, 
$\varepsilon_t^{\text{jgb}}$ denotes the JGB yield shock, 
$\varepsilon_t^{\text{fx}}$ denotes the exchange rate shock, 
$\varepsilon_t^{\text{imp}}$ denotes the crude petroleum import price shock, 
and $\varepsilon_t^{p}$ denotes the CPI shock. The structural model is identified using a recursive Cholesky decomposition. For $k=5$ endogenous variables, $k(k-1)/2=10$ zero restrictions are imposed on the matrix $P$, thus making it possible to identify the contemporaneous structural relationships.

The Cholesky ordering — oil price, JGB yield, exchange rate, crude petroleum import price, CPI — follows the standard logic in the exchange rate pass-through literature: variables assumed more contemporaneously exogenous are placed earlier. The oil price is ordered first, as the world price of oil is not contemporaneously affected by Japan-specific developments. The JGB yield is ordered second, ahead of the exchange rate, consistent with exchange rates' sensitivity to interest-rate differentials. The crude petroleum import price index is ordered fourth, as the intermediate channel through which oil costs intereacting with exchnage rate first enter Japan's prices before reaching CPI. CPI is placed last as the most contemporaneously endogenous variable in the system.

#### 3.3 Estimation

**Lag selection.** The lag order $p$ is selected using standard information criteria — AIC, BIC, FPE, and HQIC — computed over a range of candidate lag lengths (up to 12 months).  A common lag order is applied across all sample windows compared in this study, so that any differences in estimated impulse responses reflect the underlying regime rather than differences in model specification.

For the five-variable system, BIC and HQIC both select a lag order of 1, while AIC and FPE select a lag order of 3 (Table [4]). A lag order of $p=3$ is adopted as the benchmark specification.

<div style="text-align: center;">Table 4. Lag order selection (5-variable system, 1987–2026)</div>

| Lag | AIC | BIC | FPE | HQIC |
| :---: | :---: | :---: | :---: | :---: |
| 0 | -32.20 | -32.15 | 1.037e-14 | -32.18 |
| 1 | -34.40 | -34.13* | 1.146e-15 | -34.30* |
| 2 | -34.48 | -33.98 | 1.066e-15 | -34.28 |
| 3 | -34.55* | -33.83 | 9.868e-16** | -34.27 |

*Note: * indicates the minimum (selected) value for each criterion. Full table spans lags 0–12; only lags 0–3 shown here for brevity.*

**Estimation.** The reduced-form VAR (equation 3) is estimated by ordinary least squares, augmented with exogenous monthly seasonal dummies and consumption-tax-hike dummies. Japan's non-seasonally-adjusted CPI is subject to a seasonal pattern as well as one-time level shifts around each of the country's four consumption tax hikes (April 1989, April 1997, April 2014, and October 2019). Eleven monthly dummies and four tax-hike-month dummies are therefore included as exogenous regressors.

OLS estimation of the reduced-form VAR is consistent and asymptotically efficient regardless of the identification strategy. The Cholesky decomposition of $\hat\Sigma_u$ is then applied to recover the structural shocks. Model adequacy is checked via the stability condition (all eigenvalues of the companion-form VAR lying inside the unit circle).

**Impulse response functions.** Once the structural shocks $\varepsilon_t$ are recovered, the orthogonalized moving-average representation $x_t = \mu + \sum_{i=0}^{\infty}\Theta_i\,\varepsilon_{t-i}$ traces out the dynamic effect of a one-unit structural shock in variable $k$ on variable $j$ at every horizon $i$ following the shock. Each element $\theta_{jk}(i)$ of $\Theta_i$ gives this response; plotting $\theta_{jk}(i)$ against $i$ for a given shock-response pair constitutes the impulse response function. Because $\Theta_i$ is a nonlinear function of the estimated VAR coefficients, closed-form standard errors are unavailable; confidence bands are instead obtained via Monte Carlo simulation, repeatedly resampling from the fitted model to build an empirical distribution of $\hat\Theta_i$ at each horizon:

**Pass-through rates.** While the raw impulse response $\theta_{jk}(i)$ is scaled to the shock variable's own one-standard-deviation innovation, pass-through rates express the *cumulative* impulse responses of the input and output variables as a ratio, normalizing out the shock's scale:

$$
PT_{jk}(h) = \frac{\sum_{i=0}^{h} \theta_{jk}(i)}{\sum_{i=0}^{h} \theta_{kk}(i)}
$$

where $\theta_{kk}(i)$ is the shock variable's own cumulative response to its own shock (the denominator). $PT_{jk}(h)$ is directly interpretable as an elasticity — the percentage change in variable $j$ per one-percent change in variable $k$, cumulated through horizon $h$:

#### 3.4 Comparison accross periods

To assess whether the amplification of oil and exchange rate pass-through into Japanese prices has changed alongside Japan's shift in monetary policy stance, the benchmark VAR is re-estimated separately over three sample windows roughly based on major BOJ policy regimes: a pre-ZIRP period (May 1987 – January 1999), a ZIRP/deflation period (February 1999 – March 2013, spanning the near-zero interest rate era preceding quantitative and qualitative easing), and a QQE-to-normalization period (April 2013 – July 2026). These boundaries are chosen because they correspond to identifiable, citable BOJ policy actions.

The same lag order and exogenous dummy specification are applied uniformly across all three windows, so that any differences in the resulting impulse responses and pass-through rates reflect the underlying economic regime rather than differences in model specification. For each window, the VAR is re-estimated, structural shocks are recovered via the Cholesky decomposition of the window-specific $\hat\Sigma_u$, and pass-through rates $PT_{jk}(h)$ are then computed from IRFs. The resulting pass-through rates — particularly for the oil-to-CPI, exchange-rate-to-CPI, and JGB-yield-to-CPI channels — are compared across the three regimes to assess whether pass-through magnitude, speed, or persistence has changed over these periods.

### 4. Results

First, I will present results for full sample (1987-2026): VAR estimation and pass-through rates. Then, I will proceed to comparing results obtained from splitting full sample into regime-specific windows: a pre-ZIRP period (May 1987 – January 1999), a ZIRP/deflation period (February 1999 – March 2013, spanning the near-zero interest rate era preceding quantitative and qualitative easing), and a QQE-to-normalization period (April 2013 – July 2026)

#### 4.1 Baseline estimation results (1987–2026)

The following are the main results and observations from estimating benchmark five-variable VAR (lag order 3, estimated on the full June 1987 – July 2026 sample, $n=470$).

**Own-variable persistence.** Each variable shows significant own-lag persistence at the first lag: Brent ($\hat\gamma=0.273$, $p<0.001$), the JGB yield ($\hat\gamma=0.270$, $p<0.001$), the exchange rate ($\hat\gamma=0.362$, $p<0.001$), and CPI ($\hat\gamma=0.165$, $p<0.001$). But both Brent and the JGB yield later show negative persistence — Brent's second lag ($\hat\gamma=-0.361$, $p=0.001$) and the JGB yield's third lag ($\hat\gamma=-0.225$, $p<0.001$) — indicating a partial reversal of the initial response (e.g. speculative demand cools down, or producers adjust supply, causing a price reversal). The crude petroleum import price index's persistence is an exception: its own first lag is not significant, consistent with its dynamics being driven almost entirely by contemporaneous and lagged oil price and exchange rate movements.

**Oil price and crude petroleum import price index.** The crude petroleum import price equation shows a strong, highly significant relationship with lagged Brent at every lag: $L1 = 0.731$ ($p<0.001$), $L2 = 0.204$ ($p<0.001$), $L3 = 0.215$ ($p<0.001$). The exchange rate also enters this equation strongly at the first lag ($\hat\gamma=0.505$, $p<0.001$), confirming that yen depreciation raises the yen-denominated cost of imported crude with a one-month lag.

**Effects on CPI.** In the CPI equation, both the first lag of the exchange rate ($\hat\gamma=0.0132$, $p=0.044$) and Brent ($\hat\gamma=0.0026$, $p=0.059$, marginal) enter in positive but small coefficient values. The crude petroleum import price index itself does not enter the CPI equation significantly at any lag, suggesting that oil imports constitute only a small part of the broad basket of goods and services tracked by CPI.

**Residual Correlation Structure**

The residual variance-covariance matrix $\hat\Sigma_u$ reveals the contemporaneous linkages that motivate the Cholesky ordering. The strongest off-diagonal relationship is between the exchange rate and the crude petroleum import price index (implied correlation $\approx 0.60$), consistent with the near-mechanical link between yen movements and the yen-denominated cost of imported crude oil within the same month. The JGB yield and the exchange rate also show a meaningful contemporaneous correlation ($\approx 0.17$), confirming bond yield movements and exchange rate movements co-move within the same period. Contemporaneous correlation between Brent price and crude petroleum import price is only 0.06, suggesting that immediate monthly unexpected shocks in global markets do not immediately show up in import price index due to shipment contracts that were alredy priced. CPI's residual correlations with the other variables are small, consistent with its role as the most contomporaneously endogenous, slow-moving variable in the system, whose response to shocks is expected to build up gradually over subsequent months rather than within the same period.


#### 4.2 Oil, exchange rate, and monetary policy pass-through

Table 5 reports cumulative pass-through rates at selected horizons, along with speed and convergence statistics, for the six shock-response pairs of central interest.

Oil, exchange rate, JGB yield, and crude petroleum shocks all show long-run pass-through rates into CPI on the order of 0.3–1.3%, consistent with CPI being a broad aggregate basket only modestly exposed to any single upstream cost shock. Among these, the exchange rate channel shows the largest long-run pass-through into CPI (1.31%), followed by oil (0.80%), crude petroleum import prices (0.84%), and the JGB yield (0.31%). Convergence is fast across all  pass-through channels: each reaches 90% of its long-run pass-through rate within 1–3 months.

Oil price's long-run pass-through into the crude petroleum import price index is near-complete at 93.6%. The exchange rate's long-run pass-through into the same variable is smaller, at 68.2%, indicating a meaningful but incomplete transmission of yen movements into yen-denominated import costs over the medium run — despite showing the strongest immediate, within-month pass-through. Both import-price channels show a transient overshoot before settling. Oil's pass-through into crude petroleum import prices peaks above 1 (1.07) at horizon 3, before settling toward its long-run value of 0.94. Similarly, the exchange rate's pass-through into import prices peaks at 1.10 at horizon 1 before declining substantially to its long-run value of 0.68 by horizon 6 and beyond, indicating that the immediate mechanical FX-to-import-price linkage is only partially sustained as the broader system adjusts over subsequent months.

These results indicate that Japan's crude petroleum import prices absorb oil and exchange rate shocks quickly and to a large degree (particularly oil, at close to full pass-through), while the transmission from there into the aggregate consumer price level is small in magnitude but converges rapidly. Whether this balance between channels — and in particular the relative importance of the exchange rate channel — has shifted across Japan's distinct monetary policy regimes is examined directly via the regime-specific comparison in the next section.

<div style="text-align: center;">Table 5. Pass-through rates over 1, 3, 6, 12, 24 months </div>

| Pass-through pair    |   Month_1 |   Month_3 |   Month_6 |   Month_12 |   Month_24 |Peak pass-through |   Peak_horizon |   Months_to_90pct|
|:---------------------|----------:|----------:|----------:|-----------:|-----------:|------------:|---------------:|------------------------:|
| Oil -> CPI           |    0.0047 |    0.0072 |    0.0087 |     0.008  |     0.008  |      0.009  |              5 |                       2 |     
| FX -> CPI            |    0.0097 |    0.0137 |    0.0129 |     0.0131 |     0.013  |      0.0137 |              3 |                       2 |        
| JGB10Y -> CPI        |    0.0006 |    0.0031 |    0.0032 |     0.0031 |     0.0031 |      0.0036 |              4 |                       3 |      
| CrudePet -> CPI      |    0.0097 |    0.0089 |    0.0089 |     0.0085 |     0.0084 |      0.0097 |              1 |                       1 |      
| Oil -> CrudePet      |    0.59   |    1.0721 |    0.9582 |     0.9417 |     0.9361 |      1.0721 |              3 |                       2 |   
| FX -> CrudePet       |    1.0961 |    0.872  |    0.6105 |     0.6826 |     0.6816 |      1.0961 |              1 |                       0 |  


#### 4.3 Pass-through: regime comparison

Table 6 reports cumulative pass-through rates and convergence statistics for the six channels of interest, estimated separately across the three monetary policy regimes, while Figures 6 and 7 plot those cumulative pass-through rates.

<div align="center">
<img src="/assets/images/figures-oil/fig_regime_pass_through_cpi.png" width="800">
<p> <p>
</div>

<div align="center">
<img src="/assets/images/figures-oil/fig_regime_pass_through_import_prices.png" width="800">
<p> <p>
</div>

**FX → CPI.** The long-run FX pass-through into CPI moves from −0.38% (Pre-ZIRP) to −0.38% (ZIRP/Deflation, effectively unchanged) to +1.95% (QQE-to-present) — a change in sign and an increase in magnitude relative to the two earlier regimes. Yen depreciation had a negligible-to-negative association with CPI prior to 2013, but has become a driver of an increase in consumer prices in the QQE-to-present era. Additionally, in QQE-to-present, FX → CPI peaks later (horizon 9 vs. horizon 0–1), illustrating a more gradual and larger transmission process in the recent regime.

**JGB10Y → CPI** channel also shows a similar increasing trend across regimes. Long-run pass-through rises from 0.2% (Pre-ZIRP) to 0.37% (ZIRP/Deflation) to 0.91% (QQE-to-present), and again with slower convergence in the most recent period (4 months to 90% of long-run effect, vs. 3 months previously).

**Oil → CPI**, by contrast, is weaker in the most recent regime. Long-run pass-through falls from 1.53% (Pre-ZIRP) to 1.16% (ZIRP/Deflation) to 0.64% (QQE-to-present). The oil-to-CPI channel has weakened, suggesting a diminished role of oil prices in Japan's domestic prices.

**ImportPrice → CPI** is comparatively stable, with a modest increase from Pre-ZIRP to ZIRP/Deflation followed by a slight decline in QQE-to-present (0.57% → 1.84% → 0.89%), not displaying a clear monotonic trend across the three regimes.

**Oil → Import Prices.** During the most recent window (period of QQE-to-normalization), pass-through rises from 0.66 at month 1 to a peak of 1.38 at month 3, before settling to 1.04 by month 24. The peak pass-through hits 1.38 at month 3, meaning short-term import prices react even stronger than a one-to-one proportion with Brent shocks. This pattern differs qualitatively from the two earlier regimes: Pre-ZIRP shows a more gradual build-up (0.28 → 0.84 → 0.98 across months 1, 3, 6) before declining to a lower long-run level (0.78), while ZIRP/Deflation shows the fastest initial convergence (0.75 at month 1, already close to its eventual 0.93 long-run value) with comparatively little overshoot. Read together, this indicates the pass-through of oil price shocks into crude oil import prices has become both stronger (higher long-run level: 0.78 → 0.93 → 1.04 across the three regimes) and more volatile in its adjustment path in the most recent regime.

**FX → CrudePet (import prices).** Import prices shows a sharp decline in long-run pass-through despite consistently strong immediate impact. All three regimes show near-full or overshooting pass-through at horizon 0–1 (PT ≈ 0.88–1.11), consistent with the mechanical relationship between yen movements and yen-denominated import costs. But the long-run value falls sharply from Pre-ZIRP (96%) to ZIRP/Deflation (25.8%) to a partial recovery in QQE-to-present (46.4%), indicating that the extent to which the initial pass-through is sustained over subsequent months has diminished substantially since the pre-ZIRP era, with some recovery evident in the most recent period.

<div style="text-align: center;">Table 6. Regime pass-through summary (ordered by pairs) </div>

| Pass-through pair        | regime                     |   Month_1 |   Month_3 |   Month_6 |   Month_12 |   Month_24 |   peak_PT |   peak_horizon |   months_to_90pct|   half_life_from_peak |
|:---------------------|:---------------------------|----------:|----------:|----------:|-----------:|-----------:|----------:|---------------:|------------------------:|----------------------:|
| Oil -> CPI          | Pre-ZIRP (1987-1999)       |    0.002  |    0.0087 |    0.0217 |     0.0133 |     0.0153 |    0.022  |              7 |                       5 |                   nan |
| Oil -> CPI          | ZIRP/Deflation (1999-2013) |    0.0058 |    0.0115 |    0.0122 |     0.0116 |     0.0116 |    0.0128 |              5 |                       3 |                   nan |
| Oil -> CPI          | QQE-to-present (2013-2026) |    0.0042 |    0.0071 |    0.0061 |     0.0064 |     0.0064 |    0.0071 |              3 |                       2 |                   nan |
| FX -> CPI           | Pre-ZIRP (1987-1999)       |   -0.0081 |   -0.0068 |   -0.0042 |    -0.0037 |    -0.0038 |   -0.0095 |              0 |                       0 |                     5 |
| FX -> CPI           | ZIRP/Deflation (1999-2013) |    0.0143 |    0.0075 |   -0.0032 |    -0.0034 |    -0.0038 |    0.0143 |              1 |                       7 |                     3 |
| FX -> CPI           | QQE-to-present (2013-2026) |    0.0083 |    0.0137 |    0.0182 |     0.0194 |     0.0195 |    0.0197 |              9 |                       6 |                   nan |
| JGB10Y -> CPI       | Pre-ZIRP (1987-1999)       |    0.0007 |    0.0018 |    0.0023 |     0.0018 |     0.002  |    0.0023 |              6 |                       3 |                   nan |
| JGB10Y -> CPI       | ZIRP/Deflation (1999-2013) |    0.0005 |    0.0036 |    0.0044 |     0.0037 |     0.0037 |    0.005  |              5 |                       3 |                   nan |
| JGB10Y -> CPI       | QQE-to-present (2013-2026) |    0.0035 |    0.0081 |    0.0091 |     0.0091 |     0.0091 |    0.0091 |             11 |                       4 |                   nan |
| Import Price -> CPI | Pre-ZIRP (1987-1999)       |    0.0076 |   -0.0042 |    0.0015 |    -0.0009 |    -0.0006 |   -0.0134 |              2 |                       2 |                     1 |
| Import Price -> CPI | ZIRP/Deflation (1999-2013) |    0.0131 |    0.0197 |    0.0186 |     0.0184 |     0.0184 |    0.0197 |              3 |                       2 |                   nan |
| Import Price -> CPI | QQE-to-present (2013-2026) |    0.016  |    0.0097 |    0.0099 |     0.009  |     0.0089 |    0.016  |              1 |                       0 |                   nan |
| Oil -> Import Price | Pre-ZIRP (1987-1999)       |    0.2788 |    0.8372 |    0.9779 |     0.7628 |     0.7792 |    0.9896 |              5 |                       3 |                   nan |
| Oil -> Import Price | ZIRP/Deflation (1999-2013) |    0.7536 |    0.9606 |    0.9602 |     0.9295 |     0.9275 |    1.0059 |              5 |                       2 |                   nan |
| Oil -> Import Price | QQE-to-present (2013-2026) |    0.6593 |    1.3761 |    1.0136 |     1.0577 |     1.0434 |    1.3761 |              3 |                       2 |                   nan |
| FX -> Import Price  | Pre-ZIRP (1987-1999)       |    0.8823 |    0.8837 |    0.9451 |     0.9468 |     0.9496 |    0.981  |              2 |                       1 |                   nan |
| FX -> Import Price  | ZIRP/Deflation (1999-2013) |    1.1091 |    0.8915 |    0.2623 |     0.2802 |     0.2583 |    1.1299 |              0 |                       0 |                     4 |
| FX -> Import Price  | QQE-to-present (2013-2026) |    1.0915 |    0.67   |    0.3492 |     0.4385 |     0.4641 |    1.2356 |              0 |                       0 |                     4 |

*Note: peak_PT indicates the maximum cumulaive pass-through observed, peak-horizon indicates the month when peak_PT was achieved, month_to-90_pct indicates how many months in took to reach 90% of the 24-month cumulative pass-through.

### 5. Conclusion

I started this mini econometrics project with little knowledge about structural VARs, Cholesky ordering, or ways to measure pass-through, and with vague idea about what my research question is or what it is that I'm looking for. The only thing I knew I wanted to do was to explore how global oil prices propagate through Japan's crude oil import prices and consumer price index. Later, AI brainstormed some potential concrete research questions. Having picked one, I turned into learning the methodology about SVARs, residuals vs structural shocks, identification strategy and some more details on implementation.

A five-variable structural VAR was estimated — consisting of the world oil price (Brent), Japan's 10-year government bond yield, the JPY/USD exchange rate, Japan's crude petroleum import price index, and headline CPI — identified via a recursive Cholesky ordering. The model was estimated on the full 1987–2026 sample and separately across three monetary policy regimes (Pre-ZIRP, ZIRP/Deflation, and QQE-to-present), from which impulse response functions and cumulative pass-through rates were computed for each shock-response pair of interest.

Next, I summarize the main findings of this report:

1. Oil and exchange-rate shocks pass through strongly to Japan's crude import prices, but much less to CPI. Oil shocks pass through almost one-for-one to crude import prices in the full sample (93.6%), while FX pass-through is about 68%. In contrast, the long-run effects on CPI are small: about **0.80% for oil, 1.31% for FX, 0.84% for crude import prices, and 0.31% for JGB yields. Most of the CPI response occurs within the first few months.

2. The transmission structure changes substantially throughout monetary-policy regimes. FX → CPI pass-through is essentially zero/negative before and during the ZIRP/deflation period (−0.38%) but rises to +1.95% under QQE. JGB → CPI also increases steadily, from 0.18% → 0.37% → 0.91%. Oil → CPI moves in the opposite direction, falling from 1.53% → 1.16% → 0.64%.

3. The FX → crude-import-price channel weakens in persistence despite remaining strong on impact. Initial FX pass-through is close to or above 100% in all regimes, but long-run pass-through falls from 92.9% pre-ZIRP to 25.8% during ZIRP/deflation, before recovering to 46.4% under QQE. Oil → crude-import-price pass-through strengthens, reaching 104.3% under QQE, with short-run overshooting.

### References

- Blanchard, O. J., and Quah, D. (1989). "The Dynamic Effects of Aggregate Demand and Supply Disturbances." *American Economic Review*, 79(4), 655–673.

- Enders, W. (2015). *Applied Econometric Time Series* (4th ed.). Wiley.

- Faust, J. (1998). "The Robustness of Identified VAR Conclusions about Money." *Carnegie-Rochester Conference Series on Public Policy*, 49, 207–244.

- Fukunaga, I., Hirakata, N., and Sudo, N. (2011). "The Effects of Oil Price Changes on the Industry-Level Production and Prices in the U.S. and Japan." In *Commodity Prices and Markets*, National Bureau of Economic Research, pp. 195–231.

- Ito, T., and Sato, K. (2008). "Exchange Rate Changes and Inflation in Post-Crisis Asian Economies: Vector Autoregression Analysis of the Exchange Rate Pass-Through." *Journal of Money, Credit and Banking*, 40(7), 1407–1438.

- Kilian, L. (2009). "Not All Oil Price Shocks Are Alike: Disentangling Demand and Supply Shocks in the Crude Oil Market." *American Economic Review*, 99(3), 1053–1069.

- McCarthy, J. (2007). "Pass-Through of Exchange Rates and Import Prices to Domestic Inflation in Some Industrialized Economies." *Eastern Economic Journal*, 33(4), 511–537.


- Shioji, E. (2012). "The Evolution of the Exchange Rate Pass-Through in Japan: A Re-evaluation Based on Time-Varying Parameter VARs." *Public Policy Review*, 8(1), 67–92.

- Shioji, E. (2014). "A Pass-Through Revival." *Asian Economic Policy Review*, 9(1), 120–138.

- Shioji, E. (2015). "Time Varying Pass-Through: Will the Yen Depreciation Help Japan Hit the Inflation Target?" *Journal of the Japanese and International Economies*, 37, 43–58.

- Sims, C. A. (1980). "Macroeconomics and Reality." *Econometrica*, 48(1), 1–48.

- Stock, J. H., and Watson, M. W. (2012). "Disentangling the Channels of the 2007–2009 Recession." *Brookings Papers on Economic Activity*, Spring 2012, 81–135.

- Uhlig, H. (2005). "What Are the Effects of Monetary Policy on Output? Results from an Agnostic Identification Procedure." *Journal of Monetary Economics*, 52(2), 381–419.

### Data sources

U.S. Energy Information Administration (EIA). *Europe Brent Spot Price FOB (Dollars per Barrel)*. Retrieved from https://www.eia.gov/dnav/pet/hist/LeafHandler.ashx?n=PET&s=RBRTE&f=M

Ministry of Finance, Japan. *Interest Rate Data — Japanese Government Bonds*. Retrieved from https://www.mof.go.jp/english/policy/jgbs/reference/interest_rate/index.htm

Organization for Economic Co-operation and Development, Currency Conversions: *US Dollar Exchange Rate: Average of Daily Rates: National Currency: USD for Japan* [CCUSMA02JPM618N], retrieved from FRED, Federal Reserve Bank of St. Louis; https://fred.stlouisfed.org/series/CCUSMA02JPM618N

Bank of Japan. *Corporate Goods Price Index (2020 Base), Import Price Index (Yen Basis)*. Time-Series Data Search. Retrieved from https://www.stat-search.boj.or.jp/index_en.html

Statistics Bureau of Japan. *Consumer Price Index (2020 Base)*. Retrieved from https://www.e-stat.go.jp/en/stat-search/files?page=1&toukei=00200573&tstat=000001150147&metadata=1&data=1

### Appendices

<div style="text-align: center;">Table A1. Full Sample, Lag 3 — Model Summary </div>

| Statistic | Value |
| :--- | :---: |
| No. of equations | 5 |
| Nobs | 467 |
| Lag order | 3 |
| Log-likelihood | 4921.60 |
| AIC | -34.6031 |
| BIC | -33.2269 |
| HQIC | -34.0615 |
| Stable (roots inside unit circle) | True |

<br>

<div style="text-align: center;">Table A2. Equation: Brent </div>

| Regressor | Coefficient | Std. Error | t-stat | p-value |
| :--- | :---: | :---: | :---: | :---: |
| const | 0.0117 | 0.0160 | 0.733 | 0.464 |
| month_2 | -0.0142 | 0.0227 | -0.626 | 0.531 |
| month_3 | 0.0003 | 0.0224 | 0.016 | 0.988 |
| month_4 | -0.0045 | 0.0226 | -0.202 | 0.840 |
| month_5 | 0.0244 | 0.0241 | 1.014 | 0.311 |
| month_6 | 0.0021 | 0.0236 | 0.090 | 0.929 |
| month_7 | 0.0066 | 0.0225 | 0.294 | 0.768 |
| month_8 | -0.0125 | 0.0217 | -0.574 | 0.566 |
| month_9 | 0.0014 | 0.0225 | 0.063 | 0.950 |
| month_10 | -0.0030 | 0.0238 | -0.125 | 0.901 |
| month_11 | -0.0291 | 0.0228 | -1.276 | 0.202 |
| month_12 | -0.0273 | 0.0227 | -1.205 | 0.228 |
| tax_hike_1989_04 | 0.0594 | 0.0959 | 0.619 | 0.536 |
| tax_hike_1997_04 | -0.0728 | 0.0957 | -0.761 | 0.447 |
| tax_hike_2014_04 | 0.0030 | 0.0951 | 0.032 | 0.974 |
| tax_hike_2019_10 | -0.0760 | 0.0957 | -0.795 | 0.427 |
| L1.brent_log_diff | **0.2731** | 0.0483 | 5.655 | 0.000 |
| L1.jgb_diff | 0.0483 | 0.0306 | 1.581 | 0.114 |
| L1.yen_log_diff | -0.3502 | 0.2328 | -1.504 | 0.133 |
| L1.crude_petroleum_log_diff | **0.3223** | 0.1417 | 2.274 | 0.023 |
| L1.headline_log_diff | -2.5891 | 1.5305 | -1.692 | 0.091 |
| L2.brent_log_diff | **-0.3608** | 0.1127 | -3.201 | 0.001 |
| L2.jgb_diff | 0.0208 | 0.0310 | 0.670 | 0.503 |
| L2.yen_log_diff | -0.0034 | 0.2439 | -0.014 | 0.989 |
| L2.crude_petroleum_log_diff | **-0.3040** | 0.1409 | -2.157 | 0.031 |
| L2.headline_log_diff | -2.3203 | 1.5501 | -1.497 | 0.134 |
| L3.brent_log_diff | 0.1595 | 0.1166 | 1.368 | 0.171 |
| L3.jgb_diff | -0.0074 | 0.0296 | -0.249 | 0.803 |
| L3.yen_log_diff | 0.0511 | 0.1950 | 0.262 | 0.793 |
| L3.crude_petroleum_log_diff | -0.0440 | 0.0627 | -0.702 | 0.483 |
| L3.headline_log_diff | -0.6032 | 1.5279 | -0.395 | 0.693 |

<br>

<div style="text-align: center;">Table A3. Equation: JGB10Y </div>

| Regressor | Coefficient | Std. Error | t-stat | p-value |
| :--- | :---: | :---: | :---: | :---: |
| const | 0.0147 | 0.0248 | 0.592 | 0.554 |
| month_2 | 0.0096 | 0.0352 | 0.273 | 0.785 |
| month_3 | -0.0333 | 0.0347 | -0.959 | 0.338 |
| month_4 | -0.0284 | 0.0350 | -0.811 | 0.417 |
| month_5 | -0.0128 | 0.0374 | -0.343 | 0.731 |
| month_6 | -0.0071 | 0.0367 | -0.195 | 0.846 |
| month_7 | -0.0134 | 0.0350 | -0.384 | 0.701 |
| month_8 | -0.0185 | 0.0336 | -0.550 | 0.582 |
| month_9 | -0.0450 | 0.0349 | -1.289 | 0.197 |
| month_10 | -0.0357 | 0.0370 | -0.965 | 0.335 |
| month_11 | -0.0520 | 0.0353 | -1.472 | 0.141 |
| month_12 | -0.0284 | 0.0352 | -0.808 | 0.419 |
| tax_hike_1989_04 | -0.0524 | 0.1488 | -0.352 | 0.725 |
| tax_hike_1997_04 | -0.0889 | 0.1483 | -0.600 | 0.549 |
| tax_hike_2014_04 | 0.0042 | 0.1474 | 0.029 | 0.977 |
| tax_hike_2019_10 | 0.0692 | 0.1484 | 0.466 | 0.641 |
| L1.brent_log_diff | 0.0479 | 0.0749 | 0.639 | 0.523 |
| L1.jgb_diff | **0.2699** | 0.0474 | 5.697 | 0.000 |
| L1.yen_log_diff | 0.5339 | 0.3611 | 1.479 | 0.139 |
| L1.crude_petroleum_log_diff | -0.2244 | 0.2198 | -1.021 | 0.307 |
| L1.headline_log_diff | 3.4242 | 2.3735 | 1.443 | 0.149 |
| L2.brent_log_diff | 0.1549 | 0.1748 | 0.886 | 0.376 |
| L2.jgb_diff | 0.0872 | 0.0480 | 1.815 | 0.070 |
| L2.yen_log_diff | -0.0964 | 0.3782 | -0.255 | 0.799 |
| L2.crude_petroleum_log_diff | -0.2472 | 0.2186 | -1.131 | 0.258 |
| L2.headline_log_diff | -1.2986 | 2.4040 | -0.540 | 0.589 |
| L3.brent_log_diff | 0.2889 | 0.1809 | 1.597 | 0.110 |
| L3.jgb_diff | **-0.2249** | 0.0460 | -4.894 | 0.000 |
| L3.yen_log_diff | 0.3422 | 0.3024 | 1.132 | 0.258 |
| L3.crude_petroleum_log_diff | -0.0638 | 0.0972 | -0.656 | 0.512 |
| L3.headline_log_diff | 2.0297 | 2.3695 | 0.857 | 0.392 |

<br>

<div style="text-align: center;">Table A4. Equation: Yen </div>

| Regressor | Coefficient | Std. Error | t-stat | p-value |
| :--- | :---: | :---: | :---: | :---: |
| const | 0.0019 | 0.0042 | 0.461 | 0.645 |
| month_2 | -0.0006 | 0.0059 | -0.095 | 0.925 |
| month_3 | -0.0001 | 0.0058 | -0.009 | 0.993 |
| month_4 | -0.0002 | 0.0059 | -0.033 | 0.974 |
| month_5 | -0.0029 | 0.0063 | -0.457 | 0.647 |
| month_6 | -0.0013 | 0.0062 | -0.208 | 0.835 |
| month_7 | -0.0030 | 0.0059 | -0.515 | 0.607 |
| month_8 | -0.0063 | 0.0057 | -1.108 | 0.268 |
| month_9 | -0.0019 | 0.0059 | -0.321 | 0.748 |
| month_10 | -0.0043 | 0.0062 | -0.695 | 0.487 |
| month_11 | 0.0005 | 0.0059 | 0.089 | 0.929 |
| month_12 | -0.0021 | 0.0059 | -0.357 | 0.721 |
| tax_hike_1989_04 | 0.0136 | 0.0250 | 0.542 | 0.588 |
| tax_hike_1997_04 | 0.0255 | 0.0249 | 1.024 | 0.306 |
| tax_hike_2014_04 | 0.0003 | 0.0248 | 0.014 | 0.989 |
| tax_hike_2019_10 | 0.0044 | 0.0249 | 0.175 | 0.861 |
| L1.brent_log_diff | 0.0020 | 0.0126 | 0.156 | 0.876 |
| L1.jgb_diff | **-0.0163** | 0.0080 | -2.051 | 0.040 |
| L1.yen_log_diff | **0.3624** | 0.0606 | 5.976 | 0.000 |
| L1.crude_petroleum_log_diff | -0.0423 | 0.0369 | -1.145 | 0.252 |
| L1.headline_log_diff | -0.4238 | 0.3986 | -1.063 | 0.288 |
| L2.brent_log_diff | 0.0358 | 0.0294 | 1.219 | 0.223 |
| L2.jgb_diff | 0.0064 | 0.0081 | 0.788 | 0.430 |
| L2.yen_log_diff | 0.0082 | 0.0635 | 0.129 | 0.898 |
| L2.crude_petroleum_log_diff | -0.0185 | 0.0367 | -0.503 | 0.615 |
| L2.headline_log_diff | 0.4767 | 0.4037 | 1.181 | 0.238 |
| L3.brent_log_diff | 0.0217 | 0.0304 | 0.716 | 0.474 |
| L3.jgb_diff | -0.0068 | 0.0077 | -0.885 | 0.376 |
| L3.yen_log_diff | 0.0078 | 0.0508 | 0.154 | 0.878 |
| L3.crude_petroleum_log_diff | -0.0124 | 0.0163 | -0.758 | 0.448 |
| L3.headline_log_diff | -0.1700 | 0.3979 | -0.427 | 0.669 |

<br>

<div style="text-align: center;">Table A5. Equation: CrudePet (import price index) </div>

| Regressor | Coefficient | Std. Error | t-stat | p-value |
| :--- | :---: | :---: | :---: | :---: |
| const | 0.0017 | 0.0066 | 0.256 | 0.798 |
| month_2 | -0.0012 | 0.0094 | -0.122 | 0.903 |
| month_3 | 0.0012 | 0.0093 | 0.128 | 0.898 |
| month_4 | -0.0006 | 0.0094 | -0.063 | 0.949 |
| month_5 | -0.0100 | 0.0100 | -1.001 | 0.317 |
| month_6 | 0.0021 | 0.0098 | 0.217 | 0.828 |
| month_7 | 0.0067 | 0.0094 | 0.712 | 0.476 |
| month_8 | -0.0099 | 0.0090 | -1.098 | 0.272 |
| month_9 | 0.0012 | 0.0094 | 0.127 | 0.899 |
| month_10 | -0.0023 | 0.0099 | -0.229 | 0.819 |
| month_11 | -0.0046 | 0.0095 | -0.481 | 0.631 |
| month_12 | -0.0016 | 0.0094 | -0.167 | 0.867 |
| tax_hike_1989_04 | -0.0125 | 0.0399 | -0.314 | 0.753 |
| tax_hike_1997_04 | 0.0429 | 0.0397 | 1.080 | 0.280 |
| tax_hike_2014_04 | 0.0002 | 0.0395 | 0.006 | 0.995 |
| tax_hike_2019_10 | -0.0018 | 0.0397 | -0.044 | 0.965 |
| L1.brent_log_diff | **0.7313** | 0.0201 | 36.446 | 0.000 |
| L1.jgb_diff | -0.0190 | 0.0127 | -1.498 | 0.134 |
| L1.yen_log_diff | **0.5054** | 0.0967 | 5.224 | 0.000 |
| L1.crude_petroleum_log_diff | -0.0340 | 0.0589 | -0.577 | 0.564 |
| L1.headline_log_diff | -0.0356 | 0.6360 | -0.056 | 0.955 |
| L2.brent_log_diff | **0.2038** | 0.0468 | 4.350 | 0.000 |
| L2.jgb_diff | -0.0004 | 0.0129 | -0.034 | 0.973 |
| L2.yen_log_diff | 0.0672 | 0.1013 | 0.663 | 0.507 |
| L2.crude_petroleum_log_diff | **-0.1702** | 0.0586 | -2.907 | 0.004 |
| L2.headline_log_diff | -0.0420 | 0.6441 | -0.065 | 0.948 |
| L3.brent_log_diff | **0.2154** | 0.0485 | 4.446 | 0.000 |
| L3.jgb_diff | 0.0053 | 0.0123 | 0.429 | 0.668 |
| L3.yen_log_diff | 0.0507 | 0.0810 | 0.626 | 0.531 |
| L3.crude_petroleum_log_diff | -0.0445 | 0.0260 | -1.708 | 0.088 |
| L3.headline_log_diff | 0.7068 | 0.6349 | 1.113 | 0.266 |

<br>

<div style="text-align: center;">Table A6. Equation: CPI (headline CPI) </div>

| Regressor | Coefficient | Std. Error | t-stat | p-value |
| :--- | :---: | :---: | :---: | :---: |
| const | -0.0001 | 0.0005 | -0.171 | 0.864 |
| month_2 | **-0.0016** | 0.0006 | -2.546 | 0.011 |
| month_3 | **0.0027** | 0.0006 | 4.231 | 0.000 |
| month_4 | **0.0023** | 0.0006 | 3.627 | 0.000 |
| month_5 | **0.0013** | 0.0007 | 1.974 | 0.048 |
| month_6 | **-0.0014** | 0.0007 | -2.088 | 0.037 |
| month_7 | -0.0010 | 0.0006 | -1.511 | 0.131 |
| month_8 | **0.0025** | 0.0006 | 4.063 | 0.000 |
| month_9 | **0.0022** | 0.0006 | 3.502 | 0.000 |
| month_10 | **0.0018** | 0.0007 | 2.740 | 0.006 |
| month_11 | **-0.0025** | 0.0006 | -3.960 | 0.000 |
| month_12 | 0.0001 | 0.0006 | 0.099 | 0.921 |
| tax_hike_1989_04 | **0.0135** | 0.0027 | 5.003 | 0.000 |
| tax_hike_1997_04 | **0.0177** | 0.0027 | 6.556 | 0.000 |
| tax_hike_2014_04 | **0.0182** | 0.0027 | 6.802 | 0.000 |
| tax_hike_2019_10 | 0.0014 | 0.0027 | 0.527 | 0.598 |
| L1.brent_log_diff | 0.0026 | 0.0014 | 1.888 | 0.059 |
| L1.jgb_diff | -0.0001 | 0.0009 | -0.076 | 0.939 |
| L1.yen_log_diff | **0.0132** | 0.0066 | 2.015 | 0.044 |
| L1.crude_petroleum_log_diff | 0.0024 | 0.0040 | 0.598 | 0.550 |
| L1.headline_log_diff | **0.1654** | 0.0431 | 3.838 | 0.000 |
| L2.brent_log_diff | -0.0002 | 0.0032 | -0.077 | 0.939 |
| L2.jgb_diff | **0.0024** | 0.0009 | 2.796 | 0.005 |
| L2.yen_log_diff | 0.0008 | 0.0069 | 0.117 | 0.907 |
| L2.crude_petroleum_log_diff | -0.0025 | 0.0040 | -0.629 | 0.530 |
| L2.headline_log_diff | -0.0454 | 0.0436 | -1.040 | 0.298 |
| L3.brent_log_diff | -0.0001 | 0.0033 | -0.043 | 0.966 |
| L3.jgb_diff | -0.0003 | 0.0008 | -0.354 | 0.724 |
| L3.yen_log_diff | -0.0021 | 0.0055 | -0.374 | 0.708 |
| L3.crude_petroleum_log_diff | 0.0021 | 0.0018 | 1.171 | 0.241 |
| L3.headline_log_diff | 0.0043 | 0.0430 | 0.100 | 0.921 |

<br>

<div style="text-align: center;">Table A7. Residual Variance-Covariance Matrix ($\Sigma_u$)</div>

| | Brent | JGB10Y | Yen | CrudePet | CPI |
| :--- | :---: | :---: | :---: | :---: | :---: |
| Brent | 0.008746 | 0.001388 | 0.000019 | 0.000242 | 0.000025 |
| JGB10Y | 0.001388 | 0.021035 | 0.000593 | 0.000270 | 0.000011 |
| Yen | 0.000019 | 0.000593 | 0.000593 | 0.000570 | -0.000001 |
| CrudePet | 0.000242 | 0.000270 | 0.000570 | 0.001510 | 0.000005 |
| CPI | 0.000025 | 0.000011 | -0.000001 | 0.000005 | 0.000007 |

<br>
