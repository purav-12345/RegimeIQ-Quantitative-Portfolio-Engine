# Research Notes – Notebook 05
## Portfolio Optimization

---

## Objective

The objective of this notebook was to convert the Hidden Markov Model (HMM) regime predictions into actionable investment decisions using Modern Portfolio Theory (MPT). Rather than constructing a single static portfolio using the entire historical dataset, the optimization process was performed separately within each hidden market regime. This enables the portfolio allocation to adapt dynamically to changing market environments.

---

## Research Questions

The notebook addressed the following questions:

- How can the statistical properties of each hidden regime be transformed into investment decisions?
- Why should expected returns and covariance matrices be estimated separately for different market regimes?
- How can Markowitz Mean-Variance Optimization be integrated with Hidden Markov Models?
- Do different market regimes naturally produce different optimal portfolio allocations?

---

## Methodology

The portfolio optimization framework followed these major steps:

1. Selected investable assets:
   - SPY (Equities)
   - TLT (Long-Term Treasury Bonds)
   - GLD (Gold)

2. Used HMM regime labels obtained in Notebook 04.

3. Divided historical return observations according to hidden market regimes.

4. Estimated regime-specific:
   - Expected return vectors (μ)
   - Covariance matrices (Σ)

5. Formulated a long-only Mean-Variance Optimization problem.

6. Maximized the portfolio Sharpe Ratio using numerical optimization (Sequential Least Squares Programming - SLSQP).

7. Generated one optimal portfolio for each hidden market regime.

---

## Portfolio Optimization Assumptions

The optimization was performed under the following assumptions:

- Fully invested portfolio
- Sum of portfolio weights equals one
- Long-only allocation
- No leverage
- No short selling
- Daily risk-free rate assumed to be zero

---

## Mathematical Framework

The optimization objective was to maximize the portfolio Sharpe Ratio:

- Portfolio Expected Return:
  - wᵀμ

- Portfolio Variance:
  - wᵀΣw

- Portfolio Volatility:
  - √(wᵀΣw)

- Sharpe Ratio:
  - (Portfolio Return − Risk Free Rate) / Portfolio Volatility

Since SciPy minimizes objective functions, the negative Sharpe Ratio was minimized.

---

## Statistical Estimation

For every hidden regime:

### Estimated Expected Returns

The sample mean of daily returns was calculated separately for:

- SPY
- TLT
- GLD

This produced one expected return vector for each hidden regime.

---

### Estimated Covariance Matrix

The sample covariance matrix was estimated separately for each regime using only observations belonging to that regime.

This allowed portfolio risk to reflect regime-dependent market dynamics rather than long-run averages.

---

## Optimization Results

Five independent optimization problems were solved.

Each hidden regime produced a unique portfolio allocation.

Observed allocations showed clear differences between market environments.

Examples included:

- Growth-oriented portfolios dominated by SPY
- Defensive portfolios dominated by TLT
- Gold acting primarily as a diversification asset
- Crisis regimes allocating almost entirely away from equities

---

## Portfolio Statistics

For every optimized portfolio, the following statistics were computed:

- Expected Portfolio Return
- Portfolio Volatility
- Portfolio Sharpe Ratio

These statistics were used to compare the quality of optimized portfolios across market regimes.

---

## Key Observations

Several important findings emerged:

- Portfolio allocations changed significantly across hidden regimes.
- Defensive regimes naturally shifted capital toward Treasury Bonds and Gold.
- Stable market regimes allocated heavily toward equities.
- Gold generally served as a diversification asset rather than the primary investment.
- The optimizer selected economically meaningful allocations without any manually defined market rules.

---

## Research Validation

Several validation checks were performed:

- Optimization convergence confirmed.
- Portfolio weights summed to one.
- No negative portfolio weights.
- Covariance matrices were symmetric.
- Portfolio allocations were consistent with economic interpretations obtained in Notebook 04.

---

## Limitations

The optimization assumes:

- Historical return distributions remain representative within each regime.
- Transaction costs are ignored.
- Rebalancing costs are ignored.
- Portfolio optimization is based solely on historical statistical estimates.

These assumptions will be relaxed and evaluated during backtesting.

---

## Conclusion

This notebook successfully connected machine learning with portfolio construction.

The Hidden Markov Model provided market-state identification, while Markowitz optimization transformed those states into regime-specific investment strategies.

The resulting framework produced five adaptive portfolios instead of a single static allocation, forming the core decision engine of the Regime Shift project.

---

## Transition to Notebook 06

Notebook 05 answered the question:

> "Given the current market regime, what portfolio should we hold?"

The next notebook addresses the practical question:

> "If these regime-specific portfolios had been implemented historically, how would the strategy have performed relative to traditional investment approaches?"

Notebook 06 therefore focuses on historical backtesting, performance evaluation, and empirical validation of the complete regime-aware tactical asset allocation framework.
