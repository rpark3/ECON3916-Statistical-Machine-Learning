# The Illusion of Growth & the Composition Effect

## Objective
This project analyzes long-run U.S. wage stagnation by combining nominal wage data with inflation adjustments and correcting for statistical biases in standard wage measures. Using live economic data from the Federal Reserve API, the analysis distinguishes real purchasing power trends from misleading nominal growth and pandemic-era distortions.

## Methodology
- Built a Python data pipeline using the Federal Reserve Economic Data (FRED) API to ingest live macroeconomic time-series data.
- Retrieved nominal hourly wage data (AHETPI) and Consumer Price Index (CPI) data to construct an inflation-adjusted real wage series.
- Identified a sharp anomaly in 2020 where real wages appeared to spike despite deteriorating labor market conditions.
- Corrected for the composition effect by incorporating the Employment Cost Index (ECI), a fixed-weight wage measure that controls for changes in workforce composition.
- Rebased and visualized wage series to directly compare biased averages against composition-adjusted labor cost growth.

## Key Findings — The Pandemic Paradox
- Real wages have remained largely flat over the past five decades despite sustained nominal wage growth, illustrating the persistence of the money illusion.
- The apparent wage surge in 2020 was not driven by increased labor demand or productivity gains.
- Instead, the spike was a statistical artifact caused by the disproportionate exit of low-wage workers from the labor force during the pandemic.
- The Employment Cost Index shows steady growth through 2020, confirming that the observed wage “boom” reflected measurement bias rather than genuine improvements in worker compensation.
