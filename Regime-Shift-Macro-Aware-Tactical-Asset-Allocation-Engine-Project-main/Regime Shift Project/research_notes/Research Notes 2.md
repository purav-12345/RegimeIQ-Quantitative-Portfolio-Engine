# Feature Engineering

## Objective

Construct a feature matrix that summarizes the observable characteristics of financial markets while preserving economically meaningful information about latent market regimes.

Rather than maximizing the number of variables, the objective is to engineer features that encode distinct dimensions of the market, including performance, risk, trend, cross-asset relationships, and investor sentiment.

The resulting feature matrix will serve as the observation sequence for the Hidden Markov Model.

## Rolling Volatility

Rolling volatility measures the variability of returns over a moving window and serves as a proxy for recent market uncertainty.

Unlike a single global estimate of volatility, rolling volatility adapts through time and captures the dynamic nature of financial markets.

### Why Rolling Windows?

Financial markets are non-stationary. A single estimate of volatility over the entire sample cannot describe changing market conditions. Rolling windows provide a time-varying estimate of risk.

### Window Lengths

- **20-day volatility** captures short-term market risk and responds quickly to new information.
- **63-day volatility** captures intermediate-term risk and filters out short-lived fluctuations.

The choice of window length determines the *memory* of the feature.

Short windows are more responsive but noisier.

Long windows are more stable but slower to react.

### Research Insight

Rolling volatility is not the market regime itself. It is an observable consequence of changes in the hidden economic environment.

Therefore, it serves as an informative input feature for Hidden Markov Models.

### Practical Limitation

If volatility features respond to every temporary market fluctuation, the resulting allocation strategy may suffer from excessive trading, increased turnover, and higher transaction costs.

Feature engineering should therefore balance responsiveness with robustness.

## Momentum

Momentum measures the cumulative price movement of an asset over a specified lookback period and serves as an indicator of market trend persistence.

Unlike daily returns, momentum summarizes the recent trajectory of the asset rather than a single observation.

### Economic Interpretation

Positive momentum suggests that buying pressure has dominated over the lookback window.

Negative momentum suggests sustained selling pressure.

Momentum therefore captures trend persistence rather than daily fluctuations.

### Why Momentum Matters

Empirical evidence shows that financial markets often exhibit momentum due to investor underreaction, institutional trading constraints, and herding behavior.

These effects create persistent trends that can be exploited by systematic trading strategies.

### Role in Regime Detection

Momentum provides temporal context to the Hidden Markov Model.

A positive daily return during a strongly negative momentum regime may simply represent a temporary rebound rather than a genuine regime transition.

Combining momentum with volatility allows the HMM to distinguish between temporary corrections and persistent market shifts.

## Complementary Feature Design

A robust feature set should consist of complementary variables rather than multiple versions of the same statistic.

Each engineered feature should answer a distinct economic question.

| Feature | Economic Question |
|----------|-------------------|
| Returns | What happened today? |
| Rolling Volatility | How uncertain is the market? |
| Momentum | Is the market trending? |
| Rolling Correlation | Are asset relationships changing? |
| VIX | What is investor sentiment? |

By combining features that describe different dimensions of the market, the Hidden Markov Model receives a richer statistical representation of the underlying economic environment.

### Feature Engineering Checklist

Before including any feature in the model, consider:

1. Does it represent a meaningful economic concept?
2. Does it provide information not already captured by other features?
3. Does it react at an appropriate speed for the intended application?
4. Is it robust to market noise?
5. Can it help distinguish between hidden market regimes?

## Cross-Asset Relationships

Financial markets operate as an interconnected system rather than a collection of independent assets.

Different asset classes respond differently to macroeconomic conditions, and the relationships between them often change across market regimes.

### Rolling Correlation

Rolling correlation measures the co-movement between two assets over a moving time window.

Unlike a single historical correlation, rolling correlation captures the evolving dependence structure of financial markets.

### Economic Interpretation

Changes in stock-bond correlations often reflect shifts in investor risk appetite, monetary policy expectations, or macroeconomic uncertainty.

These relationship changes provide valuable information for Hidden Markov Models because they represent observable consequences of hidden economic regime transitions.

### Research Insight

Market regimes are characterized not only by changes in returns and volatility but also by changes in the relationships between assets.

Therefore, correlation is itself a dynamic feature rather than a fixed market statistic.

## Financial Markets as an Interconnected System

A common mistake in quantitative finance is to analyze each asset independently.

Professional macro investing instead views financial markets as an interconnected system in which equities, bonds, commodities, and volatility continuously interact.

The relationships between these asset classes often contain more information than the individual asset returns themselves.

### Hidden Regimes as System-Wide Phenomena

A market regime is not characterized by the behavior of a single asset.

Instead, it emerges from the collective behavior of multiple asset classes.

For example, a transition from a bull market to a crisis is often accompanied by:

- Weakening equity momentum
- Rising market volatility
- Increasing demand for Treasury bonds
- Increasing VIX
- Changing stock-bond correlations

Each individual feature provides only partial information.

Together, they create a coherent statistical representation of the hidden economic environment.

### Research Insight

Hidden market regimes should be viewed as latent macroeconomic states that gradually reveal themselves through observable changes in multiple financial variables.

The role of feature engineering is therefore not to maximize the number of variables, but to maximize the amount of complementary economic information available to the Hidden Markov Model.

## The VIX as a Forward-Looking Feature

Unlike realized volatility, the VIX is derived from option prices and represents the market's expectation of future volatility over approximately the next 30 days.

### Realized vs. Implied Volatility

- **Realized volatility** measures how much prices have fluctuated in the past.
- **Implied volatility** reflects how much the options market expects prices to fluctuate in the future.

The VIX is therefore a forward-looking measure of uncertainty.

### Economic Interpretation

An increase in the VIX indicates greater demand for downside protection through options, suggesting heightened investor concern about future market conditions.

Because option traders often react before large price movements occur, the VIX may provide early evidence of regime transitions.

### Role in Hidden Markov Models

The VIX complements historical features by adding information about market expectations.

This allows the Hidden Markov Model to infer hidden economic states using both realized market behavior and forward-looking investor sentiment.