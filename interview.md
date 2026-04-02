Q1: Conceptual - Tree Count Trade-offs
If a Random Forest with 100 trees performs identically to one with 1000 trees, you should not use 1000 trees. The trade-offs are:

Compute Cost: Training 1000 trees takes roughly 10x more CPU cycles and memory during the training phase.
Prediction Latency: In production, every prediction requires traversing every tree. 1000 trees will be significantly slower, which is critical for real-time applications.
Marginal Improvement: Once the error rate stabilizes (converges), adding more trees provides diminishing returns and does not improve generalization.
Production Deployment: Larger models result in larger serialized file sizes (e.g., .pkl or .joblib), leading to slower container startup times and higher memory footprints in cloud environments.

Q3: Debug - Feature Importance Variance
There are two primary reasons why feature importance rankings might change drastically between runs:

Missing Random Seed (random_state): Random Forests use bootstrap sampling and random feature selection at each split. Without a fixed random_state, the trees are built differently every time, leading to different Gini importance values.
Correlated Features: If two features are highly correlated, the model might arbitrarily pick one over the other in different runs. Because they provide similar information, the 'credit' for the split is split between them inconsistently across different random initializations.
