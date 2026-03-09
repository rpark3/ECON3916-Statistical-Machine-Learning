# Assignment 3: The Causal Architecture
**Module 3 — Bootstrapping, Permutation, & Causal Inference**  
**Course:** ECON 3916  
**Role:** Senior Data Economist  
**Platform:** Google Colab  

---

# Project Overview

This project investigates three key analytical questions faced by **SwiftCart Logistics**, a multinational on-demand delivery platform:

1. **Driver compensation equity** — Are public claims about median driver tips statistically reliable?
2. **Routing algorithm performance** — Does the new batch-routing algorithm truly reduce delivery times?
3. **SwiftPass subscription ROI** — Does the loyalty program actually increase user spending, or is the observed effect driven by selection bias?

Rather than relying on fragile parametric assumptions, this analysis uses **computational inference methods** and **causal econometrics** to produce empirical evidence.

The assignment is divided into four phases:

- Bootstrapping non-parametric uncertainty
- Permutation testing for algorithm validation
- Propensity Score Matching to control for selection bias
- AI-assisted visualization of causal balance

---

# Computational Environment

This project was developed in **Google Colab** using Python.

Libraries used:

- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn

Important constraint:

High-level statistical libraries such as `scipy.stats.bootstrap` or `scipy.stats.permutation_test` were **not used** in Phases 1 and 2.  
All resampling procedures were implemented manually using loops and NumPy.

---

# Phase 1 — Bootstrapping Non-Parametric Uncertainty

## Problem

Driver tip distributions in gig-economy platforms are **zero-inflated and highly right-skewed**.  
Many deliveries receive **$0 tips**, while a small number receive large tips.

Because of this distribution, **standard parametric confidence intervals are unreliable**.

## Data Generation

A synthetic dataset of **250 tips** was generated:

- 100 zero tips
- 150 tips drawn from an exponential distribution

```python
np.random.seed(42)

zeros = np.zeros(100)
tips = np.random.exponential(scale=5.0, size=150)

driver_tips = np.concatenate([zeros, tips])
