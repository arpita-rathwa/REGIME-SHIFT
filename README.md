# REGIME-SHIFT ⚡
### Macro-Aware Tactical Asset Allocation Engine

> A dynamic allocation engine that detects hidden economic regimes using Hidden Markov Models and automatically shifts capital between equities, fixed income, and safe havens — built for real-world survival, not hallucinated backtest alpha.

---

## Problem Statement

Standard quantitative strategies and static portfolios (like the classic 60/40) rely heavily on stationary assumptions, working perfectly during prolonged bull runs but failing catastrophically during structural market breaks. In the institutional Global Macro and Multi-Asset space, a static allocation is a liability. The ability to mathematically detect, quantify, and adapt to unobservable economic regime changes is the absolute core of modern portfolio management.

This project bridges the gap between unsupervised machine learning and classical convex portfolio theory — building a dynamic allocation engine from scratch that ingests noisy, multi-asset market data, classifies hidden economic states using Hidden Markov Models (HMM), and automatically shifts capital between equities, fixed income, and safe havens.

The true challenge isn't just fitting a statistical model to historical data — it is executing that logic without falling victim to lookahead bias and portfolio thrashing. Standard backtests often hallucinate alpha by acting on data from the future or ignoring the devastating cost of high turnover. By building a rigorous walk-forward validation harness, dynamically mapping optimization objectives to specific regimes, and explicitly penalizing transaction friction, this project is engineered for robust, real-world survival — demonstrating the exact risk-aware mindset that top-tier hedge funds demand from quantitative researchers.

---

## Technical Scope

### Task Type
- **Unsupervised regime detection** — classifying unobservable hidden economic states from observable market data
- **Convex portfolio optimization** — dynamically allocating capital across asset classes per detected regime
- **Walk-forward backtesting** — rigorous temporal validation that mirrors live trading conditions

### Core Technical Components

**Hidden Markov Models (HMM)**
- Models the market as a sequence of hidden states (e.g., bull, bear, crisis, recovery) that cannot be directly observed
- Observable emissions: returns, volatility, correlations, macro indicators
- **Viterbi Algorithm** — decodes the most likely sequence of hidden states given the observed data
- Regime transition matrix — probability of moving from one regime to another at each time step

**Convex Portfolio Optimization (CVXPY)**
- Mean-variance optimization per regime — different risk/return objectives for each economic state
- Constraints: long-only, weight bounds, sector limits
- Regime-conditioned objectives: maximize Sharpe in trending regimes, minimize drawdown in crisis regimes, shift to safe havens during high-volatility regimes
- Transaction cost penalization built directly into the optimization objective

**Walk-Forward Validation**
- Expanding or rolling window training — model is retrained at each step using only past data
- No lookahead bias — allocation decisions at time T use only data available before T
- Mirrors the actual constraints of a live trading system

**Transaction Friction Modelling**
- Turnover penalty explicitly included in backtesting to prevent portfolio thrashing
- Models realistic bid-ask spreads and rebalancing costs
- Prevents the common backtest illusion where high-frequency rebalancing generates phantom alpha

### Data
- Multi-asset market data via **yfinance** (equities, bonds, commodities, currencies)
- Macro-level indicators as observable HMM emissions

### Performance Metrics
- **Sharpe Ratio** — risk-adjusted return (excess return per unit of total volatility)
- **Sortino Ratio** — like Sharpe but penalizes only downside volatility
- **Calmar Ratio** — annualized return divided by maximum drawdown; measures recovery efficiency
- Maximum drawdown, turnover rate, regime-conditional performance breakdown

### Tech Stack

| Tool | Purpose |
|---|---|
| Python 3.9+ | Core language |
| hmmlearn | Hidden Markov Model training and inference |
| CVXPY | Convex portfolio optimization |
| NumPy | Numerical computation |
| Pandas | Data manipulation and time series handling |
| Matplotlib | Visualization (regime overlays, performance charts) |
| yfinance | Market data ingestion |
| scipy | Statistical utilities |

### Concepts to Master
- Hidden Markov Models & Viterbi Algorithm
- Convex Portfolio Optimization
- Walk-Forward Validation
- Sharpe / Sortino / Calmar Ratios
- Transaction Friction Modelling

### Technical Challenges
- **Regime label instability** — HMMs can flip regime labels across training runs; requires careful state alignment
- **Non-stationarity** — market regimes themselves evolve; a regime in 2008 may look different from one in 2020
- **Curse of dimensionality** — adding too many assets or features degrades HMM estimation quality
- **Overfitting to historical regimes** — the model must generalize to unseen regime structures, not just memorize past ones
- **Lookahead bias** — the single most dangerous error in quantitative backtesting; fully eliminated via walk-forward design

---

## ML Axes

| Axis | Detail |
|---|---|
| Learning Paradigm & Training Regime | Unsupervised (HMM regime detection) + optimization layer |
| Scope & Complexity | Generative probabilistic model · Research-grade |
| Data Modality | Multi-asset time series (prices, returns, volatility) |
| Explainability & Impact | High — regime-interpretable, institutional hedge fund relevance |

---

## To Be Added
- [ ] Model training results and regime visualizations
- [ ] Walk-forward backtest performance vs. 60/40 benchmark
- [ ] Sharpe / Sortino / Calmar ratio comparison across regimes
- [ ] Regime transition matrix heatmap
- [ ] Turnover and transaction cost analysis
