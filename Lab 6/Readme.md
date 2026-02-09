# Lab 5: The Architecture of Bias

## Overview
This lab investigates the **Data Generating Process (DGP)** and **Sampling Bias** in machine learning systems, demonstrating how seemingly minor architectural decisions can introduce systematic distortions that compromise model validity.

## Objectives
- Understand the relationship between sampling methodology and statistical reliability
- Detect and mitigate Covariate Shift through stratified sampling techniques
- Perform forensic audits on A/B test infrastructure using Sample Ratio Mismatch (SRM) detection
- Recognize structural biases in observational data and their corrections

## Tech Stack
- **Python** – Primary programming language
- **pandas** – Data manipulation and analysis
- **numpy** – Numerical computing and random sampling
- **scipy** – Chi-Square tests for SRM forensic analysis
- **sklearn** – Stratified sampling implementation

## Methodology

### 1. Simple Random Sampling (SRS) – Variance Analysis
Manually simulated Simple Random Sampling on the Titanic dataset to demonstrate the trade-off between unbiased estimation and high sampling error. By repeatedly drawing random samples and calculating survival rates, I quantified the **variance** inherent in non-stratified approaches—particularly problematic when class distributions are imbalanced.

**Key Finding:** SRS produces unbiased estimates but exhibits high variance due to underrepresentation of minority classes across samples.

### 2. Stratified Sampling – Eliminating Covariate Shift
Implemented **Stratified Sampling** using `sklearn.model_selection.train_test_split` with `stratify` parameter to preserve class proportions across train/test splits. This approach:
- Maintains identical class distributions between population and sample
- Eliminates **Covariate Shift** (P(X) changes but P(Y|X) remains constant)
- Reduces variance while maintaining unbiasedness

**Technical Implementation:**
```python
from sklearn.model_selection import train_test_split

train, test = train_test_split(
    titanic_df, 
    test_size=0.3, 
    stratify=titanic_df['Survived'],
    random_state=42
)
```

### 3. Sample Ratio Mismatch (SRM) Forensic Audit
Conducted **Chi-Square goodness-of-fit tests** to detect infrastructure failures in A/B test randomization. Using `scipy.stats.chisquare`, I tested whether observed group assignments deviated significantly from expected 50/50 allocation.

**SRM Detection Criteria:**
- If p-value < 0.01 → **CRITICAL FAILURE** (systematic randomization bug)
- Else → Natural sampling variation

**Real-World Impact:** SRM detection prevents analysis of compromised experimental data, saving teams from drawing invalid causal conclusions due to load balancer bugs, caching issues, or faulty hashing algorithms.

---

## Theoretical Deep Dive: Survivorship Bias in Unicorn Analysis

### The Problem: Why TechCrunch Creates "Ghost Data"

**Scenario:** Analyzing only successful unicorn startups (those featured on TechCrunch) to identify traits that predict success.

**Why This Causes Survivorship Bias:**

TechCrunch only covers **survivors**—startups that achieved unicorn status. This creates a **censored dataset** where failures are systematically excluded. The problem isn't that successful startups are unrepresentative; it's that we **observe only one side of a conditional distribution**:

- **What we see:** P(Traits | Success = 1)
- **What we need:** P(Success = 1 | Traits)

By Bayes' theorem, these are equal only if **P(Traits)** is identical in both successful and failed populations—an assumption that's almost certainly false.

### The "Ghost Data" You Need: Selection Equation Variables

To apply a **Heckman Correction** (two-stage sample selection model), you need variables that predict **selection into the observed sample** (i.e., which startups get media coverage) but don't directly affect the outcome of interest.

**Specific Ghost Data Required:**

1. **Exclusion Restriction Variables** (predict visibility, not success):
   - Founder's social media following *before* launch
   - PR budget or agency relationship
   - Geographic proximity to major tech hubs (SF, NYC, Boston)
   - Participation in high-profile accelerators (Y Combinator, Techstars)
   - Previous media appearances of founding team

2. **The Full Population** (both visible and invisible):
   - Startups that failed before gaining media attention
   - Successful bootstrapped companies that avoid press
   - Companies in "unsexy" industries (B2B SaaS for niche verticals)
   - International startups not covered by US tech media

### How Heckman Correction Works

**Stage 1 (Selection Equation):**
Model P(Covered by TechCrunch | Founder Twitter Followers, PR Budget, YC Alumni, ...)

**Stage 2 (Outcome Equation):**
Model P(Unicorn Status | Business Traits, **Inverse Mills Ratio from Stage 1**)

The Inverse Mills Ratio (λ) corrects for the fact that startups appearing in your dataset are **non-randomly selected**. Without this correction, you'd confound "traits that predict success" with "traits that predict media coverage."

### Example of Distortion

Suppose aggressive PR spending correlates with media coverage but *negatively* correlates with product focus. A naive analysis might conclude:

> "Unicorns had strong PR presence early on" ✗

When the truth is:

> "We only observed startups with strong PR presence; among those, excessive PR spending may have *decreased* success probability" ✓

---

## Key Takeaways

1. **Sampling methodology is architecture** – The way data enters your pipeline determines what questions you can answer
2. **Stratification reduces variance** – When class labels are available, always stratify to preserve population structure
3. **Infrastructure failures masquerade as data** – SRM detection prevents analyzing corrupted experiments
4. **Observability ≠ Randomness** – Selection bias requires modeling the **visibility process itself**

## Skills Demonstrated
- Statistical hypothesis testing (Chi-Square goodness-of-fit)
- Bias detection and mitigation in ML pipelines
- Understanding of causal inference prerequisites (Heckman selection models)
- Practical application of sampling theory to real-world datasets

---

**Author's Note:** This lab reinforced that "more data" doesn't solve bias—only **better data architecture** does. Whether it's stratifying samples, auditing randomization, or modeling selection mechanisms, the goal is the same: ensure your dataset reflects the **Data Generating Process** you actually care about, not just the one that's easiest to observe.
