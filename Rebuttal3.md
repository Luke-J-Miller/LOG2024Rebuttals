Dear Reviewer,
Thank you for your constructive review and acknowledging the novelty of our method. We address your comments below with analysis, results, and citations.

# Abstract
- The abstract now explicitly emphasizes prior works' limitations. 
    - Computational inefficiency
    - Extensive hyperparameter tuning
    - Data augmentation in graph-level CL
    - Discussion of graph-level CL models' sensitivity to these aspects [Guo 2023](#refernces)
- We explicitly address the research gap in CL based on graph structures. 
- We clearly argue our method efficiently characterizes graph structures.
# Rationale for Weisfeiler-Leman (WL) Graph Kernels
- The WL kernel is a powerful isomorphim test.
- It is deterministic and expressive in capturing structures in large datasets [Morris 2023](#refernces).
- Random walks/tree embeddings possess significant stochastic variation due to their sampling nature that fails to consider the entire graph [Kim 2024](#references).
- WL kernels are more efficient than common subgraph approaches [Fürer 2017](#refernces)
  - EmbCL linearly scales to large datasets (Figure 2).
  - Other methods are quadratic or cubic in time complexity [Kim 2024](#references) [Willis 2020](#refernces).
# Limitations of Other Methods
We include a new section highlighting existing methods' failures.
- Simplistic graph invariants are insufficient proxies for graph difficulty [Willis 2020](#refernces).
- Other methods do not quantify and enumerate the entirety of graph structures [Willis 2020](#refernces).
- Their complexity makes them not scalable to massive datasets. 
- Figs 7 and 8 illustrate our approach outperforms baseline models by up to 5% on difficult tasks involving large graph datasets.
# Overall Structure
- The introduction now motivates our use of the WL kernel in curriculum learning
- Contrastive learning is introduced cohesively, and it is thoroughly explained in its relation to EmbCL.
- We include how EmbCL considers both similarity and differences when measuring structures between contrasting graphs.
#Figure Quality
Figures 3 and 5 have been adjusted as suggested:
- Rescaled
- Clear text
- Improved labels
- Neat layout for legibility

Your critical feedback significantly strengthens our work. Thank you.

Best regards,
The Authors

# References
1. Guo, Y et al [*Data-centric Graph Learning: A Survey*](https://doi.org/10.48550/arXiv.2310.04987), arXiv e-prints, 2023
2. Kim, J et al [*Revisiting Random Walks for Learning on Graphs*](10.48550/arXiv.2407.01214) ICML 2024 Workshop on Geometry-grounded Representation Learning and Generative Modeling, 2024
3. Morris, C. et al [*Glocalized weisfeiler-lehman graph kernels: Global-local feature maps of graphs*](10.1109/ICDM.2017.42), IEEE ICDM, 2023
4. Fürer, M. [*On the combinatorial power of the Weisfeiler-Lehman algorithm*](https://link.springer.com/chapter/10.1007/978-3-319-57586-5_22), International Conference on Algorithms and Complexity, 2017
5. Wills, P, and Meyer, F. [*Metrics for graph comparison: a practitioner’s guide*](https://doi.org/10.1371/journal.pone.0228728), Plos one, 2020
