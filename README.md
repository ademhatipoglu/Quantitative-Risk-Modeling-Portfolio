# Quantitative Risk Management & Portfolio Analytics

## Executive Summary
This repository serves as a comprehensive risk management framework, modeling market and interest rate risks for multi-asset portfolios. The objective is to quantify potential portfolio losses, evaluate tail risks under stressed market conditions, and capture time-varying volatility dynamics. The methodologies applied bridge the gap between theoretical econometrics and practical asset management requirements.

## Project Scope and Methodologies

### 1. Yield Curve Dynamics & Interest Rate Risk
* **Objective:** To identify the underlying drivers of interest rate movements and quantify their impact on fixed-income exposures.
* **Methodology:** Applied Principal Component Analysis (PCA) on Euro area AAA-rated government bond yields. The covariance matrix is decomposed by solving the eigenvalue problem:
  
  $$C v_k = \lambda_k v_k$$

  where $\lambda_k$ represents the variance explained by factor $k$, and $v_k$ is the corresponding eigenvector.
* **Application:** Constructed a factor-based risk model to calculate standard deviation and 99% 1-day Value-at-Risk (VaR), demonstrating vulnerability to curve steepening and flattening scenarios.

### 2. Empirical Tail Risk & Stress Testing
* **Objective:** To assess the empirical tail risk of a diversified global equity portfolio (DJIA, FTSE 100, CAC 40) using 15 years of historical data.
* **Methodology:** Implemented Historical Simulation to calculate 99% VaR and Expected Shortfall (ES). The Expected Shortfall is defined as the expected loss conditional on losses exceeding the VaR level:
  
  $$ES_{\alpha} = \mathbb{E}[L | L \ge VaR_{\alpha}]$$

* **Application:** Enhanced the standard historical approach by integrating stress testing (COVID-19 pandemic shock) and applying non-parametric bootstrapping (1,000 resamples) to establish 95% confidence intervals around the risk metrics.

### 3. Time-Varying Volatility & Stochastic Simulation
* **Objective:** To estimate short-term market risk by accounting for volatility clustering and mean-reverting market behavior.
* **Methodology:** Estimated time-varying covariance matrices using Exponentially Weighted Moving Average (EWMA) and Maximum Likelihood Estimation for GARCH(1,1) processes. The GARCH(1,1) variance process is modeled as:
  
  $$\sigma_t^2 = \omega + \alpha r_{t-1}^2 + \beta \sigma_{t-1}^2$$

  And the EWMA is defined with a decay factor $\lambda$:

  $$\sigma_t^2 = \lambda \sigma_{t-1}^2 + (1 - \lambda) r_{t-1}^2$$

* **Application:** Computed parametric VaR and ES, cross-validating these analytical metrics by deploying a Monte Carlo simulation engine generating 100,000 multivariate normal daily return scenarios.

## Technical Infrastructure
* **Core Language:** Python
* **Libraries:** pandas, numpy, scipy, statsmodels, scikit-learn
* **Domain Expertise:** Econometrics, Volatility Modeling, Dimensionality Reduction, Stochastic Simulations
