# Weekly Sales Forecasting with Facebook Prophet

After the Marketing Mix Model, I wanted to go one step further and work with data that actually moves through time. The adstock transformation in my previous project is built for time-series data, and this felt like the right way to do it properly. This project is self-driven, another step in translating what I studied into something real.

---

## What the project does

Forecasts weekly e-commerce revenue using Facebook Prophet. The notebook covers exploratory data analysis, model fitting with tuned seasonality parameters, evaluation against a held-out 12-week test set, and a forward-looking 12-week forecast with confidence intervals.

---

## Dataset

**UCI Online Retail Dataset**
UK-based online retailer, December 2010 to December 2011. Each row is a transaction line item with product, quantity, unit price, and timestamp. Revenue is computed as Quantity × UnitPrice and aggregated to weekly frequency. The dataset is publicly available without authentication from the UCI ML Repository.

---

## Pipeline

1. **Data cleaning** — remove cancelled orders (InvoiceNo prefix C), drop rows with missing CustomerID or Description, filter out negative quantities and zero unit prices
2. **Feature engineering** — compute Revenue per line item, resample to weekly Monday-anchored sums
3. **EDA** — full time series plot, 4-week rolling mean and volatility, additive seasonal decomposition, z-score anomaly detection, monthly revenue distribution
4. **Modelling** — Facebook Prophet with multiplicative seasonality mode, tuned changepoint and seasonality priors, custom monthly seasonality component added alongside yearly
5. **Evaluation** — 12-week train/test split, MAE, RMSE, MAPE, residual analysis
6. **Forward forecast** — model retrained on full dataset, 12-week horizon with 95% confidence intervals

---

## Key findings

Revenue has a clear upward trend through 2011 and a sharp Q4 spike in November and December. The seasonal decomposition confirms a strong yearly cycle. A handful of anomalous weeks cluster around the holiday period, driven by large promotional orders. Residuals are roughly centred around zero with no systematic directional bias, which means the model is not systematically over or under-forecasting.

---

## Results

Prophet captures the trend and the yearly seasonal ramp-up well. The 12-week test evaluation shows the model tracking actual revenue closely, with error metrics expressed relative to mean weekly revenue in the model performance table inside the notebook. Confidence intervals widen with forecast horizon, which is the expected behaviour for an honest probabilistic model.

---

## Stack

| Tool | Purpose |
|---|---|
| Python 3.10 | Core language |
| pandas | Data loading, cleaning, weekly resampling |
| numpy | Numerical operations |
| matplotlib / seaborn | All visualisations |
| statsmodels | Seasonal decomposition |
| Facebook Prophet | Time series forecasting model |
| scikit-learn | MAE and RMSE computation |
| Jupyter Notebook | Analysis environment |
