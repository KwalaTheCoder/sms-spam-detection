# Audit and refactor

Splits raw messages before learning TF-IDF; vectorization is fitted separately inside each CV fold. Keeps sparse word/bigram features, removing dense .toarray(), scaling, SMOTE and external NLTK corpus downloads. Compares Complement Naive Bayes with class-weighted logistic regression and a dummy baseline. Duplicate messages are grouped to prevent cross-split contamination.

Original algorithms and historical outputs remain in legacy/. No production dataset was available during refactoring; new real-data metrics remain unmeasured. See README.md for the reproducible evaluation protocol.
