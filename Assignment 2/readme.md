# Audit 02: Deconstructing Statistical Lies

## Overview
This audit investigates how common statistical metrics can mislead real-world decision-making.  
Using simulation, Bayesian reasoning, and distribution analysis, three statistical failure modes were examined:

- **Latency skew in distributed systems**
- **False positives in rare-event detection**
- **Survivorship bias in crypto markets**

The objective is to distinguish **vanity metrics** from **truthful signals**.

---

## 1. Latency Skew — When Averages Lie

### Method
- Simulated **1,000 request latencies**
  - 980 normal requests (20–50 ms)
  - 20 extreme spikes (1000–5000 ms)
- Compared:
  - **Standard Deviation (SD)**
  - **Median Absolute Deviation (MAD)**

### Findings
- **SD increased dramatically** due to a small number of extreme spikes.
- **MAD remained stable**, accurately reflecting normal system performance.

**Insight:**  
In heavy-tailed systems, SD measures **rare disasters**, not **typical behavior**.  
Robust metrics such as **median, MAD, P95, and P99 latency** provide more reliable observability.

---

## 2. False Positive Paradox — Accuracy Without Context

### Method
Applied **Bayes’ Theorem** to a plagiarism detector with:

- Sensitivity = 98%  
- Specificity = 98%  

Evaluated across cheating base rates:

- Bootcamp: **50%**
- Econ class: **5%**
- Honors seminar: **0.1%**

### Findings
Posterior probability of cheating when flagged:

- **98%** (Bootcamp)
- **~72%** (Econ)
- **~5%** (Honors)

**Insight:**  
High accuracy becomes **nearly meaningless** when the event is rare.  
False positives dominate rare-event detection, making **base rates essential** for interpretation.

---

## 3. Survivorship Bias — The Illusion of Success

### Method
- Simulated **10,000 crypto token launches** using a **Pareto (power-law) distribution**.
- Created:
  - **df_all** → full market (“graveyard”)
  - **df_survivors** → top 1% only
- Compared **mean peak market cap** between groups.
- Visualized distributions using **log-scaled histograms**.

### Findings
- The **overall market mean** remained relatively low.
- The **survivor-only mean** was dramatically inflated.

**Insight:**  
Observing only winners creates a **false narrative of universal success**.  
This bias appears across **venture capital, startups, crypto, and social-media investing**.

---

## Key Takeaways

1. **Heavy tails break classical statistics**  
   → Prefer robust metrics over mean and SD alone.

2. **Accuracy is meaningless without base rate**  
   → Bayesian reasoning is required for real interpretation.

3. **Visible winners distort reality**  
   → Always analyze the **full distribution**, not just survivors.

---

## Conclusion

Modern data systems often present **statistically correct but practically misleading** metrics.  
This audit demonstrates that:

- **Robust statistics**
- **Bayesian inference**
- **Distribution-aware visualization**

are essential for separating **signal from illusion** in technology and finance.
