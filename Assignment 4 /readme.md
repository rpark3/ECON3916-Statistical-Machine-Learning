# OmniCare Analytics — Dynamic Medical Pricing & Patient Risk

## Overview
This project rebuilds a predictive pricing algorithm for elective imaging procedures (MRIs, CT scans) from statistical first principles. The goal is to identify and fix data issues that were causing volatile and legally problematic pricing recommendations.

## Files
- `OmniCare_Clinical_Vitals.csv` — patient physiological data
- `OmniCare_Telemetry_Data.csv` — remote wearable monitoring data

## Libraries Used
- pandas
- numpy
- statsmodels
- missingno
- category_encoders
- matplotlib
- seaborn

## Project Breakdown

### Phase 1 — Causal Topology and Multicollinearity Forensics
- Identified omitted variable bias using a Fork DAG structure with socioeconomic status as the confounder
- Ran a VIF audit on physiological features and dropped BMI due to multicollinearity

### Phase 2 — Visual Forensics and High-Cardinality Encoding
- Generated a missingness matrix and classified missing heart rate data as MNAR
- Explained the dummy variable trap with 850 ICD-10 codes and why it breaks OLS
- Applied target encoding to reduce 850 diagnosis codes down to one continuous feature

### Phase 3 — OLS Prediction Engine
- Merged datasets and built a final clean dataframe
- Fit an OLS model using Patsy formula syntax
- Calculated RMSE in dollars to quantify financial risk
- Ran residual diagnostics to check for heteroscedasticity

### Phase 4 — AI Context Engineering
- Used the P.R.I.M.E. prompting framework to generate White's Lagrange Multiplier Test
- Tested and executed the AI-generated code to confirm heteroscedasticity findings

## How to Run
1. Open Google Colab
2. Upload both CSV files
3. Run each phase sequentially
"""

with open("README.md", "w") as f:
    f.write(readme)

print("README.md created")
