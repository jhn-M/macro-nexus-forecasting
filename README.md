# Title: Forecasting Macroeconomic Trends: The Nexus of Exchange Rates, Energy, and CPI Hybrid SARIMA + Machine Learning model: Forecasting Philippine inflation using oil prices, USD-PHP exchange rates, and NLP sentiment scores from financial news.

**Status:** In Progress — Correction Layer Development

## Problem Statement
Inflation forecasting is critical for banks, financial institutions, and market participants making forward-looking decisions, yet most univariate models fail to capture the external shocks that drive sudden price movements. This project builds a hybrid SARIMA model corrected by machine learning using macroeconomic indicators — Brent crude oil prices, USD-PHP exchange rates, and NLP sentiment scores derived from financial news headlines — to forecast Philippine inflation one to several months ahead. A key limitation of this approach is that while sentiment and oil prices exhibit high daily volatility that likely influences inflation, BSP reports inflation monthly, forcing all features to be aggregated at the monthly level and potentially losing granular signal in the process.

## Architecture Overview
The following steps are structured to create the final Model to forecast Inflation Rates:

**Step 1: Scrape Data:**
- 1.1  Scrape Headlines in Business world Headlines Using BeautifulSoup while Enforcing it with ThreadPoolExecutor to make it scrape faster.
- 1.2 Get the Inflation rates from BSP while Oil brent and USD PHP exchange can get using yfinance library

**Step 2: Clean Data**
- 2.1. Removing unnecessary symbols to headlines
- 2.2. removing stop words
- 2.3.  Remove NaNs for exogeneous variables
- 2.4. Make sure to apply correct time stamps by lagging or leading the data after using rolling mean to make sure there is no leakage.

**Step 3: Modeling**
- 3.1. Create ARIMA/SARIMA model varies on whether the data has seasonality or not 
- 3.2. Then Create RF-Regression model and XG boost model to catch the non linearity of ARIMA/SARIMA.
- 3.3. RF-Regression and XGBoost models are trained on SARIMA residuals to capture non-linear patterns the SARIMA cannot model. The correction model's output is added to the SARIMA forecast to produce the final hybrid prediction.

**Step 4: Evaluate the Models** 
- 4.1. Evaluate the two model plus their ensemble model (aggregating the two model's result) to see which of the three performs well
- 4.2 Then Create the final Model by integrating it to SARIMA results

**Step 5: Conclusion and Findings**
- 5.1. State what the findings are. 
- 5.2. Did the Multi Model performs better than ARIMA/SARIMA? 
- 5.3. Did they successfully corrected the errors.
- 5.4. What are the Limitations that the modeling encountered etc.

## Data Sources
- 1. **Inflation rates:** https://www.bsp.gov.ph/Statistics/Prices/tab34_inf_2018.aspx, Jan. 2021 - March 2026
- 2. **USD/PHP: ticker:** USDPHP=X, Date range: Jan.2021-Mar.2026
- 3. **Oil Brent: ticker:** BZ=F, Date range: Jan.2021-Mar.2026
- 4. **Sentiment scores:** finBERT applied to financial headlines scraped from Business World Online (https://www.bworldonline.com/banking-finance/), Jan. 2021 - Mar. 2026

## Progress

**Step 1: Scrape Data:**
- ✅ 1.1  Scrape Headlines in Business world Headlines Using BeautifulSoup while Enforcing it with ThreadPoolExecutor to make it scrape faster.
- ✅ 1.2 Get the Inflation rates from BSP while Oil brent and USD PHP exchange can get using yfinance library \
 
**Step 2: Clean Data**
- ✅2.1. Removing unnecessary symbols to headlines
- ✅2.2. removing stop words
- ✅2.3.  Remove NaNs for exogeneous variables
- ✅2.4. Make sure to apply correct time stamps by lagging or leading the data after using rolling mean to make sure there is no leakage.

**Step 3: Modeling**
- ✅3.1. Create ARIMA/SARIMA model varies on whether the data has seasonality or not 
- ✅3.2. Then Create RF-Regression model and XG boost model to catch the non linearity of ARIMA/SARIMA.
- ✅3.3. RF-Regression and XGBoost models are trained on SARIMA residuals to capture non-linear patterns the SARIMA cannot model. The correction model's output is added to the SARIMA forecast to produce the final hybrid prediction.

**Step 4: Evaluate the Models**
- ✅4.1. Evaluate the two model plus their ensemble model (aggregating the two model's result) to see which of the three performs well
- ⬜4.2 Then Create the final Model by integrating it to SARIMA results
 
**Step 5: Conclusion and Findings**
- ⬜5.1. State what the findings are. 
- ⬜5.2. Did the Multi Model performs better than ARIMA/SARIMA? 
- ⬜5.3. Did they successfully corrected the errors.
- ⬜5.4. What are the Limitations that the modeling encountered etc.

## Tech Stack
- **Language:** Python
- **Data Analysis and Engineering:** Pandas, NumPy, Exploratory Data Analysis (EDA), Feature Engineering, Data Cleaning 
- **Machine Learning:** Scikit-Learn, Random-Forest, Regression, XGboost, Model Evaluation 
- **Time Series and Econometrics:** ARIMA, SARIMA, Forecasting, Residual Modeling, Stationary Testing (ADF), Seasonal Decomposition, Statsmodels 
- **Natural Language Processing:** finBERT, Sentiment Analysis, Text Processing, Web Scraping(BeautifulSoup) 
- **Visualization:** Matplotlib

## Preliminary Results
SARIMA baseline metrics on the test set **(MSE: 0.5099, RMSE: 0.7141, MAE: 0.4168)** reflect expected behavior for a univariate model on a volatile macro series — strong at short horizons, degrading over longer forecast windows. The correction layer using exogenous variables is expected to address this degradation, particularly during external shock periods.

This plot shows how SARIMA captured perfectly the initial horizons as it struggles forecasting the volatility of inflation rates in the following months.
<img width="2084" height="735" alt="prelimenary_plot" src="https://github.com/user-attachments/assets/8830adbe-2e6a-4260-b752-c4f482008cb5" />

This plot shows the model evaluation, highlighting how Hybrid Model corrects initial ARIMA forecast
<img width="2084" height="735" alt="Model_evaluation_plot" src="https://github.com/user-attachments/assets/5fd88141-61d4-41c9-8d2e-1012c44a9095" />



## Next Steps
Currently building the model, applying direct step ahead prediction to random-forest to avoid its weakness (error propagation), along with XGboost, ensembling them to evaluate the three to see which performs better.

