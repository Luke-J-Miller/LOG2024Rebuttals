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

### Section 3: Curriculum Learning Methodology and Scheduling
#### Adaptive Data Release Schedules

To address the reviewers' questions about our data release strategy, we provide an expanded explanation of EmbCL’s adaptive data release schedule. The design of our schedule was informed by literature on curriculum learning, which highlights the importance of progressively exposing the model to increasingly complex data samples to enhance stability and prevent early-stage overfitting (e.g., Na et al., 2024; Cheng et al., 2019). EmbCL begins with an initial data release of 50-70% of the most representative, structurally simpler samples within each classification category. This initial release allows the model to establish a foundational understanding of basic graph structures before encountering more complex samples.

To prevent models from becoming trapped in local minima during training, we implemented a Cumulative Improvement Ratio (CIR) to guide the timing of subsequent data releases. CIR measures the model’s improvement rate over a specified number of epochs, enabling dynamic data releases based on genuine performance gains. If the model’s improvement rate exceeds a set threshold, additional data is incrementally introduced. This strategy ensures that EmbCL’s curriculum progresses only when the model is effectively learning from its current data subset, thereby enhancing model robustness and performance stability.

#### Data Release Strategies and Performance

In our expanded experiments, we compared several data release schedules—EmbCL I, II, and III—with differing initial release sizes, CIR thresholds, and release increments. Table 4 (in the appendix) summarizes these schedules and their respective performance results, offering insights into the optimal configurations for EmbCL’s curriculum learning approach. EmbCL I, which uses a 50% initial release with smaller, 10% increments, demonstrated the best balance of stability and performance gains across diverse datasets. In contrast, EmbCL III, with a larger 70% initial release and a 20% increment, showed faster convergence but slightly reduced generalizability, as it exposed the model to complex samples earlier.

We also conducted a comparison with a random data release approach to assess the impact of CIR-guided releases on model performance. Our findings indicate that the CIR-guided strategy consistently outperformed random release schedules, particularly on complex datasets like D&D. The structured progression of CIR-guided releases allows EmbCL to avoid overexposure to complex data early on, which aligns with curriculum learning principles and ensures a stable improvement trajectory.

#### Illustrative Figures

To visually represent the impact of CIR-guided data scheduling on EmbCL’s performance, we have updated Figures 3 and 5. These figures now clearly illustrate how CIR-guided releases prevent premature saturation of model learning capacity. Figure 3 demonstrates the performance differences between EmbCL’s adaptive scheduling and random data release, showing how the model achieves higher accuracy and stability over time with CIR guidance. Figure 5 further emphasizes this point by illustrating CIR-based incremental improvements, highlighting EmbCL’s ability to dynamically adjust data release based on model readiness.

Together, these updates to Figures 3 and 5 provide a more accessible and illustrative view of CIR’s role in EmbCL’s curriculum learning methodology, underscoring its importance in enhancing model performance and adaptability.

### Section 4: Robustness and Sensitivity Analysis
#### Hyper-parameter Sensitivity

We appreciate the reviewers’ interest in EmbCL’s sensitivity to hyper-parameters and provide additional details here, with preliminary findings available in Appendix Table 4. Due to space limitations in the original submission, we included only a limited exploration of hyper-parameter configurations. However, we conducted several preliminary tests to gauge EmbCL’s robustness across different parameter settings, focusing on the Cumulative Improvement Ratio (CIR) thresholds, data release increments, and patience values.

These initial findings reveal that EmbCL’s performance is generally stable across a range of CIR thresholds, with only minor variations in accuracy when the threshold is adjusted within a reasonable range. Similarly, the release increment size shows a consistent impact on training dynamics: smaller increments (e.g., 10%) yield smoother learning curves, while larger increments (e.g., 20%) accelerate training but may reduce generalizability. These findings underscore EmbCL’s adaptability to different parameter settings, although further exploration is required to optimize configurations fully.

#### Future Robustness Studies

In response to reviewer comments, we are planning an in-depth sensitivity analysis in future work to explore EmbCL’s robustness across a wider array of models and datasets. This planned study will investigate the interaction of key hyper-parameters (e.g., CIR thresholds, initial release size, and increment size) with different types of graph structures, providing more granular insights into optimal configurations for EmbCL in various scenarios.

We emphasize that EmbCL’s simplicity is a deliberate design choice aimed at enhancing robustness and scalability across diverse datasets. By focusing on a straightforward, structure-based curriculum learning approach, EmbCL reduces dependence on fine-tuning and complex parameter adjustments, allowing it to operate effectively across a broad range of tasks with minimal customization. This robustness supports EmbCL’s potential as a flexible, model-agnostic solution for curriculum learning in graph neural networks, capable of achieving consistent performance without extensive hyper-parameter tuning.

#### Updated Figures and Tables

To provide a clearer view of our robustness and sensitivity findings, we have made specific improvements to the figures and tables in the appendix. Appendix Table 4 now includes a more comprehensive summary of hyper-parameter sensitivity across different configurations, detailing how changes in CIR thresholds, release sizes, and increment values affect model performance. We have also enhanced the clarity and formatting of these tables to ensure that reviewers can easily interpret the results. 

These updates in the appendix offer a more detailed and transparent view of EmbCL’s performance across various parameter settings, underscoring our commitment to exploring and improving the robustness of EmbCL for practical applications.

### Section 5: Improved Abstract, Motivation, and Flow
#### Expanded Abstract

We have revised the abstract to address the limitations in existing curriculum learning methods, particularly for graph-level tasks. The expanded abstract now highlights the primary challenges that EmbCL is designed to overcome: the scalability issues and structural complexity limitations found in current approaches. Traditional curriculum learning methods often struggle to process large graph datasets efficiently or to capture the nuanced structural details critical for accurate predictions. By introducing a structure-based curriculum learning framework that scales linearly, EmbCL addresses these gaps, offering a practical solution for graph neural networks across varied datasets.

This expanded abstract emphasizes EmbCL’s adaptability and performance on large-scale graph datasets, noting that the method not only improves accuracy but also provides a stable and efficient approach to managing structural complexity in graph data. This added context provides a clearer introduction to the purpose and significance of our work, offering readers an immediate understanding of the paper’s core contributions.

#### Justification for WL Kernels

To further clarify the methodological choices behind EmbCL, we have expanded our justification for using Weisfeiler-Leman (WL) graph kernels as the core embedding method. We compared WL kernels with alternative approaches such as random walks and subgraph matching, both of which were considered but ultimately not selected due to their limitations. Random walk-based embeddings, for instance, introduce stochasticity that can lead to inconsistent representations, particularly in highly diverse datasets. Subgraph methods, while effective in capturing fine-grained structural details, often exhibit quadratic or cubic time complexity, making them impractical for large datasets.

WL kernels, on the other hand, offer a deterministic and efficient approach to embedding graph structures, with proven robustness in handling a variety of graph types (e.g., Morris et al., 2023; Fürer, 2017). This approach aligns well with EmbCL’s goals of scalability and consistency, enabling the model to effectively manage diverse graph structures while maintaining linear time complexity. By leveraging WL kernels, EmbCL avoids the limitations of alternative methods, providing a streamlined, reliable way to create structurally rich embeddings suitable for curriculum learning.

#### Flow and Cohesion Improvements

In response to reviewers’ feedback on the clarity and flow of the paper, we have made several revisions to improve the logical progression of ideas throughout the methodology and related work sections. Specifically, we clarified the role of contrastive learning within EmbCL, ensuring that its integration into the curriculum learning framework is explained cohesively from the start. The methodology section now introduces contrastive learning principles in a way that connects naturally to the curriculum learning structure, providing readers with a smoother and more intuitive understanding of EmbCL’s design.

Additionally, we revised the introductions to Figures 3 and 5 to better contextualize their purpose within the flow of the paper. These figures now include updated captions and clearer explanations, helping readers quickly grasp the significance of the visual information presented. These adjustments improve the overall coherence of the paper, making EmbCL’s methodology and contributions more accessible and logically structured.

### Section 6: Improved Figure Quality and Presentation
#### Enhanced Figure Quality

In response to the reviewers’ feedback on visual clarity, we have made several adjustments to improve the quality and accessibility of our figures. All key figures, including Figures 3, 5, and 8, have been enhanced with higher DPI and a balanced layout, ensuring that visual elements are clear and easy to interpret at any viewing scale. We have also increased the text size and optimized the color scheme to improve readability, particularly for those viewing the document on screens or in printed form.

Additionally, the color contrast within the figures has been adjusted to meet accessibility standards, making the visual information easier to discern for individuals with color vision deficiencies. These adjustments enhance the overall accessibility of the paper, ensuring that the figures communicate EmbCL’s results clearly and effectively to a wide audience.

#### Tabular Enhancements

We have also made significant improvements to the presentation of tabular data within the paper. Tables 2 and 3, which previously appeared in the appendix, have been moved to the main text to provide more immediate access to critical performance comparisons across datasets. This relocation allows readers to quickly reference the numerical results supporting our claims without navigating to supplemental sections.

To improve the readability of these tables, we have updated the formatting to ensure clear alignment and spacing between entries, making it easier to compare model performances across different configurations. These changes enhance the clarity and usability of the tables, supporting a more streamlined presentation of EmbCL’s performance metrics and making the results accessible at a glance.

### Conclusion and Future Work

This unified response addresses each point raised by the reviewers in detail, covering all major aspects of EmbCL’s methodology, performance, and presentation. We have carefully reviewed and incorporated feedback to enhance the clarity, robustness, and accessibility of our work, making significant revisions across performance analysis, embedding choices, curriculum learning strategy, and visual presentation.

Looking ahead, we plan to further explore several promising areas of future work. One area of interest is the integration of feature embeddings alongside structural embeddings to expand EmbCL’s applicability across datasets where node or edge features provide critical information. Additionally, we are committed to conducting an in-depth sensitivity analysis to refine EmbCL’s hyper-parameter configurations and assess its robustness across different GNN architectures and dataset types.

We are sincerely grateful to the reviewers for their constructive feedback, which has been instrumental in strengthening our paper. Their insights have allowed us to address important methodological and presentation-related aspects, ensuring that EmbCL is both practically robust and theoretically grounded. We believe these improvements make our paper well-suited for inclusion in the 2024 Learning on Graphs Conference.
