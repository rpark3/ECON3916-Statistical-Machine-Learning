# Causal ML — Double Machine Learning for 401(k) Policy Evaluation

## Objective
This project applies modern causal machine learning methods to estimate the effect of 401(k) eligibility on household net financial assets, while addressing regularization bias in high-dimensional settings and exploring treatment effect heterogeneity across income groups.

## Methodology
- Began with a simulated data-generating process to illustrate a core identification problem in causal ML: when LASSO is applied naively in a treatment-outcome setting, regularization can shrink the treatment coefficient toward zero and bias causal estimates downward, even when the true effect is known.
- Used this bias demonstration to motivate a Double Machine Learning (DoubleML) framework designed to separate prediction from causal estimation.
- Implemented a **Partially Linear Regression (PLR)** specification within the DoubleML framework on 401(k) pension plan data.
- Estimated nuisance functions with **Random Forest** learners in order to flexibly model both the outcome and treatment assignment processes without imposing restrictive linearity assumptions.
- Applied **5-fold cross-fitting** to reduce overfitting and orthogonalize the treatment effect estimate from machine learning errors in the nuisance models.
- Estimated the **Average Treatment Effect (ATE)** of 401(k) eligibility on net financial assets.
- Extended the analysis to **Conditional Average Treatment Effects (CATEs)** by income quartile to evaluate whether the policy effect differed systematically across the income distribution.
- Visualized subgroup CATE estimates with confidence intervals to compare both effect size and statistical precision across income-based strata.

## Key Findings
- The simulation exercise confirmed that naïve regularized regression is not a reliable causal estimator: LASSO materially attenuated the treatment coefficient toward zero despite a true underlying effect of **5.0**, demonstrating regularization bias in a causal setting.
- By contrast, the DoubleML PLR approach produced a policy-relevant estimate of the effect of 401(k) eligibility on net financial assets while using flexible machine learning methods for nuisance estimation.
- The estimated **ATE** was **[INSERT ATE]**, indicating that 401(k) eligibility is associated with a meaningful increase in household net financial assets.
- The **CATE** analysis showed that treatment effects were **[INSERT PATTERN: relatively stable across quartiles / increasing with income / strongest in middle-income groups / weakest in the lowest quartile, etc.]**.
- Across income quartiles, estimated effects ranged from **[INSERT LOWEST CATE]** to **[INSERT HIGHEST CATE]**, with confidence intervals indicating **[INSERT WHETHER DIFFERENCES WERE SHARP OR MODEST]**.
- Overall, the results suggest that access to tax-advantaged retirement saving vehicles can increase asset accumulation, but that the magnitude of the effect may vary depending on household income and underlying financial capacity.

## Interpretation
This project shows why causal inference requires more than strong predictive performance. In policy settings such as retirement saving, machine learning methods must be combined with identification strategies that protect against regularization bias and overfitting. Double Machine Learning provides that structure, allowing flexible nuisance estimation while preserving valid inference on the treatment effect of economic policy.
