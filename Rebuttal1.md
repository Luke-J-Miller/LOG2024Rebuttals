Dear Reviewer,

Thank you for your positive feedback and for recommending our paper for acceptance. We are pleased you found our methods promising.

# Visuals
- Figure 8's scaling has been increased to provide clearer delineation between model performance.
- It now better highlights significant, single-digit accuracy gains.

# Tables
- Tables 2 and 3 have been moved from the appendix to the main text.
- The distinct performance differences are numerically represented in the main text.

# Performance compared to FAIR
## NCI1 Performance
We used GraphSAGE and Graph Isomorphism Network (GIN) to evaluate TUDataset datasets. 
### GIN
- EmbCL attained 81.2±0.6% accuracy outcompeting FAIR's 80.0±1.4% [Errica 2020](#references).
- Recent progress on these benchmarks with light weight models has slowed [Na 2024](#references).
- While our gains are modest on NCI1, a 1% increase is significant.
### GraphSAGE
- Using GraphSAGE, EmbCL's performance (76.1%) matched FAIR's perfomance (76.0%) [Errica 2020](#references).
- However, while accuracies were similar, EmbCL has a tighter confidence interval (EmbCL: ±1.1%, FAIR: ±1.6%).

# ENZYMES Performance
We saw few gains regardless of model architecture on the ENZYMES dataset. 
- We hypothesize in the article that small datasets (100 samples per category) limit curriculum learning's (CL) effectiveness.
- Progressive data release fails to provide enough diversity in early training. 
- Models with insufficient data becoming stuck in local minima are well corrobarated in the literature [Na 2024](#ref) [Brigato 2021](#ref) [Cheng 2019](#ref).
- ## Reason for Inclusion
    - We desired to give an honest, throrough evaluation of EmbCL's performance.
    - Despite our hopes, very small datasets are still unsuitable for CL, even with EmbCL's ability to identify structural tendencies.
    - The provision of where a method does not work is necessary for rigour.  We show where EmbCL does not work, as well as its considerable strength with more suitable data.
# ogbg-ppa Performance
- EmbCL shows strong improvements on large datasets like ogbg-ppa. 
- Recent progression has stalled on this benchmark in recent years [Hu 2024](#references). 
- EmbCL beat leading methods by 4% [Hu 2024](#references) (Appendix: Figure 7, Table 2). 
- EmbCL is most effective on large datasets with high structural complexity. 

Your critical feedback significantly strengthens our work. Thank you..

Best regards,
The Authors

# References
1. Na, M., et al. [*Curriculum Learning for Small Code Language Models*](https://doi.org/10.48550/arXiv.2407.10194), Proceedings of the 62nd Annual Meeting of the Association for Computational Linguistics, 2024
1. Errica, F. et al. [*A Fair Comparison of Graph Neural Networks for Graph Classification*](https://doi.org/10.48550/arXiv.1912.09893), Proceedings of the Eighth International Conference on Learning Representations, 2020.
1. Brigato, L., and Iocchi, L. [*A Close Look at Deep Learning with Small Data*](https://doi.org/10.1109/ICPR48806.2021.9412492), 25th International Conference on Pattern Recognition, 2021
1. Cheng, H., et al. [*Local to global learning: Gradually adding classes for training deep neural networks*](https://doi.ieeecomputersociety.org/10.1109/CVPR.2019.00488), Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition, 2019
1. Hu, W. [*Leaderboards for graph property prediction*](https://ogb.stanford.390.edu/docs/leader_graphprop), Online: https://ogb.stanford.390.edu/docs/leader_graphprop, 2024
