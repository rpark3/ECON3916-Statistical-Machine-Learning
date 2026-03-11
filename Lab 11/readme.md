# Data Wrangling & Engineering Pipeline

## Objective
Built a preprocessing pipeline to transform a noisy HR-economics dataset into a model-ready analytical base table through structured missing-data diagnostics, categorical feature engineering, and multicollinearity-aware encoding.

## Methodology
- Audited the raw `messy_hr_economics.csv` dataset to identify data quality issues, variable types, missing-value patterns, and high-cardinality categorical fields.
- Used `missingno` and pandas-based diagnostics to map the structure of missingness and assess whether incomplete observations were consistent with a Missing At Random (MAR) process.
- Cleaned and standardized variables to improve consistency across numeric and categorical fields prior to modeling.
- Engineered categorical features using encoding strategies appropriate to variable structure and downstream econometric use.
- Prevented perfect multicollinearity during dummy encoding by dropping a reference class, avoiding the Dummy Variable Trap in regression design matrices.
- Applied target encoding to high-cardinality geographic variables to retain predictive signal while reducing dimensionality and noise.
- Prepared the final feature set for econometric modeling using a workflow built with Python, `pandas`, `statsmodels`, `missingno`, and `category_encoders`.

## Key Findings
The lab demonstrated how careful preprocessing materially improves econometric model readiness in messy real-world data. Missingness diagnostics suggested that several incomplete fields followed a structured MAR pattern rather than purely random absence, which justified informed imputation and feature treatment. The pipeline also successfully avoided perfect multicollinearity by using a dropped reference category during dummy construction, preserving valid regression specification. Finally, high-cardinality geographic information was efficiently compressed through target encoding, allowing location-based variation to be captured without exploding the dimensionality of the dataset.
