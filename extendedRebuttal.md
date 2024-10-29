# Introduction
The extended character limit provided by the Learning on Graphs Conference allows us to offer a more thorough response to the reviewers' insightful feedback. Each reviewer’s unique perspective helped us identify areas for improvement, enhancing the work from multiple angles. This expanded rebuttal consolidates all updates and corrections, offering detailed justifications for each change made to the paper. We are sincerely grateful to all reviewers for their constructive input, which has strengthened our paper’s suitability for inclusion in the 2024 Learning on Graphs Conference.

In this rebuttal, we address each major theme raised in the reviews:

1. Expanded Performance Analysis – We provide a comprehensive breakdown of EmbCL’s performance across key datasets (D&D, ENZYMES, and NCI1), with new figures and tables illustrating the model’s adaptability and robustness across varied data conditions.

1. Rationale for Embedding Choices – To clarify the design decisions behind EmbCL, we expand on the rationale for focusing on structure-based embeddings. We discuss the limitations of incorporating node and edge features and present future directions for feature-enhanced embeddings.

1. Curriculum Learning and Adaptive Data Scheduling – We detail our adaptive data release schedule, including the Cumulative Improvement Ratio (CIR), which prevents models from becoming stuck in local minima. This section provides additional insights into our methodology and compares alternative scheduling strategies.

1. Robustness and Sensitivity Analysis – We address reviewer feedback on hyper-parameter sensitivity by expanding our preliminary findings and discussing future studies to further enhance robustness across architectures and datasets.

1. Improved Abstract and Methodological Flow – In response to feedback on the paper’s structure, we clarify the motivation, methodology, and the role of contrastive learning within EmbCL. These improvements ensure a smoother flow and coherence throughout the paper.

1. Enhanced Figures and Presentation – To improve accessibility and readability, we have revised multiple figures and tables, enhancing resolution, layout, and clarity.

Each section provides both the rationale behind updates and the specific changes made, ensuring a comprehensive and transparent response.

### Section 1: Expanded Performance Analysis
#### Dataset Performance Overview

In response to the reviewers’ comments regarding the variability of EmbCL’s performance across datasets, we provide a detailed analysis of EmbCL’s results on the D&D, ENZYMES, and NCI1 datasets. Each of these datasets presents unique structural challenges, allowing us to examine EmbCL’s effectiveness in varied settings.

- **D&D Dataset**: EmbCL showed particularly strong results on the D&D dataset, achieving a significant 5% improvement over baseline methods. The dataset’s larger sample size and rich structural features align well with EmbCL’s curriculum learning approach, which benefits from diverse graph structures to guide the model progressively through complex samples. We attribute this improvement to EmbCL’s ability to capture subtle structural variations, which are especially relevant for D&D’s protein structure graphs. This dataset offers a high level of structural detail that aligns well with EmbCL’s design, where structural distinctions play a critical role in the learning process.

- **ENZYMES Dataset**: The ENZYMES dataset, in contrast, showed limited performance gains with EmbCL. We observed that ENZYMES’ smaller sample size and relatively lower structural diversity present limitations for curriculum learning. With fewer than 100 samples per category, this dataset constrains the progressive data release strategy that EmbCL employs, reducing the benefits of incremental learning. Literature on curriculum learning (e.g., Na et al., 2024; Brigato et al., 2021) suggests that small datasets can lead to models becoming trapped in local minima when early training lacks sufficient structural diversity. Although EmbCL improves stability and performance relative to baseline models, the impact is constrained by these dataset-specific limitations.

- **NCI1 Dataset**: On NCI1, EmbCL achieved modest improvements, reflecting the dataset’s intermediate sample size and structural complexity. EmbCL’s performance gains here are relatively small but consistent, showing an improvement of approximately 1% over comparable methods. While modest, this improvement aligns with recent literature, which suggests that even slight gains in challenging datasets like NCI1 can signify meaningful progress in graph classification tasks. NCI1’s chemical compound graphs present moderate structural diversity, which allows EmbCL to apply its curriculum strategy effectively, albeit with less pronounced results than on D&D.

In summary, these results underscore EmbCL’s adaptability to datasets with high structural complexity and adequate sample size, where curriculum learning can fully leverage the progressive release of increasingly complex samples. Updated figures and tables provide additional detail on these dataset-specific outcomes, and we invite reviewers to refer to Tables 2 and 3 for a more granular presentation of these results.

#### Metrics and Confidence Intervals

To further clarify EmbCL’s performance across datasets, we have included additional details in updated Figures 8 and Tables 2 and 3. These updates offer a clearer visual and numerical breakdown of performance, including accuracy metrics and confidence intervals for each dataset and model configuration.

The confidence intervals across D&D, ENZYMES, and NCI1 datasets reveal important insights into EmbCL’s stability relative to baseline methods. For example, EmbCL consistently demonstrated narrower confidence intervals on D&D, underscoring the method’s robustness in this more structurally complex dataset. These narrower intervals indicate greater consistency in performance, which aligns with EmbCL’s design to handle varying structural complexities. In contrast, the wider intervals observed on ENZYMES align with the limitations previously discussed, as smaller datasets can introduce greater variability in results due to less structural diversity. This variability is consistent with the literature on curriculum learning (e.g., Na et al., 2024; Cheng et al., 2019), which notes that small sample sizes may prevent models from fully leveraging curriculum-based progression, thereby reducing stability in outcomes.

In NCI1, the confidence intervals are moderate, with EmbCL achieving slightly tighter intervals than baseline models. This consistency suggests that, while gains are modest, EmbCL offers stable performance improvements, particularly in structurally diverse datasets where curriculum learning strategies can be effectively applied.

#### Significant Gains on D&D

The 5% accuracy improvement observed on the D&D dataset is particularly noteworthy, as even small performance gains on structurally complex graph datasets are recognized as meaningful in the curriculum learning literature. For instance, Na et al. (2024) and Brigato et al. (2021) discuss the impact of incremental improvements in curriculum learning, highlighting that minor accuracy gains often correspond to more substantial increases in model robustness and generalizability. In D&D, where graphs represent detailed protein structures, this gain is a testament to EmbCL’s capability to adaptively introduce increasingly complex structures, enhancing both model accuracy and robustness.

This improvement is significant given D&D’s sample size and inherent structural richness, which aligns well with the curriculum learning progression employed by EmbCL. The 5% gain not only reflects EmbCL’s efficiency in handling diverse graph structures but also underscores its effectiveness in leveraging complex dataset features to optimize model learning. This finding strengthens our assertion that EmbCL is particularly well-suited to large and structurally varied datasets where curriculum learning can drive meaningful performance improvements.

### Section 2: Rationale for Embedding and Feature Integration
#### Structure-Only Embeddings

In response to the reviewers’ feedback, we provide additional justification for our decision to focus exclusively on structure-based embeddings using Weisfeiler-Leman (WL) graph kernels. WL kernels offer a powerful, deterministic approach to embedding that is especially well-suited to characterizing graph structures across diverse datasets. Our choice to exclude node and edge feature embeddings was driven by both practical and theoretical considerations: including features often introduces high sparsity, which can destabilize the embedding vectors and reduce performance. As noted in recent studies (e.g., Chakraborty and Zhang, 2021), sparsity in high-dimensional embeddings can lead to orthogonality among vectors, undermining the similarity measurements crucial to EmbCL’s curriculum learning approach.

The WL kernel’s deterministic, structure-focused embeddings avoid these issues by relying solely on topological information, which ensures consistency and avoids the sparsity challenges commonly associated with feature-rich embeddings. Furthermore, the structure-only approach aligns with EmbCL’s goal of achieving a scalable, dataset-agnostic solution that generalizes well across different types of graph data.

#### Challenges with Feature Embeddings

Our preliminary experiments with feature embeddings revealed several key challenges that reinforced our decision to focus on structure-only embeddings. First, including node and edge features in the embedding space led to an explosion in dimensionality, as each feature effectively increased the vector space exponentially. This high dimensionality not only made computations more resource-intensive but also amplified sparsity within the embedding space, causing distribution instability and reducing embedding efficacy for curriculum learning. In several instances, the embeddings became so sparse that their effectiveness in capturing structural similarity was significantly diminished, as documented in Khoshraftar and An (2024), who explored similar issues in graph representation learning.

Distribution instability was another observed challenge, where feature embeddings led to inconsistent vector distributions across samples. This inconsistency posed a risk for EmbCL’s progressive data release strategy, as models struggled to interpret or leverage embeddings with high-dimensional, sparse vectors effectively. These observations informed our decision to prioritize a structure-based embedding approach that retains high consistency and is less prone to distributional challenges.

#### Benefits of Structural Embeddings

The decision to rely on structure-only embeddings offers several benefits, particularly in terms of robustness and scalability across datasets. By focusing on structural information, EmbCL remains largely dataset-agnostic, making it adaptable to a wide range of graph types without requiring specific feature engineering or preprocessing steps. This flexibility is crucial for applications where datasets vary in size, complexity, or domain, as it allows EmbCL to operate effectively across domains as diverse as bioinformatics, chemistry, and social networks.

Additionally, structure-only embeddings enhance scalability, as the WL kernel’s linear time complexity allows EmbCL to process large datasets efficiently without the added computational overhead of high-dimensional feature vectors. This efficiency is especially valuable for graph-based tasks where scalability and performance consistency are paramount. Our choice of structure-only embeddings thus aligns with EmbCL’s design goals, enabling it to balance robustness, efficiency, and adaptability across varied datasets.

# Section 3: Curriculum Learning Methodology and Scheduling
## Adaptive Data Release Schedules

- Initial 50-70% data release.
- Cumulative Improvement Ratio (CIR) prevents local minima.
## Data Release Strategies and Performance

- Table summarizing EmbCL I, II, III schedules.
- Comparison with random vs. CIR-guided release.
## Illustrative Figures

- Improved Figures 3 and 5 showing CIR impact.
# Section 4: Robustness and Sensitivity Analysis
## Hyper-parameter Sensitivity

- Limited exploration due to space.
- Preliminary findings in Appendix Table 4.
## Future Robustness Studies

- Planned in-depth sensitivity analysis.
- Emphasize EmbCL’s simplicity for robustness.
## Updated Figures and Tables

- Specific improvements in appendix clarity.
# Section 5: Improved Abstract, Motivation, and Flow
## Expanded Abstract

- Added limitations in prior methods.
- Highlight scalability and structural challenges.
## Justification for WL Kernels

- Compare with random walks and subgraph methods.
- References on WL’s efficiency and robustness.
## Flow and Cohesion Improvements

- Clarified methodology and related work.
- Revised Figure 3 and 5 intros.
# Section 6: Improved Figure Quality and Presentation
## Enhanced Figure Quality

- Higher DPI, balanced layout, improved text size.
- Improved color and contrast for accessibility.
## Tabular Enhancements

- Moved Tables 2 and 3 to main text.
- Improved formatting for performance comparisons.
# Conclusion and Future Work
- Unified Response addresses all reviewer points.
- Future Exploration in feature embedding and sensitivity.
- Thanks to reviewers for constructive feedback.
