"""
Run this script to generate README.md in the current directory.
    python write_readme.py
"""

readme = """# The Architecture of Dimensionality: Hedonic Pricing & the Frisch-Waugh-Lovell Theorem

---

| | |
|---|---|
| **Domain** | Applied Econometrics \| Real Estate Pricing |
| **Dataset** | 2026 California Real Estate Metrics (Zillow Synthetic) |
| **Variables** | `Sale_Price`, `Property_Age`, `Distance_to_Tech_Hub` |
| **Stack** | Python 3.10+ \| `pandas` \| `statsmodels.formula.api` \| `matplotlib` |
| **Theorem** | Frisch-Waugh-Lovell (FWL) Projection Theorem |

---

## Objective

To construct a multivariate hedonic pricing model for California residential real estate
using Ordinary Least Squares regression, and to formally prove the Frisch-Waugh-Lovell
(FWL) Theorem by manually extracting orthogonalized residuals — demonstrating that
multivariate OLS coefficients represent pure, ceteris paribus partial effects that are
fully immune to the confounding influence of co-linear predictors.

---

## Methodology

- **Step 1 — Full Multivariate OLS Estimation**
  - Estimated the full structural model: `Sale_Price ~ Property_Age + Distance_to_Tech_Hub`
    using `statsmodels.formula.api.ols()`, producing the multivariate partial coefficients
    β₁ and β₂ — the theoretical ground-truth benchmarks for the FWL proof.

- **Step 2 — Bivariate OLS Estimation (Baseline for OVB Diagnosis)**
  - Estimated a restricted model regressing `Sale_Price` on `Property_Age` alone,
    deliberately omitting `Distance_to_Tech_Hub` to isolate and quantify the magnitude
    of omitted variable bias (OVB) contaminating the naive coefficient estimate.

- **Step 3 — Residual Extraction via the FWL Partialling Procedure**
  - Regressed `Property_Age` on `Distance_to_Tech_Hub`; captured residuals ẽ₁ — the
    component of age orthogonal to distance (i.e., age variance unexplained by tech-hub
    proximity).
  - Regressed `Sale_Price` on `Distance_to_Tech_Hub`; captured residuals ẽ₂ — the
    component of price orthogonal to distance.

- **Step 4 — FWL Univariate Regression on Purged Residuals**
  - Regressed the purged price residuals (ẽ₂) on the purged age residuals (ẽ₁). By the
    FWL Theorem, the resulting slope coefficient must equal the multivariate partial
    coefficient β₁ — no intercept required, as both residual vectors are mean-zero by
    construction.

- **Step 5 — Numerical Verification & Visualization**
  - Tabulated all three coefficient estimates side-by-side and confirmed exact numerical
    equivalence between the FWL residual regression and the full multivariate model.
    Residual scatter plots were generated via `matplotlib` to visualize the orthogonalized
    variance structure.

---

## Key Findings

- **Severe Omitted Variable Bias Detected**
  - The bivariate model (`Sale_Price ~ Property_Age` only) produced a materially inflated
    coefficient on `Property_Age`. Because newer properties disproportionately cluster near
    tech employment hubs — and proximity independently commands a significant price premium
    — the naive model incorrectly attributed a portion of the tech-hub premium to the
    physical recency of the structure itself. This is a textbook upward OVB:
    `Cov(Property_Age, Distance_to_Tech_Hub) ≠ 0`, and the omitted variable carries a
    negative price coefficient, jointly satisfying both conditions for bias amplification.

- **FWL Theorem Formally Confirmed — Exact Coefficient Recovery**
  - The FWL residual regression recovered the multivariate partial coefficient on
    `Property_Age` with full numerical precision. Once the shared covariance between
    `Property_Age` and `Distance_to_Tech_Hub` was surgically removed via the partialling
    procedure, the residual-on-residual slope collapsed to the true ceteris paribus effect
    — mathematically proving that OLS, in higher dimensions, is executing this
    orthogonalization procedure implicitly and simultaneously for all regressors.

- **Algorithmic Ceteris Paribus Proven**
  - The experiment provides a rigorous empirical demonstration that a multivariate OLS
    coefficient does not merely "control for" covariates in a loose statistical sense — it
    literally projects out their influence from both the dependent variable and the
    regressor of interest before estimating the slope. The FWL Theorem reframes multivariate
    regression not as a black-box correction mechanism, but as a sequence of explicit
    geometric projections onto orthogonal subspaces, each isolating a predictor's unique
    explanatory signal.

---

*Econometrics Lab | 2026 | California Real Estate Metrics*
"""

with open("README.md", "w", encoding="utf-8") as f:
    f.write(readme)

print("README.md written successfully.")
