Dear Reviewer,

Thank you for your thoughtful review. Your insights are valuable. We address your concerns below.

# Incorporating Features into EmbCL
Preliminary experiments including node/edge features showed incredibly high, sparse dimensionality.
## Sparse Embeddings/Vector Dissimilarity
- Embedding vectors including features are too sparse. Most elements in an embedding are 0, and vectors share very few dimensions.
- The sparsity causes vectors to become mutually othogonal which destroys vector similarity measures [Chakraborty 2021](#references).
- Omitting features provides: 
  - Dataset-Agnosticism
  - Scalability
  - Wide Applicability
## Under-researched Structural Similarity Metrics
- Structural Similarity: There are significant research gaps in characterizing the distribution of graph structures [Chikwendu 2023](#references).
- Feature similarity: Conversely, measures of feature distibutions are well-explored [Khoshraftar 2024](#references).
- While the Weisfelier-Leman embedding is incompatible with feature inclusion, bivariate measures of EmbCL and established techniques are promising, and represent one of the next steps in our research.
# R_c Robustness 
- R_c is consistent across models/datasets since it does not consider model hyperparameters, confidence scores, or weights, but only the rate of change of the learning rate.
- It is effective at identifying inflection points where the model is receiving diminishing returns on the current subset of data.
- We limited R$_c$ configurations in this work for clarity and space considerations. Eager as we were, we could only discuss so many aspects of our research in the limited space of a conference paper.
- However, we conducted a much more rigorous analysis of how R_c variables affected training in preliminary research. We include 24 tested configurations in the appendix (Appx Tab 4).
## Robustness thorugh Simplicity
- The simplicity of the method provides agnosticism. Comparing the change in learning rate change between last k epochs and the preceeding k epochs as a ratio is universally applicable.
- The ease of implementation provides a transparent metric in a space where explainability is a frequent challenge.
## Existing Methods' Challenges
- While powerful methods exist for evaluating momentum, they require specific tuning for model confidence and network activation between disparate architectures [Bian 2024](#references).
- This individual tuning prevents fast iteration of models and model-specific hyperparameters and reduces the ability to experiment.
# Hyperparameter Sensitivity
Hyperparameter tuning is promising. There are certainly optimal model configurations in conjuntion with EmbCL
- Hyperparameter tuning will be highly model-specific [Bischl 2023](#references)
- We sought to demonstrate model agnosticism/wide applicability, although we are eager to exploit performance gains by optimizing on specific architectures.
- We include 75 experiments in this work evaluating EmbCL's performance on a wide array of datasets and models.
- Addtionally, 100's of preliminary explorations are in Appx Table 5
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

# References
1. Chakraborty, S. and Zhang X. [*A new framework for distance and kernel-based metrics in high dimensions*](10.1214/21-EJS1889) Electronic Journal of Statistics, 2021
1. Chikwendu, I. et al. [*A comprehensive survey on deep graph representation learning methods*](https://doi.org/10.1613/jair.1.14768), Journal of Artificial Intelligence Research, 2023
1. Khoshraftar, S. and An A. [*A survey on graph representation learning methods*](https://doi.org/10.1145/3633518), ACM Transactions on Intelligent Systems and Technology, 2024
1. Bian, K, and Rahul P. [*Machine learning optimization techniques: a Survey, classification, challenges, and Future Research Issues*](https://link.springer.com/article/10.1007/s11831-024-10110-w), Archives of Computational Methods in Engineering, 2024
1. Bischl, B et al. [*Hyperparameter optimization: Foundations, algorithms, best practices, and open challenges*]( https://doi.org/10.1002/widm.1484) Wiley Interdisciplinary Reviews: Data Mining and Knowledge Discovery, 2023
