# ML-Trading-Strategy
This document outlines a comprehensive machine learning approach to trading S&P 500 stocks, including data collection, feature engineering, clustering, and portfolio optimization.

## Key Components of the Strategy
### 1. Data Collection and Preparation
Downloads 8 years of historical data for all S&P 500 constituents from Yahoo Finance

Handles ticker symbols with special characters (replaces dots with dashes)

Creates a stacked DataFrame with multi-index (date, ticker)

### 2. Feature Engineering
The strategy calculates several technical indicators for each stock:

Garman-Klass Volatility: A measure of volatility using high, low, open and close prices

RSI (Relative Strength Index): Momentum oscillator (20-day lookback)

Bollinger Bands: With 20-day moving average and ±2 standard deviations

ATR (Average True Range): Measures market volatility

MACD (Moving Average Convergence Divergence): Trend-following momentum indicator

Dollar Volume: Price × Volume (liquidity measure)

### 3. Data Aggregation and Filtering
Converts daily data to monthly frequency

Filters to top 150 most liquid stocks each month based on 5-year rolling average dollar volume

Calculates monthly returns for different horizons (1m, 2m, 3m, 6m, 9m, 12m)

### 4. Factor Analysis
Incorporates Fama-French 5 factors (Market, Size, Value, Profitability, Investment)

Calculates rolling factor betas using 24-month windows

### 5. Clustering
Uses K-Means clustering with 4 clusters

Initializes centroids based on target RSI values (30, 45, 55, 70)

Selects stocks from cluster with RSI around 70 (hypothesized to continue outperforming)

### 6. Portfolio Optimization
For each month, optimizes portfolio weights using PyPortfolioOpt's Efficient Frontier

Maximizes Sharpe ratio with constraints (minimum 1/(2n) and maximum 10% per stock)

Falls back to equal weights if optimization fails

Calculates daily portfolio returns

### 7. Performance Comparison
Compares strategy returns to SPY (S&P 500 ETF) buy-and-hold

Visualizes cumulative returns over time

## Implementation Notes
The strategy handles many edge cases (missing data, optimization failures)

Uses robust data processing techniques (outlier clipping, normalization)

Implements a realistic trading workflow with monthly rebalancing

Includes comprehensive error handling and fallback mechanisms

## Potential Improvements
Experiment with different clustering approaches or number of clusters

Test alternative portfolio optimization objectives (minimum volatility, etc.)

Incorporate additional fundamental factors

Add transaction cost modeling

Implement more sophisticated risk management

This strategy demonstrates a systematic approach to combining technical indicators, factor models, and machine learning for quantitative trading.
