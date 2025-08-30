# On the Superiority of Data-Driven Combined Forecasts Based on Deep Learning Models

Forecasting financial asset prices and quantifying associated risks are critical challenges in computational finance. This study presents an optimal forecast combination framework by integrating advanced time series models and machine learning techniques to enhance prediction accuracy and risk assessment. A novel data-driven risk measure ($DDRisk_{new}$) based on price differences is introduced, and $sign$ correlation is used to capture risk and mitigate the limitations of traditional risk metrics. Our approach incorporates state-of-the-art forecasting models, including ARIMA, Neural Network Autoregressive, Long Short-Term Memory, XGBoost, and Random Forest, alongside two combination methods: equally weighted averages (FComp\_SA) and data-driven optimal weighted averages (FComp\_Weighted).

The PDF copy of the paper can be downloaded from here: [Download Paper](https://ieeexplore.ieee.org/abstract/document/11126694) 

A preprint version of the paper is available in the repository.

Programming Language: [R](https://cran.r-project.org/bin/windows/base/) / [RStudio](https://posit.co/downloads/)

Data: The provided R codes download data directly from [Yahoo!Finance](https://ca.finance.yahoo.com/)

### A New Risk Measure ($DDRisk_{new}$)

Based on our empirical analysis, it has been observed that the fitted ARIMA models for all stock prices have first differences during the study period, indicating that the price difference ($d_{t} = P_{t} - P_{t-1}$) is a stationary series. Thus, we use the price difference (because of the stationary behaviors) to define a new risk measure that we call Data-Driven New Risk ($DDRisk_{new}$) as
```math
    DDRisk_{new} = \frac{|d - E[d]|}{\rho},
```
where $\rho = Corr(d-E(d), sign(d-E(d)))$.

### Optimal Forecast Combination

Let for the target variable $y$, $\hat{y}_{k,t+h|t}$ is the h-step ahead forecast ($h=1,2, \ldots, H$) using model $k$ ($k=1,2, \ldots, K$) given the information up to time $t$ is available. Then the forecast combination based on the optimal weight (FComb\_Weighted) can be derived as:
```math
    \hat{y}_{t+h|t}^{c}= \sum_{k=1}^{K} w_k \ \hat{y}_{k,t+h|t}
```
where $w_k$ $\left( \sum_{k=1}^{K} w_k = 1 \right)$ are the weights associated with the individual models. In this work, the optimal weight $(w^{*})$ is obtained by minimizing the one-step ahead forecast error sum of squares (FESS),
```math
    \text{FESS} = \sum_{h=1}^{H} (y_{t+h} - \hat{y}_{t+h|t}^{c})^{2},
```
where $y_{t+h}$ is the observed value of $y$ at time $t+h$.

### Findings

Experimental results conducted on a dataset of stocks from ten diverse sectors during the highly volatile COVID-19 period demonstrate the superior performance of FComp\_Weighted in minimizing forecasting errors across multiple metrics (RMSE, MAE, MAPE). Moreover, the RMSE of asset price and $DDRisk_{new}$ forecasts using FComp\_Weighted models is always lower than the RMSE obtained using the FComp\_SA model.

### References

1. R. J. Hyndman and G. Athanasopoulos, Forecasting: principles and practice, 3rd edition, OTexts: Melbourne, Australia. OTexts.com/fpp3, 2021.
2. Thavaneswaran, A., Paseka, A., \& Frank, J. (2020). Generalized value at risk forecasting. Communications in Statistics-Theory and Methods, 49(20), 4988-4995.
