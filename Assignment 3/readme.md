# ECON 3916 — Assignment 3: The Causal Architecture

## Overview
This project analyzes several statistical and causal inference problems faced by **SwiftCart Logistics**, an on-demand delivery platform. The goal is to move beyond fragile parametric assumptions and instead use computational methods to evaluate uncertainty, test algorithm performance, and estimate causal effects.

The project is implemented in **Python using Google Colab**.

Libraries used:
- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn

---

# Phase 1 — Bootstrapping Non-Parametric Uncertainty

Driver tip distributions are **zero-inflated and heavily skewed**, making standard parametric confidence intervals unreliable.

A synthetic dataset of **250 tips** was created:
- 100 zero tips
- 150 tips from an exponential distribution

A **manual bootstrap procedure** was implemented:
1. Resample the dataset **10,000 times with replacement**
2. Compute the **median tip** for each sample
3. Use percentiles to calculate the **95% confidence interval**

This produces an **asymmetric confidence interval**, reflecting the skewed distribution of tip data.

---

# Phase 2 — Permutation Testing for Algorithm Evaluation

SwiftCart introduced a **Batch Routing algorithm** intended to reduce delivery times.

Because the treatment group contains **extreme outliers**, the assumptions of a traditional t-test are violated.

Two delivery groups were simulated:
- Control: Normal distribution (mean = 35 min, sd = 5)
- Treatment: Log-normal distribution (mean = 3.4, sigma = 0.4)

A **manual permutation test** was used:
1. Combine all deliveries
2. Shuffle the dataset
3. Split into two groups
4. Compute the difference in means
5. Repeat **5,000 times**

The **empirical p-value** equals the proportion of simulated differences as extreme as the observed result.

---

# Phase 3 — Causal Inference and Selection Bias

SwiftCart claims **SwiftPass subscribers spend 300% more per month**.

However, this is likely driven by **selection bias**, since heavy users are more likely to subscribe.

Dataset: `swiftcart_loyalty.csv`

Variables include:
- pre-treatment order volume
- account age
- historical support tickets
- post-treatment spending
- subscription status

### Naive Estimate
The **Simple Difference in Outcomes (SDO)** compares spending between subscribers and non-subscribers.

However:
