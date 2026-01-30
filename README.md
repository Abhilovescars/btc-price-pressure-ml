# btc-price-pressure-ml
This project explores how short-horizon directional signals can be extracted from tick-level BTC trade data using a from-scratch implementation of linear regression.
Short-Horizon Price Pressure Modeling using Linear Regression (From Scratch)
Overview

This project explores how short-horizon directional signals can be extracted from tick-level BTC trade data using a from-scratch implementation of linear regression.

Instead of attempting precise price prediction, the goal is to model short-term price pressure—i.e., whether the market is slightly more likely to move up or down over the next few trades—using simple, interpretable features derived from recent trade activity.

This project emphasizes:

correct problem formulation for financial time series

proper evaluation on unseen future data

optimization behavior on large, noisy datasets

interpretability over black-box accuracy

Problem Statement

At very short horizons, financial markets are dominated by noise.
The objective is not to predict exact prices, but to answer:

Given recent trade activity, is the next short-term move more likely to be up or down?

This is a core problem in:

quantitative trading

execution algorithms

market microstructure analysis

ML-driven trading infrastructure

Data

Instrument: BTC (crypto)

Data type: Tick-level trade data

Granularity: Individual trades

Target: Price change after a fixed number of future trades (horizon-based)

A strict time-based train/test split is used to simulate real-world deployment and avoid data leakage.

Feature Engineering

Each trade is represented using three simple, interpretable features:

Recent price change
Captures short-term momentum or mean reversion.

Trade volume
Approximates price impact from trade size.

Time since last trade
Captures market activity / liquidity conditions.

All features are standardized before training to ensure stable optimization.

Model

Model: Linear Regression

Implementation: From scratch (no sklearn or ML libraries)

Loss function: Mean Squared Error (MSE)

Optimization:

Batch Gradient Descent

Mini-batch Gradient Descent (for scalability comparison)

The model is intentionally simple to prioritize:

interpretability

stability

correct evaluation

Evaluation Metrics

Because short-horizon financial targets are extremely noisy, evaluation focuses on:

Mean Squared Error (MSE)
To measure overall fit.

Directional Accuracy
Percentage of times the model correctly predicts the direction of future price movement.

Baseline Comparison
A zero-prediction baseline (predicting no price change) is used to verify that the model adds real value.

Results
Baseline vs Model

The trained model consistently outperforms a zero-prediction baseline in both MSE and directional accuracy.

Directional accuracy on unseen future data is approximately 54%, which is meaningful at short horizons in financial markets.

Optimization Comparison

Mini-batch gradient descent converges significantly faster than batch gradient descent on this large dataset.

Mini-batch optimization also achieves slightly better out-of-sample performance due to its stochastic nature.

Horizon Analysis

Directional accuracy was evaluated across multiple prediction horizons:

Horizon (Trades Ahead)	Directional Accuracy
5	~53%
10	~54%
20	~54%
30–40	~55%

Interestingly, accuracy increases slightly with horizon, suggesting that the model captures persistent order-flow pressure rather than immediate microstructure noise.

Key Takeaways

Short-horizon financial prediction is noise-dominated; small, stable edges matter more than point accuracy.

Simple linear models, when evaluated correctly, can extract meaningful directional signals.

Proper baselines, time-aware validation, and interpretability are critical in quantitative ML.

Optimization behavior (batch vs mini-batch) matters significantly at scale.

Limitations & Future Work

Only trade-level features are used (no order book data).

No transaction costs or execution modeling is included.

Future extensions could explore:

toy P&L simulations

richer microstructure features

comparison with non-linear models

Tech Stack

Python

NumPy

Pandas

Matplotlib

Google Colab

Author

Built as a learning-focused project to deepen understanding of:

machine learning fundamentals

optimization

financial time series

quantitative modeling principles

How to Run

Clone the repository

Open the notebook in Google Colab or Jupyter

Run cells sequentially from data preparation to evaluation

would love to have more contributions to this project, PRs are encouraged!.
