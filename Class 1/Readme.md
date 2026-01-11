## 🌍 Global Purchasing Power Parity Analysis via the Big Mac Index

### Project Title  
**Global Purchasing Power Parity Analysis**

### Objective  
To empirically test the **Law of One Price** by using the Big Mac Index as a proxy for cross-country purchasing power parity (PPP) and identifying currency misalignments relative to the US Dollar.

### Methodology  
- Constructed a raw dataset from *The Economist’s* 2015 Big Mac Index data using manually defined Python dictionaries.  
- Ingested and structured the data using Pandas for transparent, reproducible analysis.  
- Computed **implied PPP exchange rates** by comparing local Big Mac prices to the US benchmark price.  
- Calculated **currency valuation gaps** by measuring percentage deviations between implied PPP rates and actual market exchange rates.  
- Interpreted deviations as indicators of **overvaluation**, **undervaluation**, and potential **arbitrage signals**.

### Key Findings  
The analysis revealed meaningful departures from purchasing power parity across countries.  
For example, **[INSERT YOUR RESULT HERE — e.g., “the Norwegian Krone appeared significantly overvalued relative to the US Dollar, while several emerging market currencies showed persistent undervaluation”]**.  

These deviations highlight real-world frictions — including trade barriers, local cost structures, and market inefficiencies — that prevent immediate price equalization, demonstrating why absolute PPP rarely holds in practice despite its theoretical foundation.
