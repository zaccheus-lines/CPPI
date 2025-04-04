# Portfolio Strategies and Financial Simulations

This project explores portfolio management techniques and derivatives pricing using Python and Jupyter Notebooks. It includes a detailed simulation of the Constant Proportion Portfolio Insurance (CPPI) strategy, covariance matrix estimation for portfolio diversification, and empirical testing of put-call parity in Bitcoin options.

---

## CPPI Simulation

The Constant Proportion Portfolio Insurance (CPPI) strategy adjusts the exposure to risky assets dynamically based on a predefined floor level to protect against downside risk while maintaining upside potential.

Stock prices are simulated using a Geometric Brownian Motion (GBM) with the following assumptions:
- Drift: 10%
- Volatility: 20%
- Risk-free rate: 2%
- Monthly rebalancing
- Initial investment: \$100

The portfolio is simulated across 10,000 paths over a 3-year horizon with different leverage multipliers (`m = 1, 3, 5`). Monthly portfolio rebalancing is conducted using the CPPI allocation rule, where exposure to the risky asset depends on the cushion value above the floor.

Visualizations include:
- Sample paths of the simulated stock index
- Histogram of gross portfolio returns
- Comparison of return distributions across different multipliers

Key statistics such as minimum, mean, and percentiles (25th, 50th, 75th) of portfolio gross returns are computed to assess the performance impact of leverage.

---

## Structured Covariance Matrix Estimation

To evaluate the impact of estimation methods on portfolio diversification, this section estimates portfolio weights using:
- Sample Covariance Matrix
- Structured Covariance Matrix (constant correlation model from Elton & Gruber)

Diversification is evaluated using two metrics:
- **Leverage**: Magnitude of negative weights
- **ENC (Effective Number of Constituents)**: Measures portfolio concentration

The dataset includes monthly returns for 70 portfolios formed on size and book-to-market, sourced from Ken French’s data library (Jan 1970 to Sep 2024).

The structured covariance matrix assumes constant correlation across all assets and uses individual volatilities to build the matrix.

A rolling window of 10 years (120 months) is used to analyze leverage and ENC over time. The out-of-sample returns of GMV (global minimum variance) portfolios are computed and compared.

Findings show that:
- Portfolios based on the sample covariance matrix exhibit higher and more volatile leverage.
- Structured covariance portfolios are more stable and better diversified, though slightly higher in out-of-sample volatility.

---

## Put-Call Parity in Bitcoin Options

This analysis investigates the validity of the put-call parity relationship in BTC options data.

The dataset includes call and put prices with matching:
- Trade date
- Maturity date
- Strike price

Twin options are matched and the price spread (call price minus put price) is calculated.

A linear regression is conducted between strike price and price spread. The distribution of R-squared values shows:
- Mean R² ≈ 0.97
- Most twin pairs show near-perfect linear relationships

However, a t-test on the regression intercept reveals:
- 0% of twin pairs have intercepts statistically equal to zero
- Implies consistent and significant deviation from theoretical put-call parity

These findings suggest market frictions or pricing inefficiencies in BTC options markets, despite the high explanatory power of strike price on the spread.

---

## How to Run

1. Install required libraries:
```bash
pip install numpy pandas matplotlib scipy
