# The Cost of Living Crisis: A Data-Driven Analysis

## The Problem: Why the “Average” CPI fails students
The official Consumer Price Index (CPI) is designed to reflect the spending patterns of an average urban consumer, not students.  
Students allocate a disproportionate share of their budget to rent, tuition, food away from home, and subscriptions—categories that have experienced inflation rates that differ significantly from the national average. As a result, headline CPI systematically understates the true cost-of-living pressures faced by students.

---

## Methodology: Python, APIs, and Index Theory (Laspeyres)
**Tools:** Python, fredapi, pandas, matplotlib

**Process:**
- Retrieved CPI component series from the Federal Reserve’s FRED database, including:
  - Tuition & education
  - Rent (shelter)
  - Food away from home (proxy for everyday student consumption)
  - Streaming services
  - Official CPI (all urban consumers)
- Constructed a **Student Price Index (SPI)** using a **Laspeyres index framework**, holding student-relevant expenditure weights constant over time.
- Normalized all series to **Jan 2016 = 100** to enable direct comparison of inflation trajectories.
- Visualized:
  - Component-level inflation vs official CPI
  - Student SPI vs official CPI with an “inflation gap”
  - Raw (non-normalized) CPI series to illustrate why normalization is necessary
  - National CPI vs Boston CPI vs Student SPI to isolate regional effects

---

## Key Findings
- By the end of the sample period, the Student Price Index reached **141.05**, while the Official CPI reached **137.19** (2016 = 100).
- This implies a **2.8% cumulative divergence** between student inflation and national inflation.
- Regional inflation does not fully explain the gap: Boston CPI closely tracks national CPI, while student costs continue to rise faster.
- The divergence is driven primarily by rent and food-away-from-home, which carry higher weights in the student consumption basket than in the official CPI.

---

## Implications
This analysis demonstrates that aggregate inflation metrics can mask significant subgroup-level disparities.  
For students, the effective inflation rate is persistently higher than the national average, suggesting that policies and financial aid indexed to headline CPI may underestimate real cost-of-living increases.

---

## Stack & Concepts
- Python (pandas, matplotlib, fredapi)
- CPI decomposition and normalization
- Laspeyres index construction
- Regional vs national inflation comparison
- Cost-of-living measurement bias
