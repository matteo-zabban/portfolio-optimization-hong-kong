# Portfolio Optimization in the Hong Kong Market

**Mean–Variance Optimization vs Equal-Weight Allocation**

An empirical quantitative-finance project comparing monthly rebalanced **equal-weight (EW)** and **Markowitz mean–variance (MV)** portfolios using market data downloaded through `yfinance`. The analysis explores whether optimization improves risk-adjusted performance—and whether better performance necessarily means better diversification.

## Research questions

1. Does mean–variance optimization improve the risk–return trade-off relative to equal weighting?
2. Does an optimized portfolio diversify risk or concentrate capital in fewer assets and sectors?
3. How sensitive are the results to portfolio weight constraints?

## Data and methodology

- **Sample:** January 2023–December 2025, using Yahoo Finance price data.
- **Universe:** Eight Hong Kong-listed equities spanning finance, technology, real estate and consumer goods, plus gold futures (`GC=F`) as an additional asset in the notebook's downloaded universe.
- **Strategies:** equal weighting and rolling mean–variance optimization, with monthly rebalancing.
- **Estimation:** 252-trading-day rolling window; historical expected returns and Ledoit–Wolf covariance shrinkage.
- **Optimization:** maximum Sharpe ratio, with a minimum-volatility fallback when necessary; long-only weight constraints.
- **Benchmark:** Hang Seng Index (`^HSI`).
- **Evaluation:** annualized return, volatility, Sharpe ratio, maximum drawdown, historical/parametric VaR and expected shortfall, concentration (HHI/effective holdings), sector exposure, turnover, and internal correlation.

> **Implementation note:** The primary notebook currently sets `weight_cap = 0.32` (32%), whereas some explanatory markdown cells describe a 35% cap. The code is the source of truth for the executed specification; this discrepancy should be reconciled before treating the report as final. The universe also includes gold futures, so the experiment is not strictly equities-only.

## Selected findings

The notebook's reported backtest results are approximately:

| Strategy | Annualized return | Sharpe ratio | Maximum drawdown |
| --- | ---: | ---: | ---: |
| Equal weight | 26.9% | 1.13 | −21.4% |
| Constrained mean–variance | 31.5% | 1.41 | −19.6% |
| Unconstrained-cap mean–variance (robustness test) | 40.7% | 1.89 | Not summarized here |

The constrained MV strategy showed stronger risk-adjusted returns than EW in the studied window, but it was also **more concentrated by asset weights**. Removing the cap increased backtested performance while reducing the effective number of holdings to roughly 1.5–2.2. These are **historical backtest observations**, not forward-looking performance claims.

## Repository contents

```text
notebooks/
  portfolio_optimization.ipynb   # Main analysis and results

docs/
  MS4226_Group12_REPORT.pdf      # Group project report (PDF)

requirements.txt
.gitignore
README.md
```

## Project report

[Read the group project report (PDF)](docs/MS4226_Group12_REPORT.pdf). This was a **group project**; the report credits the contributors.

## Run locally

1. Clone or download this repository.
2. Install dependencies: `pip install -r requirements.txt`.
3. Open `notebooks/portfolio_optimization.ipynb` in Jupyter or VS Code and run cells in order.

The notebook downloads data from Yahoo Finance at runtime. Data availability and vendor adjustments may change, so rerunning the analysis can produce different results. No investment advice is intended.

## Limitations

- Short historical sample and sensitivity to the chosen assets and estimation window.
- Transaction costs, slippage and market-impact assumptions are not established as part of the headline results.
- Optimized allocations can be highly sensitive to expected-return estimates and portfolio constraints.
- The code/markdown weight-cap discrepancy should be corrected for full reproducibility.

## Tools

Python · pandas · NumPy · Matplotlib · yfinance · PyPortfolioOpt · SciPy · Jupyter
