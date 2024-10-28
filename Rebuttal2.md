Dear Reviewer,

Thank you for your thoughtful review. Your insights are valuable. We address your concerns below.

# Incorporating Features into EmbCL
Preliminary experiments including node/edge features showed incredibly high, sparse dimensionality
## Sparse Embeddings/Vector Dissimilarity
- Vectors including features are too sparse
- They become mutually othogonal
- Including features destroys vector similarity measures
## Agnositicism
Omitting features provides: 
- Dataset-Agnosticism
- Scalability
- Wide Applicability
## Under-researched Structural Similarity Metrics
- Structural Similarity: significant research gaps [1]
- Feature similarity: well-explored [2]
- Composite methods using EmbCL with existing, robust feature similarity metrics are our next step
# R$_c$ Robustness 
- Consistent across models/datasets.
- Identifies when learning slows.
- We limited R$_c$ configurations in this work for clarity
- We tested 24 schedules in preliminary work (Appx Tab 4)
## Robustness thorugh Simplicity
- Compares learning rate change between last k epochs and the preceeding k epochs
- Simple but effective and trasparent.
## Existing Methods' Challenges
- Require specific tuning for model confidence and network activation [3]
- Prevents model/dataset agnosticism 
# Hyperparameter Sensitivity
Hyperparameter tuning is promising. There are certainly optimal model configurations in conjuntion with EmbCL
- Hyperparameter tuning will be highly model-specific
- We sought to demonstrate model agnosticism/wide applicability
- We include 75 experiments in this work
- 100's of preliminary explorations are in Appx Table 5
Full, model-specific hyperparameter sensitivity analysis will give insights. We plan to explore this soon.

# Figure Quality
Figures 3 and 5 have been adjusted:
- Rescaled
- Clear text
- Improved labels
- Neat layout for legibility.

Your critical feedback significantly strengthens our work. Thank you.

Best regards,
The Authors

[1] Chikwendu, I. et al. A comprehensive survey on deep graph representation learning methods, Journal of Artificial Intelligence Research, 2023
[2] Khoshraftar, S. and An A. A survey on graph representation learning methods, ACM Transactions on Intelligent Systems and Technology, 2024
[3] Bian, K, and Rahul P. Machine learning optimization techniques: a Survey, classification, challenges, and Future Research Issues, Archives of Computational Methods in Engineering, 2024
