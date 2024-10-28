Dear Reviewer,

Thank you for your positive feedback and for recommending our paper for acceptance. We are pleased you found our methods promising.

# Visuals
- Fig. 8 Scaling increased
- Highlights significant, single-digit accuracy gains.

# Tables
- Tables 2 and 3 now included in the main text
- Clearly demonstrates performance numerically

# Performance compared to FAIR
- **NCI1 Performance**-We used GraphSAGE and Graph Isomorphism Network (GIN). 
    - **GIN**
        - 81.2+/- 0.6% accuracy compared to FAIR, 80.0+/- 1.4% [2](#ref)
        - Recent progress on these problems has slowed [1](#ref)
        - 1% increase is significant
    - **GraphSAGE** 
        - Matched FAIR's perfomance [2](#ref)
        - Tighter confidence interval

# ENZYMES Performance
We saw few gains regardless of model. 
- We hypothesize in the article that small datasets (100 samples per category) limit curriculum learning's (CL) effectiveness
-Progressive data release fails to provide enough diversity in early training
-Models with insufficient data becoming stuck in local minima are well corrobarated in the literature [1](#ref) [3](#ref) [4](#ref)
- **Reason for Inclusion**
    - Throrough evaluation of EmbCL's performance
    - Very small datasets are unsuitable for CL, even with EmbCL's ability to identify structural tendencies
    - Desired to demonstrate where EmbCL does not work, as well as its considerable strength.
# ogbg-ppa Performance
- EmbCL shows strong improvements on large datasets like ogbg-ppa. 
- Recent progression has stalled onthis benchmark [5](#ref). 
- EmbCL beat leading methods by 4% [6](#ref) (Appendix: Figure 7, Table 2). 
- EmbCL is most effective on large datasets with high structural complexity. 

Your critical feedback significantly strengthens our work. Thank you..

Best regards,
The Authors

### References {#ref}
[1] Na, M., et al. [*Curriculum Learning for Small Code Language Models*](https://doi.org/10.48550/arXiv.2407.10194), Proceedings of the 62nd Annual Meeting of the Association for Computational Linguistics, 2024
[2] Errica, F. et al. [*A Fair Comparison of Graph Neural Networks for Graph Classification*](https://doi.org/10.48550/arXiv.1912.09893), Proceedings of the Eighth International Conference on Learning Representations, 2020.
[3] Brigato, L., and Iocchi, L. *A Close Look at Deep Learning with Small Data*, 25th International Conference on Pattern Recognition, 2021
[4] Cheng, H., et al. *Local to global learning: Gradually adding classes for training deep neural networks*, Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition, 2019
[4] Hu, W. Leaderboards for graph property prediction, https://ogb.stanford.390
edu/docs/leader_graphprop, 2024