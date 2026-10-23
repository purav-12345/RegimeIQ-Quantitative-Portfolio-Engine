# Notebook 06 — Backtesting

## Objective

The objective of this notebook was to evaluate the real-world performance of the regime-aware portfolio allocation strategy developed in previous notebooks. Unlike theoretical portfolio optimization, this notebook focused on realistic implementation by incorporating walk-forward execution, transaction costs, and institutional benchmarking.

---

# Research Questions

- Does the regime-aware strategy outperform traditional static portfolios?
- Does the strategy remain profitable after transaction costs?
- Can Hidden Markov Model regime detection improve long-term risk-adjusted returns?
- Does the strategy avoid excessive portfolio turnover?
- How does the strategy compare against institutional benchmark portfolios?

---

# Methodology

The backtesting framework followed a realistic investment workflow.

Daily process:

1. Observe previous day's market regime.
2. Apply one-day lag to eliminate look-ahead bias.
3. Select the optimal portfolio corresponding to the detected regime.
4. Compute daily portfolio return.
5. Calculate portfolio turnover.
6. Apply transaction cost penalty.
7. Update portfolio value.

---

# Transaction Cost Model

Portfolio turnover was calculated as

Turnover = Σ |Current Weight − Previous Weight|

Transaction cost:

5 basis points (0.05%) per unit turnover

Daily Cost = Turnover × 0.0005

Portfolio returns were reduced by transaction costs before computing cumulative performance.

---

# Look-Ahead Bias Correction

Originally, the strategy used today's detected regime to allocate today's portfolio.

This introduces future information into the backtest.

The issue was corrected by shifting regime predictions forward by one trading day.

Decision timeline:

Day t

↓

Observe market

↓

Detect regime

↓

Trade on Day t+1

↓

Receive Day t+1 return

This modification makes the backtest temporally correct and suitable for research.

---

# Portfolio Turnover Analysis

Results:

- Average Turnover: 2.09%
- Rebalance Days: 123
- Percentage of Trading Days Rebalanced: 2.32%

Interpretation:

The Hidden Markov Model produced persistent market regimes.

As a result, portfolio allocations changed infrequently, leading to low transaction costs and reduced portfolio thrashing.

---

# Equity Curve

The cumulative portfolio value was constructed by compounding daily strategy returns after transaction costs.

The strategy demonstrated:

- Long-term capital appreciation
- Controlled drawdowns
- Consistent outperformance over benchmark portfolios

---

# Benchmark Portfolios

Three benchmark strategies were constructed.

1. Buy & Hold SPY
2. Equal Weight Portfolio
   - SPY (33.3%)
   - TLT (33.3%)
   - GLD (33.3%)

3. Traditional 60/40 Portfolio
   - SPY (60%)
   - TLT (40%)

All benchmarks were evaluated using the identical sample period and performance methodology.

---

# Performance Metrics

The following institutional performance metrics were computed.

- Total Return
- CAGR
- Annual Return
- Annual Volatility
- Sharpe Ratio
- Sortino Ratio
- Maximum Drawdown
- Calmar Ratio

---

# Final Results

## Regime Strategy

Total Return:
1217.20%

CAGR:
13.01%

Annual Volatility:
13.09%

Sharpe Ratio:
1.00

Sortino Ratio:
1.27

Maximum Drawdown:
-27.30%

Calmar Ratio:
0.48

---

# Benchmark Comparison

The regime-aware strategy outperformed all benchmark portfolios.

Compared to Buy & Hold SPY:

- Higher CAGR
- Lower volatility
- Higher Sharpe Ratio
- Higher Sortino Ratio
- Significantly lower maximum drawdown

Compared to Equal Weight:

- Higher return
- Higher Sharpe Ratio
- Better Calmar Ratio

Compared to Traditional 60/40:

- Higher return
- Higher risk-adjusted performance
- Better downside protection

---

# Key Findings

The Hidden Markov Model successfully identified persistent market regimes.

Dynamic allocation allowed capital to migrate between equities, bonds, and gold depending on prevailing market conditions.

The strategy achieved superior long-term performance while maintaining relatively low portfolio turnover.

Transaction costs had limited impact due to infrequent rebalancing.

Removing look-ahead bias ensured the backtest remained economically realistic.

Overall, the regime-aware strategy demonstrated superior risk-adjusted performance compared to traditional static allocation methods.

---

# Research Conclusion

Notebook 06 validated the practical usefulness of Hidden Markov Model regime detection for dynamic asset allocation.

The strategy produced higher returns, better risk-adjusted performance, lower drawdowns than Buy & Hold SPY, and remained implementable due to extremely low trading frequency.

This notebook established that machine learning-based regime detection can improve portfolio management without requiring excessive trading or unrealistic assumptions.

---

# Transition to Notebook 07

Notebook 06 answered:

"Did the strategy work?"

Notebook 07 investigates:

"Why did the strategy work?"

The focus shifts from performance measurement to performance attribution, robustness analysis, regime contribution analysis, and statistical validation.