# Research Notes — Notebook 04
## Hidden Markov Model (HMM) Regime Detection

---

## Objective

The objective of this notebook was to identify latent market regimes using a Hidden Markov Model (HMM) trained on engineered financial features developed in Notebooks 1–3. The notebook focused on validating the statistical quality, economic interpretation, and historical relevance of the inferred regimes before using them in portfolio construction.

---

# Methodology

### Model Selection

Multiple Gaussian Hidden Markov Models were trained with different numbers of hidden states.

Candidate models:

- 2 States
- 3 States
- 4 States
- 5 States

Each model was evaluated using:

- Log-Likelihood
- Akaike Information Criterion (AIC)
- Bayesian Information Criterion (BIC)
- EM Algorithm Convergence

The 5-state model achieved the highest likelihood together with the lowest AIC and BIC while successfully converging, and was therefore selected for further analysis.

---

# Observation Features

The HMM was trained using standardized engineered features representing different aspects of market behaviour.

Selected features:

- SPY Daily Return
- TLT Daily Return
- SPY 20-Day Volatility
- SPY 63-Day Volatility
- TLT 20-Day Volatility
- TLT 63-Day Volatility
- SPY 20-Day Momentum
- SPY 63-Day Momentum
- SPY–TLT Rolling Correlation (20-Day)
- VIX Level

All features were standardized prior to model estimation.

---

# Hidden State Decoding

The fitted HMM was used to infer the most probable hidden state for every trading day using the Viterbi algorithm.

The decoded regimes were appended to the engineered feature dataset for further statistical analysis.

---

# Model Diagnostics

Several diagnostics were performed to validate the model.

## 1. Information Criteria

Compared competing HMMs using:

- Log-Likelihood
- AIC
- BIC

The 5-state model provided the best overall statistical fit.

---

## 2. State Occupancy

Calculated:

- Number of observations in each regime
- Percentage of historical observations

Purpose:

- Detect unused states
- Identify dominant market regimes
- Evaluate model balance

One regime occupied only a small proportion of history but was retained because it corresponded to economically meaningful crisis periods.

---

## 3. Transition Matrix

Estimated the Markov transition probability matrix.

The transition matrix was analysed to verify:

- Regime persistence
- Transition probabilities
- Economic plausibility

Diagonal probabilities exceeded 96% for every state, indicating persistent market regimes.

---

## 4. Expected Regime Duration

Expected duration was computed as:

Expected Duration = 1 / (1 − Pii)

where Pii denotes the probability of remaining in the same hidden state.

Estimated regime durations ranged approximately from:

- 32 days
- 75 days

These durations are economically consistent with medium-term market regimes.

---

# Economic Interpretation

After decoding the hidden states, summary statistics were computed for every regime.

Variables analysed included:

- SPY Returns
- TLT Returns
- Rolling Volatility
- Momentum
- SPY–TLT Correlation
- VIX Level

Rather than assigning labels immediately, financial interpretation was performed only after analysing the statistical characteristics of each state.

---

# Preliminary Regime Interpretation

| State | Interpretation |
|--------|----------------|
| State 0 | Expansion / Moderate Bull |
| State 1 | High-Volatility Recovery |
| State 2 | Defensive / Transitional |
| State 3 | Crisis / Panic |
| State 4 | Stable Bull Market |

These interpretations were derived from multiple indicators simultaneously rather than any single metric.

---

# Historical Validation

Hidden regimes were overlaid on the historical SPY price series.

The objective was to determine whether inferred regimes aligned with known market events.

Major observations:

- Crisis regime appeared during the 2008 Financial Crisis.
- Crisis regime reappeared during the COVID-19 market crash.
- Stable Bull regime dominated long expansionary periods.
- Intermediate regimes captured market transitions between major phases.

This provided historical validation of the inferred latent states.

---

# Distributional Analysis

Distributional differences between regimes were examined using boxplots.

Variables analysed:

- SPY Returns
- SPY Volatility
- VIX
- TLT Returns

The Crisis regime exhibited:

- Highest volatility
- Largest return dispersion
- Extreme downside observations

The Stable Bull regime exhibited:

- Low volatility
- Narrow return distributions
- Limited downside risk

These findings confirmed that the hidden states represent statistically distinct market environments.

---

# Key Findings

- Five hidden regimes best described historical market dynamics.
- Market regimes exhibited strong persistence.
- Hidden states were economically interpretable.
- Historical market crises were successfully identified.
- Statistical and financial evidence jointly supported the selected HMM.

---

# Limitations

The following limitations were identified:

- Gaussian emissions may not fully capture heavy-tailed financial returns.
- Daily classifications may contain short-term fluctuations near regime boundaries.
- Regime labels are interpretative rather than directly estimated.
- Model performance depends on the selected feature set.

---

# Deliverables

Outputs generated during this notebook include:

- Trained Gaussian Hidden Markov Model
- Hidden regime sequence
- Transition probability matrix
- State occupancy statistics
- Expected regime duration
- Regime summary statistics
- Historical regime visualization
- Distributional validation plots

---

# Conclusion

Notebook 04 established a statistically validated and economically interpretable Hidden Markov Model capable of identifying persistent latent market regimes. These inferred regimes provide the decision-making layer required for regime-aware tactical asset allocation, forming the foundation for portfolio optimization in Notebook 05.