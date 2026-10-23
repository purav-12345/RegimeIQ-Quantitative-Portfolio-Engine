# Module 1
# Market Regimes and Data Preparation

---

# Learning Objectives

After completing this module, the reader should be able to:

- Explain why financial markets are non-stationary.
- Understand why log returns are preferred over prices.
- Explain volatility clustering and fat tails.
- Understand why hidden market regimes exist.
- Justify the use of Hidden Markov Models for regime detection.
- Prepare financial time series for statistical modelling.

---

# 1. The Motivation Behind the Project

Traditional portfolio allocation strategies such as the 60/40 portfolio assume that financial markets behave similarly through time. Historical evidence suggests otherwise.

Markets evolve through different macroeconomic environments.

Examples include:

- Bull Markets
- Bear Markets
- Financial Crises
- Recoveries
- Inflationary Periods

Each environment exhibits different statistical behaviour.

Therefore, a single static allocation cannot remain optimal forever.

Our project attempts to automatically detect these hidden market environments and dynamically allocate capital according to the inferred regime.

---

# 2. Why Prices Are Not Modelled Directly

Raw prices exhibit strong trends through time.

For example,

SPY has generally increased over the last twenty years.

This violates one of the key assumptions of many statistical models:

Stationarity.

Instead of prices, quantitative finance models daily returns.

Even better,

we use logarithmic returns.

---

# 3. Log Returns

For two consecutive prices

P_t

and

P_(t-1)

the logarithmic return is

r_t = ln(P_t / P_(t-1))

---

## Advantages

### Time Additivity

Multi-period returns are simply the sum of individual log returns.

This property greatly simplifies statistical modelling.

---

### Scale Invariance

A $10 increase does not have the same meaning for a $20 stock and a $500 stock.

Log returns remove this problem.

---

### Better Statistical Behaviour

Returns are considerably closer to stationarity than prices.

This makes them appropriate inputs for Hidden Markov Models.

---

# 4. Distribution of Financial Returns

Financial returns are not Normally distributed.

Empirical observations reveal

- Fat tails
- Skewness
- Extreme events

This implies

large market crashes occur significantly more frequently than predicted by a Gaussian distribution.

---

# Kurtosis

Kurtosis measures tail heaviness.

Large kurtosis indicates

higher probability of extreme market events.

This is one reason why Gaussian assumptions often fail during crises.

---

# 5. Volatility Clustering

Financial volatility is persistent.

Periods of high volatility tend to be followed by more high volatility.

Periods of calm markets are usually followed by continued calm.

This phenomenon is called

Volatility Clustering.

It violates the IID assumption.

---

# Why Does Volatility Cluster?

Economic shocks unfold over weeks or months.

Examples include

- Financial crises
- Pandemics
- Monetary policy shocks
- Banking stress

Therefore market uncertainty is persistent.

---

# 6. Dynamic Correlations

Asset relationships are not constant.

During calm periods

Stocks and Bonds may exhibit low correlation.

During crises

their relationships often change dramatically.

Therefore

a single covariance matrix cannot adequately describe financial markets.

---

# 7. Stationarity

Many classical statistical models assume

Constant Mean

Constant Variance

Constant Covariance

Financial markets violate these assumptions.

Although returns are approximately stationary,

their volatility and correlations evolve continuously.

---

# 8. Market Regimes

A market regime represents a hidden macroeconomic environment that generates the observable behaviour of financial assets.

Examples include

- Bull Market
- Bear Market
- Crisis
- Recovery

Importantly,

these regimes cannot be directly observed.

Only their consequences can be observed.

Observable variables include

- Returns
- Volatility
- VIX
- Bond Prices
- Gold Prices

---

# 9. Hidden Markov Models

The Hidden Markov Model assumes

there exists a hidden sequence of states

which generate the observed financial variables.

The HMM attempts to infer

those hidden states

using observed market behaviour.

Importantly,

the model does not know

Bull

Bear

or

Crisis.

It simply learns

State 0

State 1

State 2

Researchers later interpret these statistically distinct states economically.

---

# 10. Why HMM Instead of Threshold Rules?

Threshold rules such as

Return > 0

↓

Bull Market

are arbitrary.

Financial markets are multidimensional.

The same return may occur under very different volatility environments.

Hidden Markov Models infer regimes probabilistically using multiple features simultaneously.

---

# 11. Why Not Use GARCH Alone?

GARCH models

time-varying volatility.

However,

our objective is

dynamic asset allocation.

Portfolio allocation requires

economically interpretable market regimes.

HMM provides hidden state probabilities that naturally drive allocation decisions.

---

# Key Research Insights

Financial markets are

- Non-IID
- Non-stationary
- Regime-dependent
- Sequential

These empirical observations provide the scientific justification for Hidden Markov Models.

---

# Feynman Summary

Market regimes cannot be directly observed.

Instead,

they leave statistical fingerprints in financial variables such as returns, volatility, correlations and investor sentiment.

Feature engineering attempts to capture these fingerprints.

The Hidden Markov Model then reconstructs the hidden economic environment from these observable signals.

---

# Module Summary

Notebook 1 established the research motivation for the entire project.

Rather than immediately fitting machine learning models,

we first demonstrated empirically that financial markets violate the assumptions of many classical statistical models.

This naturally motivates the use of probabilistic latent-state models such as Hidden Markov Models.
