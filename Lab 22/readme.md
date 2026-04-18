# Clustering World Economies with K-Means & PCA

## Objective
This project applies unsupervised machine learning to cross-country development data in order to identify latent economic groupings, evaluate how closely data-driven clusters align with World Bank income classifications, and compare those patterns to a second application using California housing data.

## Methodology
- Collected 10 World Bank development indicators for approximately 160 countries using the `wbgapi` package.
- Cleaned and organized the dataset so that each country was represented by a consistent vector of development and macroeconomic features.
- Standardized all variables using `StandardScaler` so that features measured on different scales contributed equally to distance calculations in K-Means.
- Fit K-Means clustering models to the country-level dataset, with an initial benchmark specification of **K = 4**.
- Reduced the standardized feature space to two principal components using PCA in order to visualize country clusters in a 2D scatter plot.
- Evaluated cluster quality across **K = 2 through K = 10** using both the **elbow method** and **silhouette analysis**.
- Compared algorithmically generated clusters with official **World Bank income classifications** through cross-tabulation to assess how strongly unsupervised groupings tracked existing economic categories.
- Applied the same preprocessing, clustering, and visualization pipeline to the **California Housing** census tract dataset to test how the workflow generalized to a domestic, subnational context.

## Key Findings
- The clustering results showed that development indicators contain enough structure for K-Means to recover meaningful economic groupings across countries.
- Model selection diagnostics indicated that **[INSERT OPTIMAL K]** provided the best balance between cluster compactness and separation.
- The resulting clusters showed **[strong / moderate / limited]** alignment with World Bank income classifications, suggesting that unsupervised learning can recover broad development tiers while also revealing heterogeneity within official income groups.
- PCA visualization showed that countries with similar development profiles tended to concentrate in identifiable regions of the reduced feature space, making the cluster structure interpretable rather than purely algorithmic.
- When extended to the California Housing dataset, the same workflow demonstrated that clustering pipelines built for international macro-development analysis can also be adapted effectively to high-dimensional regional socioeconomic data.

## Interpretation
Taken together, the results show that unsupervised learning can be a useful tool for comparative economic analysis. Rather than relying only on predefined classifications, clustering allows researchers to detect underlying patterns in development data, identify borderline or atypical cases, and assess whether institutional categories reflect the empirical structure of the data itself.
