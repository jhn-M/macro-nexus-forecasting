# Forecasting Macroeconomic Trends: The Nexus of Exchange Rates, Energy, and CPI

> **Note: This project is currently IN PROGRESS.** 🚧
> Data ingestion and architectural design are complete. I am currently refining the Hybrid ARIMA-Random Forest integration and optimizing the NLP sentiment pipeline.

## **Project Overview**
This project develops a **multi-stage hybrid forecasting system** to predict Philippine inflation (Consumer Price Index). Traditional statistical models often struggle with "shocks"—sudden price jumps caused by global events or currency fluctuations. To solve this, I’ve engineered a pipeline that combines the reliability of **time-series econometrics (ARIMA)** with the pattern-recognition power of **Machine Learning (Random Forest)** and the sentiment-awareness of **Natural Language Processing (NLP)**.

---

## **The Hybrid Methodology**
To capture the "Nexus" of factors affecting the Philippine economy, the project follows a four-pillar technical strategy:

### **1. Statistical Baseline: ARIMA/SARIMA**
*   **Role:** Captures the internal "memory" of inflation.
*   **Function:** Utilizes ARIMA to model the historical trend and seasonality of the Bangko Sentral ng Pilipinas (BSP) inflation data. This provides a clean baseline forecast based solely on previous price behavior.

### **2. Residual Correction: Random Forest (RF) Regression**
*   **Role:** Explains what the statistical model missed.
*   **Function:** Since ARIMA is often "blind" to external shocks, I train a **Random Forest Regressor** on the *residuals* (errors) of the ARIMA model. By using **USD-PHP exchange rates** and **Brent Crude Oil prices** as exogenous features, the RF learns to correct the forecast when energy costs spike or the Peso weakens.

### **3. Market Sentiment: Natural Language Processing (NLP)**
*   **Role:** Quantifying the "mood" of the economy.
*   **Function:** Economic data is often lagging. To get a real-time signal, I use NLP to analyze financial news headlines and BSP policy statements. By calculating **Sentiment Scores**, the model gains an "early warning" signal of upcoming inflationary pressure before it shows up in the official numbers.

### **4. Directional Logic: Random Forest (RF) Classification**
*   **Role:** Validating the trend.
*   **Function:** Beyond just predicting a number, I implement an **RF Classifier** to predict the *direction* of the move (e.g., "Will inflation increase by more than 0.5% next month?"). This acts as a secondary validation layer for the regression results.

---

## **Technical Stack**
*   **Languages:** Python (Pandas, NumPy, Scikit-Learn)
*   **Time-Series:** Statsmodels (ARIMA/SARIMA)
*   **Machine Learning:** Random Forest (Regression & Classification)
*   **NLP:** NLTK / VADER / Transformers (Sentiment Analysis)
*   **Data Sources:** Bangko Sentral ng Pilipinas (BSP), FRED Economic Data, News APIs

---

## **Why This Project Matters**
For an import-dependent country like the Philippines, inflation is driven by more than just domestic demand. By integrating **Exchange Rates** and **Energy** prices through a hybrid ML approach, this model provides a more resilient forecast than traditional methods, demonstrating a deep understanding of both data science and macroeconomic reality.
