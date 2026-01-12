## 🌍 Global Purchasing Power Parity Analysis via the Big Mac Index

### Project Title  
**Global Purchasing Power Parity Analysis via the Big Mac Index**

### Objective  
To empirically test the **Law of One Price** by using the Big Mac Index as a proxy for Purchasing Power Parity (PPP) and identifying systematic currency misalignments relative to the US Dollar.

### Data Source  
Raw price data from **The Economist Big Mac Index (January 2015 edition)**, manually structured into a custom dataset.

### Methodology  
- Manually constructed a dataset from raw Big Mac price data using Python dictionaries.  
- Ingested and organized the data using Pandas for transparent data handling.  
- Calculated **implied PPP exchange rates** by comparing local Big Mac prices to the US benchmark price.  
- Computed **percentage currency misalignment** by measuring deviations between implied PPP rates and observed market exchange rates.  
- Interpreted deviations as evidence of **overvaluation**, **undervaluation**, and limits to international price arbitrage.

### Key Findings  
The results show clear departures from absolute Purchasing Power Parity.  
The January 2015 data indicates that the **Norwegian Krone was significantly overvalued** against the US Dollar, while the **Chinese Yuan appeared undervalued**, consistent with structural cost differences and the **Balassa–Samuelson effect**.  

These findings highlight real-world frictions — including non-tradable input costs, local wage structures, and market segmentation — that prevent the Law of One Price from holding exactly, even in standardized consumer goods markets.

### Tools Used  
Python, Pandas, Seaborn, Matplotlib
