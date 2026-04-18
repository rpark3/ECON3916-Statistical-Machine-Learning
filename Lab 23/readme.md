# FedSpeak Analysis — NLP on FOMC Minutes

## Objective
This project applies natural language processing and unsupervised learning to FOMC meeting minutes in order to quantify changes in Federal Reserve communication over time, measure shifts in sentiment and uncertainty, and identify recurring thematic regimes in monetary policy language.

## Methodology
- Collected and organized more than two decades of FOMC meeting minutes into a structured text corpus.
- Preprocessed the documents using standard NLP cleaning steps, including tokenization, lemmatization, and stop word removal, to isolate economically meaningful language.
- Constructed a TF-IDF document-term matrix with both unigrams and bigrams to capture not only key policy terms but also recurring multi-word expressions used in Fed communication.
- Computed dictionary-based sentiment measures using the Loughran-McDonald lexicon, with emphasis on net sentiment and uncertainty scores tailored to financial and policy text.
- Visualized the time series behavior of sentiment metrics to track how the tone of FOMC communication evolved across major macroeconomic periods.
- Applied K-Means clustering to PCA-reduced TF-IDF representations in order to identify latent groupings of FOMC documents based on linguistic similarity.
- Compared the distribution of sentiment scores in the pre-COVID and post-COVID periods to evaluate whether the pandemic marked a structural break in Fed communication style.

## Key Findings
- The text analysis indicates that FOMC communication is not stylistically uniform over time; instead, the minutes appear to sort into distinct clusters reflecting different policy environments and macroeconomic conditions.
- The clustering results suggest the emergence of regimes such as **stable expansion / normalization language**, **crisis-response communication**, and **inflation-risk / policy-tightening discussion**, with post-2020 documents more likely to separate from earlier periods due to unusually elevated macroeconomic uncertainty.
- Sentiment trends show that Fed language became materially more cautious during periods of economic stress, with uncertainty measures rising sharply around major disruptions and remaining more elevated in the post-COVID era than in much of the pre-2020 sample.
- The pre-COVID versus post-COVID comparison suggests a meaningful shift in the distribution of policy tone: post-COVID minutes appear less anchored in steady-state language and more concentrated in vocabulary associated with uncertainty, inflation pressures, labor market imbalances, and policy adjustment.
- Overall, the results show that simple NLP tools can recover economically interpretable structure from central bank text and help translate qualitative policy communication into measurable, analyzable signals.

## Interpretation
This analysis demonstrates that central bank communication can be studied as data rather than treated as purely narrative text. By combining TF-IDF representations, finance-specific sentiment scoring, and unsupervised clustering, the project shows how changes in Fed language can reveal shifts in macroeconomic conditions, policy priorities, and the broader communication strategy of monetary authorities.
