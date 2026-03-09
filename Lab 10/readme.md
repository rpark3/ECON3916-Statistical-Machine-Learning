# Detecting Spurious Correlation in Macroeconomic Time-Series Data

## Project Overview
This project investigates how misleading statistical relationships can emerge in macroeconomic time-series data due to non-stationarity, spurious correlation, and multicollinearity. Using economic indicators retrieved from the Federal Reserve Economic Data (FRED) API, the analysis demonstrates how raw level data can create false correlations that appear statistically significant but have no real causal meaning.

## Objective
The objective of this lab was to identify and correct statistical distortions in macroeconomic datasets by combining visualization, diagnostic testing, and proper data transformation techniques.

## Methodology

### 1. Data Collection
Macroeconomic indicators were retrieved programmatically using the **FRED API** and processed in **Python** using the `pandas` library.

### 2. Exploratory Analysis
Initial exploratory analysis visualized relationships between variables using **Seaborn** correlation plots. When using raw level data, many variables appeared highly correlated due to shared long-term trends rather than genuine economic relationships.

### 3. Multicollinearity Diagnostics
To quantify redundancy between predictors, **Variance Inflation Factor (VIF)** diagnostics were calculated using `statsmodels`. High VIF scores confirmed severe multicollinearity, indicating that several variables were explaining overlapping variance in the regression models.

### 4. Time-Series Transformation
To address non-stationarity, variables were transformed into **Year-over-Year (YoY) growth rates**, removing shared trend components and revealing more realistic relationships between economic indicators.

### 5. Structural Causal Reasoning
Finally, **Directed Acyclic Graphs (DAGs)** were used to conceptualize the underlying structural relationships between variables. This step helped distinguish correlation from causation and clarified which variables should be treated as drivers, mediators, or outcomes.

## Key Takeaways
- Raw macroeconomic level data can produce **spurious correlations** due to shared time trends.
- **Multicollinearity diagnostics** such as VIF help detect redundant explanatory variables.
- Transforming data into **growth rates** reduces non-stationarity and improves interpretability.
- **Causal diagrams (DAGs)** provide a structured way to reason about economic mechanisms beyond simple correlations.

## Tools & Technologies
- Python  
- pandas  
- seaborn  
- statsmodels  
- FRED API  

## Skills Demonstrated
- Time-series data analysis  
- Multicollinearity diagnostics (VIF)  
- Statistical visualization  
- Data transformation and stationarity handling  
- Causal inference concepts with DAGs
