# Exploratory Cross-Lingual Baseline Comparison

Predictions use the repository Track 1 Affinity Propagation baseline with the listed encoder. New-period gold labels were masked during prediction. ARI and NMI are averaged across target words; Official Macro-F1 follows the scorer. Novel-sense precision/recall/F1 are micro-averaged binary scores over new-period usages, where a sense is novel if it is absent from that word's old-period inventory.

**Caution:** Finnish and Russian are development splits; German is the surprise-language test split. Treat German as a separate test-only result, not a dev-set comparison. These are exploratory runs, not the official leaderboard baseline.

| Language   | Split           | Model        |   New_usages |   Target_words |     ARI |   Official_Macro_F1 |    NMI |   Novel_precision_micro |   Novel_recall_micro |   Novel_F1_micro |
|:-----------|:----------------|:-------------|-------------:|---------------:|--------:|--------------------:|-------:|------------------------:|---------------------:|-----------------:|
| Finnish    | Dev             | LEALLA-large |         3351 |            254 |  0.0220 |              0.2217 | 0.1091 |                  0.1867 |               0.4898 |           0.2703 |
| Finnish    | Dev             | mBERT        |         3351 |            254 |  0.0099 |              0.2325 | 0.0968 |                  0.1914 |               0.4086 |           0.2607 |
| Russian    | Dev             | LEALLA-large |         1605 |            201 |  0.0982 |              0.2740 | 0.4353 |                  0.6331 |               0.7415 |           0.6830 |
| Russian    | Dev             | mBERT        |         1605 |            201 |  0.0503 |              0.3076 | 0.4546 |                  0.7053 |               0.4615 |           0.5580 |
| German     | Test (surprise) | LEALLA-large |          568 |             24 |  0.0221 |              0.1257 | 0.1578 |                  0.2922 |               0.7627 |           0.4225 |
| German     | Test (surprise) | mBERT        |          568 |             24 | -0.0042 |              0.1617 | 0.1240 |                  0.2635 |               0.6186 |           0.3696 |
