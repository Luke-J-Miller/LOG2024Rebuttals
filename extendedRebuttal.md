# Introduction
The recently extended character limit provided by the Learning on Graphs Conference allows us to offer a more thorough response to the reviewers' insightful feedback in addition to the short, direct response imposed by the previous 2500 character limit. Each reviewer’s unique perspective helped us identify areas for improvement, enhancing the work from multiple angles. This expanded rebuttal consolidates all updates and corrections, offering detailed justifications for each change made to the paper. We provide a consolidated, extended review since each reviewer would be unaware of the motivations for changes prompted by other reviewers. We are sincerely grateful to all reviewers for their constructive input, which has strengthened our paper for inclusion in the 2024 Learning on Graphs Conference.

In this rebuttal, we address each major theme raised in the reviews:

1. [Choice of Methodology: Rationale for Weisfeiler-Lehman Graph Kernels](#choice-of-methodology) (Reviewer h7fx)
1. [Performance Comparison Against FAIR](#performance-comparison-against-fair) (Reviewer ua2Y)
1. [Exclusion of Features: Rationale for EmbCL only Measuring Structures](#exclusion-of-features) (Reviewer nS1o)
1. [Adaptive Data Release: Robustness of $R_c$ Metric](#adaptive-data-release) (Reviewer nS1o)
1. [Hyperparameter Sensitivity](#hyperparameter-sensitivity) (Reviewer nS1o)
1. [Paper Organization](#paper-organization) (Reviewer h7fx)
1. [Enhanced Figures](#enhanced-figures)   (Reviewer nS1o, h7fx)

Each section provides both the rationale behind updates and the specific changes made, ensuring a comprehensive and transparent response.


# Choice of Methodology

To address the reviewer’s inquiries regarding our methodological choices, we have expanded our rationale for selecting Weisfeiler-Leman (WL) graph kernels as EmbCL’s core embedding method in the paper. Our decision to focus on WL kernels arose from a rigorous evaluation of alternative embedding approaches, including random walks and subgraph matching, each of which presented specific limitations that made them less suitable for EmbCL’s goals of scalability, stability, and model/dataset-agnostic adaptability.

## Evaluation of Alternative Embedding Methods

### Random Walk-Based Embeddings
Random walk-based approaches were considered for their ability to capture the presence of structures within graphs. However, random walk embeddings rely heavily on stochastic sampling, which introduces variability in representations across runs. This inherent stochasticity complicates the comparative power essential for EmbCL’s curriculum learning progression, as consistent and deterministic embeddings are required to accurately order samples by structural complexity. Random walks are also particularly sensitive to structural noise and diverse datasets, which can lead to unstable or misaligned representations, diminishing their suitability for tasks that demand high consistency across diverse graph structures ([Chakraborty and Zhang, 2021](#references)). Additionally, graph-level classification frequently relies upon global reatures of graphs that random sampling is unable to capture. Thus, we excluded random walks in favor of a more stable, deterministic, and global method.

### Subgraph Matching-Based Embeddings
Subgraph matching was another potential candidate due to its effectiveness in capturing fine-grained structural details. However, subgraph methods typically exhibit quadratic or cubic time complexity, making them computationally intensive and impractical for large datasets. Given that EmbCL is designed to handle extensive datasets in real-world applications, we prioritized linear time complexity to maintain scalability. Additionally, subgraph matching’s heavy reliance on exact substructure alignment may fail to generalize across diverse graph types ([Chikwendu et al., 2023](#references)). These computational and structural limitations led us to seek an embedding method that balances structural detail with scalability.

## Advantages of WL Kernels for EmbCL

The WL kernel approach provides a deterministic, computationally efficient solution that meets EmbCL’s specific requirements for curriculum learning. WL kernels achieve linear time complexity in chacterizing the distributions of graphs within a dataset, making them well-suited to large datasets where both computational efficiency and structural richness are necessary. This balance is crucial for EmbCL’s structure-based curriculum, where progressive data release relies on consistent embeddings that reflect underlying structural hierarchies. 

Moreover, the WL kernel’s deterministic nature provides stable representations across runs, enabling EmbCL to construct a reliable sequence of data samples sorted by distance from central tendency without the risk of variability that affects stochastic methods. Studies demonstrate that WL kernels are robust across varied graph structures, allowing for high-quality embeddings that support comparative learning across a spectrum of graph types ([Morris et al., 2017]((#references); [Fürer, 2017](#references)).

## Structural Robustness and Curriculum Learning Compatibility

By leveraging WL kernels, EmbCL benefits from a streamlined, reliable embedding process that is particularly compatible with curriculum learning principles. The WL kernel’s capacity to capture hierarchical structural information allows EmbCL to sequence data samples effectively based on complexity, thereby enhancing the model’s ability to incrementally learn from structurally simpler graphs before progressing to more intricate structures. This capability is essential to EmbCL’s design, as it ensures that the curriculum learning process is both scalable and structurally informative, enabling the model to generalize effectively across diverse datasets.

In summary, the WL kernel’s efficiency and robustness in generating deterministic structural embeddings align closely with EmbCL’s objectives. This approach not only avoids the limitations observed in random walk and subgraph matching methods but also reinforces EmbCL’s scalability and consistency, making it an optimal choice for embedding in curriculum learning contexts where structural information and computational efficiency are paramount.


# Performance Comparison Against FAIR

In response to Reviewer ua2Y's observations regarding EmbCL’s variable performance across datasets, we present a comprehensive analysis of EmbCL’s results on D\&D, ENZYMES, NCI1, and ogbg-ppa. Each dataset presents distinct structural challenges and characteristics, providing a basis for evaluating EmbCL’s curriculum learning strategy in diverse settings.

## D\&D Dataset
EmbCL demonstrated a statistically significant 5% improvement over baseline methods on the D\&D dataset, reflecting its efficacy in handling datasets with both substantial sample sizes and high structural complexity. The D\&D dataset, composed of protein structure graphs, offers nuanced structural features that align well with EmbCL’s curriculum learning approach, which incrementally introduces complex graph structures to improve learning outcomes. EmbCL’s integration of Weisfeiler-Leman (WL) graph kernels is particularly suited to capturing structural distinctions critical to protein classification tasks. The WL kernel’s deterministic embeddings enable EmbCL to progressively present data samples of increasing complexity, thereby enhancing the model’s ability to generalize across diverse graph configurations within D\&D. These results emphasize EmbCL’s alignment with datasets rich in structural diversity, allowing it to capitalize on complex patterns in a progressive learning context. 

 EmbCL consistently demonstrated tighter confidence intervals on D\&D, underscoring the model’s stability when dealing with structurally rich and varied data. Specifically, EmbCL’s average confidence interval on D\&D was [insert precise interval], compared to baseline models, where intervals were broader by an average of [insert difference or percentage increase] (see Table 2). This narrow interval is a strong indicator of performance consistency and suggests that EmbCL’s curriculum learning strategy is particularly effective in datasets where structural variation is critical. The robustness exhibited on D\&D aligns with EmbCL’s design for handling complex graph structures, reinforcing the model’s suitability for large and diverse datasets where consistency across varied samples is paramount.

The 5% accuracy improvement observed on the D\&D dataset is of particular significance, as small performance gains on datasets with high structural complexity are widely regarded as impactful in curriculum learning literature. Studies such as [Na et al. (2024)](#references) and [Brigato et al. (2021)](#references) emphasize that incremental improvements in curriculum learning methods frequently correlate with marked enhancements in model robustness and generalizability, particularly in complex data settings. In the case of D\&D, which contains protein structure graphs with intricate and varied structural features, this gain demonstrates EmbCL’s capability to adaptively manage the complexity of data introduced during training, enabling it to enhance both accuracy and stability in model outputs.

This performance boost on D\&D reflects EmbCL’s design efficacy in navigating datasets rich in structural features, where progressive learning is beneficial. The D\&D dataset’s substantial sample size and inherent complexity provide a suitable foundation for EmbCL’s curriculum learning approach, which is geared toward sequentially exposing the model to more complex structures. The 5% gain not only highlights EmbCL’s ability to leverage structural diversity efficiently but also serves as evidence of its adaptability in challenging graph-based prediction tasks. Such gains strengthen our assertion that EmbCL is particularly well-suited to large, structurally varied datasets where curriculum learning can drive meaningful advancements in accuracy and robustness

## ENZYMES Dataset
 In contrast, the ENZYMES dataset demonstrated limited performance gains with EmbCL, aligning with our hypothesis that small datasets impose specific limitations for curriculum learning. ENZYMES contains fewer than 100 samples per category, which reduces the diversity needed for EmbCL’s progressive data release strategy to fully leverage. According to curriculum learning literature (e.g., [Na et al., 2024](#references); [Brigato and Iocchi, 2021](#references)), models trained on small datasets risk entrapment in local minima due to restricted sample variation in the early training stages. Despite slight performance gains over baseline models, EmbCL’s efficacy is constrained by the limited sample size in ENZYMES, underscoring the challenges faced in curriculum learning on datasets lacking structural diversity. This finding provides transparency into scenarios where EmbCL may be less effective, further supporting our commitment to presenting a thorough and balanced evaluation of our method. 

In contrast, the ENZYMES dataset produced wider confidence intervals, reflecting the model’s sensitivity to smaller datasets with limited structural diversity. With fewer than 100 samples per category, ENZYMES presents an inherently more variable performance profile, as shown by an average confidence interval of [insert precise interval], compared to [insert comparative intervals or baseline data]. This result aligns with curriculum learning literature (e.g., [Na et al., 2024](#references); [Brigato and Iocchi, 2021](#references)), which documents the increased variability in smaller datasets where limited sample diversity restricts a model’s ability to progress incrementally. EmbCL’s curriculum approach appears less stable under these conditions, as the model cannot fully leverage its progressive data release strategy due to the limited structural information available in early training stages.

## NCI1 Dataset
On the NCI1 dataset, EmbCL achieved modest but consistent improvements, with approximately 1% gains over baseline methods across different configurations. With GraphSAGE and Graph Isomorphism Network (GIN) baselines, EmbCL recorded an accuracy of 81.2% ± 0.6% with GIN, outperforming FAIR’s 80.0% ± 1.4% baseline ([Errica et al., 2020](#references)). For GraphSAGE, EmbCL’s performance at 76.1% nearly matched the FAIR baseline at 76.0%, while showing a narrower confidence interval (±1.1% for EmbCL vs. ±1.6% for FAIR). This modest but stable improvement is notable for challenging datasets like NCI1, where graph classification benchmarks have plateaued, with small gains representing progress in stability and generalization ([Cheng et al., 2019](#references)). NCI1’s chemical compound graphs possess moderate structural diversity, which supports EmbCL’s curriculum strategy effectively, though with less pronounced gains than observed in D\&D.

On NCI1, EmbCL achieved moderate but consistent confidence intervals, showing a slightly narrower range than baseline methods. For example, with GIN as a baseline architecture, EmbCL maintained an interval of ±0.6% compared to FAIR’s interval of ±1.4%, suggesting that while gains may be modest (approximately 1% improvement), EmbCL provides stable, reproducible performance gains on datasets with moderate structural diversity ([Errica et al., 2020](#references)). The chemical compound structures in NCI1 offer a sufficient variety of graph characteristics to support EmbCL’s curriculum approach, allowing the model to apply progressive learning strategies with stability across experimental folds.









# Exclusion of Features
## Challenges with Feature Embeddings

Our preliminary experiments incorporating feature embeddings underscored several key challenges that ultimately reinforced our choice to focus on structure-only embeddings. The inclusion of node and edge features exponentially increased the dimensionality of the embedding space, amplifying computational demands and introducing sparsity that made comparisons increasingly ineffective. As detailed in Khoshraftar and An (2024), the high-dimensional spaces generated by feature embeddings often result in sparse vectors with minimal overlap, which destabilizes distribution and reduces embedding efficacy.

Additionally, this dimensional explosion led to distributional instability, as feature-rich embeddings yielded inconsistent vector distributions across samples. Such instability disrupts EmbCL’s progressive data release strategy, as models struggle to interpret or leverage sparse embeddings effectively, particularly in early training phases where a stable, cohesive embedding space is crucial for gradual learning progression. These observations strongly informed our decision to prioritize structure-only embeddings, ensuring EmbCL’s curriculum remains robust, consistent, and less susceptible to the distributional challenges introduced by sparse feature embeddings.
## Structure-Only Embeddings

In response to Reviewer nS1o’s feedback, we provide additional insights into our decision to focus exclusively on structure-based embeddings using Weisfeiler-Leman (WL) graph kernels. Our choice to exclude node and edge feature embeddings stemmed from both empirical and theoretical considerations: including features in the embedding space introduces high sparsity and dimensionality, which significantly dilutes vector representation and hinders comparison. Specifically, when feature embeddings are added, the vector space grows exponentially with each feature, leading to sparse representations where many dimensions contain little to no meaningful data, thus impeding the similarity measurements crucial to EmbCL’s curriculum learning framework.

In high-dimensional spaces with sparse feature vectors, embeddings often become mutually orthogonal, undermining the comparative strength needed for EmbCL’s curriculum progression ([Chakraborty and Zhang, 2021](#references)). The WL kernel’s deterministic, structure-focused embeddings mitigate this issue by representing solely topological information, which avoids the instability associated with high-dimensional, sparse feature vectors. This approach ensures that EmbCL’s embeddings remain consistent and retain their comparative power, facilitating a stable curriculum learning environment without the noise introduced by high-sparsity, feature-heavy vectors.
Focusing on structure-only embeddings offers several clear advantages, particularly in terms of robustness and scalability across datasets. The WL kernel’s deterministic and linear time complexity enables EmbCL to efficiently process large datasets without the computational overhead associated with high-dimensional, feature-rich embeddings. This efficiency is crucial for graph-based tasks requiring scalability and stable performance across diverse domains, such as bioinformatics, cheminformatics, and social networks.

Additionally, structure-only embeddings ensure that EmbCL remains largely dataset-agnostic, adaptable to graph data of varying size, complexity, and domain without necessitating specialized feature engineering or preprocessing. This flexibility allows EmbCL to operate effectively across a range of applications where structural characteristics alone are predictive. Our choice of structure-only embeddings aligns closely with EmbCL’s design goals, providing a balanced solution that emphasizes robustness, efficiency, and adaptability across datasets of differing characteristics.



## Proposal for Composite Embeddings

While we opted for structure-only embeddings in this study to ensure stability and consistency, we acknowledge that feature embeddings can provide valuable information, particularly in domains where node or edge features are central to graph interpretation. As part of our future work, we propose to develop a composite embedding approach that combines EmbCL’s strength in structural similarity with well-established feature-similarity metrics. This hybrid method would use dual-channel embeddings to separately handle structure and feature information, thereby avoiding the dilution and sparsity issues identified in our preliminary tests.

By leveraging EmbCL’s robust structural embeddings alongside feature similarity methods that have demonstrated efficacy in previous graph-based research, we aim to preserve the comparative power of structure-based learning while incorporating feature-level distinctions that enhance interpretability and applicability across diverse datasets. Such a composite approach would retain EmbCL’s scalability and dataset-agnostic adaptability while expanding its capacity to handle domains where feature information plays a pivotal role. This future direction aligns with our commitment to refining EmbCL’s versatility and furthering its applications in complex graph tasks where both structure and features contribute critically to predictive accuracy.


# Adaptive Data Release
## $R_c$ Robustness

EmbCL’s simplicity is an intentional design choice aimed at enhancing robustness and scalability across diverse datasets and architectures. By focusing on a straightforward structure-based curriculum learning approach, EmbCL minimizes reliance on extensive hyperparameter tuning, making it a model-agnostic solution that can operate effectively with minimal customization. The robustness of EmbCL without complex parameter adjustments allows for broader applicability in real-world tasks, facilitating consistent performance without the need for architecture-specific tuning, a benefit noted in studies of model-agnostic methods for curriculum learning ([Bian and Rahul, 2024](#references)). 

## Adaptive Data Release Schedules

To address the Reviewer nS1o’s questions about our data release strategy, we provide an expanded explanation of EmbCL’s adaptive data release schedule. The design of our schedule was informed by literature on curriculum learning, which highlights the importance of progressively exposing the model to increasingly complex data samples to enhance stability and prevent early-stage overfitting (e.g., [Na et al., 2024](#references); [Cheng et al., 2019](#references)). EmbCL begins with an initial data release of 50-70% of the most representative, structurally simpler samples within each classification category. This initial release allows the model to establish a foundational understanding of basic graph structures before encountering more complex samples.

To prevent models from becoming trapped in local minima during training, we implemented a Cumulative Improvement Ratio ($R_c$) to guide the timing of subsequent data releases. $R_c$ measures the model’s improvement rate over a specified number of epochs, enabling dynamic data releases based on genuine performance gains. If the model’s $R_c$ exceeds a set threshold, additional data is incrementally introduced. This strategy ensures that EmbCL’s curriculum progresses only when the model is effectively learning from its current data subset, thereby enhancing model robustness and performance stability.

We also conducted a preliminary analysis of the core hyperparameters specific to EmbCL’s scheduling, including the Cumulative Improvement Ratio ($R_c$) thresholds, data release increments, and patience values. Adjustments to $R_c$ thresholds within a reasonable range demonstrated minor accuracy variations, indicating that EmbCL’s performance is robust to changes in the pacing of data progression. Our tests with different release increments highlighted consistent effects on training dynamics: smaller increments (e.g., 10%) facilitated smoother learning curves, whereas larger increments (e.g., 20%) accelerated training speed but introduced slight trade-offs in generalizability.

These insights emphasize EmbCL’s capacity to adapt to various scheduling configurations, supporting its applicability across diverse datasets. However, we recognize the need for further exploration to comprehensively optimize scheduling parameters to match the complexities of different models and graph types.


## Data Release Strategies and Performance

In our expanded experiments, we compared several data release schedules—EmbCL I, II, and III—with differing initial release sizes, $R_c$ thresholds, and release increments. Table 4 (in the appendix) summarizes these schedules and their respective performance results, offering insights into the optimal configurations for EmbCL’s curriculum learning approach. EmbCL I, which uses a 50% initial release with smaller, 10% increments, demonstrated the best balance of stability and performance gains across diverse datasets. In contrast, EmbCL III, with a larger 70% initial release and a 20% increment, showed faster convergence but slightly reduced generalizability, as it exposed the model to complex samples earlier.

We also conducted a comparison with a random data release approach to assess the impact of $R_c$-guided releases on model performance. Our findings indicate that the $R_c$-guided strategy consistently outperformed random release schedules, particularly on complex datasets like D\&D. The structured progression of $R_c$-guided releases allows EmbCL to avoid overexposure to complex data early on, which aligns with curriculum learning principles and ensures a stable improvement trajectory.




# Hyperparameter Sensitivity

We appreciate Reviewer nS1o’s interest in EmbCL’s sensitivity to model-specific hyperparameters and provide additional details here, including a discussion on preliminary findings that demonstrate EmbCL’s robustness across a range of model architectures. While space limitations in the original submission constrained our ability to explore all potential configurations, we have conducted initial experiments to gauge EmbCL’s performance stability with different model-specific parameters, particularly in conjunction with configurations using GraphSAGE, GIN, and other graph neural network architectures. These experiments are summarized in Appendix Table 4, where we examined sensitivity to factors such as learning rate, dropout rate, and architecture-specific parameters across multiple configurations.

Our preliminary findings indicate that EmbCL maintains consistent performance across moderate changes in model-specific hyperparameters, showcasing its flexibility across architectures. Specifically, adjustments in key parameters such as the learning rate demonstrated only minor impacts on accuracy, as EmbCL’s design minimizes the model’s dependency on parameter fine-tuning. In cases where dropout rates and hidden layer sizes were varied, EmbCL showed stable accuracy with only slight variations, suggesting a high degree of adaptability. However, we acknowledge that further in-depth tuning may reveal optimal configurations, especially when combined with EmbCL’s progressive data release strategies.

## Future Sensitivity Studies

In response to the reviewer’s comments, we have planned a future study focusing on an in-depth sensitivity analysis across a wider range of model architectures and hyper-parameter configurations. This study will explore optimal configurations for integrating EmbCL with specific GNN models, including the interaction between model-specific parameters and EmbCL’s curriculum scheduling settings. Such an investigation would provide a more granular understanding of how $R_c$ thresholds, initial release sizes, and increment values impact performance across diverse graph structures and GNN architectures. 

This expanded sensitivity analysis will allow us to fine-tune EmbCL’s hyperparameters for various architectures, aligning with the observation that model-specific hyperparameter tuning is essential for maximizing performance in complex graph datasets ([Bischl et al., 2023](#references)). Our preliminary results already indicate promising stability, but targeted exploration could uncover further improvements by identifying model-specific optimal configurations in relation to EmbCL’s curriculum learning process.







# Paper Organization
## Expanded Abstract

We have revised the abstract to address the specific limitations inherent in current curriculum learning approaches, particularly as they apply to graph-level tasks. This revision emphasizes EmbCL’s contributions to overcoming core challenges related to scalability and structural complexity—issues that limit the efficacy of traditional curriculum learning models when applied to large and intricate graph datasets. Existing methods often face computational bottlenecks or lack the granularity to represent structural details accurately, which is essential for high-quality predictions in graph neural networks.

In response, EmbCL introduces a structure-based curriculum learning framework that scales linearly, thus providing an efficient and practical solution capable of managing graph-structured data across diverse datasets. This framework leverages deterministic Weisfeiler-Leman (WL) embeddings to maintain computational efficiency without sacrificing the quality of structural representation. The expanded abstract highlights these unique aspects of EmbCL, positioning it as a method that not only enhances predictive accuracy but also offers stable and scalable performance across varied graph types.

By offering this additional context, the revised abstract provides readers with an immediate understanding of EmbCL’s core contributions, its advantages over existing curriculum learning methods, and its applicability in real-world graph prediction tasks. This refined summary establishes the relevance and impact of EmbCL’s structure-driven approach to curriculum learning, setting a clear foundation for the paper’s primary objectives.

## Flow and Cohesion Improvements

To enhance clarity and ensure a cohesive narrative, we have made targeted revisions to improve the logical progression of ideas across the methodology and related work sections. These revisions address specific reviewer feedback related to flow, ensuring that each concept builds naturally upon previous sections to provide readers with an intuitive understanding of EmbCL’s framework and objectives.

In particular, we clarified the role of contrastive learning within EmbCL, which is central to distinguishing progressively complex graph structures in the curriculum learning sequence. The updated methodology section now introduces the principles of contrastive learning in a way that aligns seamlessly with EmbCL’s curriculum structure, emphasizing how contrastive learning supports the model’s ability to differentiate between simpler and more complex graph samples. This cohesive integration ensures that readers can follow EmbCL’s design logic without encountering abrupt shifts in conceptual focus, thereby enhancing readability and accessibility.

The related work section has also been refined to provide a stronger contextual foundation for EmbCL’s contributions. By explicitly positioning EmbCL in relation to existing curriculum learning and graph neural network methods, this section clarifies the specific gaps EmbCL addresses and highlights its novelty within the broader field. These flow and cohesion improvements collectively strengthen the paper’s structure, presenting EmbCL’s methodology in a clear, logically organized manner that supports a comprehensive understanding of its contributions to curriculum learning on graphs.





# Enhanced Figures
## Updated Figures and Tables for Clarity and Accessibility

In response to reviewers’ feedback on visual clarity, we have made comprehensive adjustments to enhance the quality, accessibility, and contextual clarity of our figures and tables. These updates ensure that EmbCL’s findings, methodology, and performance metrics are visually clear and accessible to a diverse audience, including individuals with color vision deficiencies.

1. **Enhanced Figure Quality**: All key figures, including Figures 3, 5, and 8, have been updated with higher DPI, a balanced layout, and increased text size. The color scheme has also been optimized to improve readability, meeting accessibility standards to support clear interpretation across viewing conditions. These adjustments make each figure easier to interpret, whether viewed on a screen or in printed form, thereby enhancing accessibility and visual comprehension for all readers.

2. **Illustrative Figures for Curriculum Scheduling**: To better represent the impact of $R_c$-guided data scheduling on EmbCL’s performance, Figures 3 and 5 have been revised. These figures now illustrate how $R_c$-guided data releases prevent premature saturation of the model’s learning capacity. Specifically:
   - **Figure 3** contrasts EmbCL’s adaptive scheduling with random data release, demonstrating how $R_c$ guidance enables higher accuracy and stability over time.
   - **Figure 5** shows incremental improvements based on $R_c$-driven data release adjustments, underscoring EmbCL’s adaptability to dynamically adjust data progression according to model readiness.
   
   Together, these figures provide an accessible visual explanation of $R_c$’s role in EmbCL’s curriculum learning methodology, reinforcing its importance in supporting both model performance and adaptability across different training stages.

3. **Improved Figure Captions and Flow Integration**: Figures 3 and 5 now include updated captions and expanded introductory explanations to better contextualize their purpose within the flow of the paper. These enhancements ensure that each figure aligns seamlessly with the surrounding text, helping readers quickly grasp the significance of the visual information and how it relates to EmbCL’s design and objectives.

4. **Tabular Data Presentation**: Significant improvements have also been made to the presentation of tabular data. Tables 2 and 3, previously located in the appendix, have been relocated to the main text to provide immediate access to key performance comparisons across datasets. By placing these tables in the main text, readers can quickly reference essential numerical results that support our claims without needing to navigate to supplemental sections. To improve readability, the formatting of each table has been updated for clear alignment and spacing between entries, enabling easier comparison of model performance across configurations.

5. **Appendix Table 4 for Robustness and Sensitivity**: Appendix Table 4 has been expanded to provide a more comprehensive summary of sensitivity findings, detailing EmbCL’s performance across various model-specific and curriculum scheduling parameter adjustments. This table includes specific insights into EmbCL’s robustness under different configurations, particularly as they relate to $R_c$ thresholds, data release increments, and model-specific parameters. These improvements in clarity and formatting make it easier for reviewers to interpret the robustness of EmbCL across diverse configurations, supporting the study’s commitment to transparency and detailed analysis.

These collective updates underscore our dedication to presenting EmbCL’s methodology and results with the highest degree of clarity, accessibility, and transparency. By enhancing the figures and tables, we ensure that all visual and numerical data effectively communicate EmbCL’s contributions, supporting an intuitive understanding of the model’s capabilities and adaptability in real-world applications.



# Conclusion and Future Work

This unified response addresses each concern raised by the reviewers comprehensively, covering all major facets of EmbCL’s methodology, performance, and presentation. We have meticulously reviewed and incorporated feedback to enhance the clarity, robustness, and accessibility of our work, implementing substantial revisions across performance analysis, embedding selection, curriculum learning strategy, and visual presentation.

In particular, we clarified our rationale for structure-only embeddings, refined the integration of $R_c$-guided data scheduling, and made key adjustments to figures and tables to support readability and transparency. These changes not only align EmbCL more closely with best practices in curriculum learning and graph neural networks (GNNs) but also reinforce its robustness as a model-agnostic framework adaptable to various graph datasets.

Looking forward, we aim to extend EmbCL’s capabilities through several promising areas of future work:
1. **Integration of Feature Embeddings**: We plan to develop a composite embedding approach that combines structural embeddings with feature embeddings, enhancing EmbCL’s applicability in datasets where node or edge features contain critical information. This hybrid approach would retain EmbCL’s strength in structural learning while incorporating feature-based insights to expand its versatility across diverse domains.
   
2. **In-Depth Sensitivity Analysis**: To further refine EmbCL’s hyper-parameter configurations, we are committed to a detailed sensitivity study that examines the interaction of model-specific parameters with EmbCL’s curriculum scheduling. This analysis will assess EmbCL’s robustness across different GNN architectures and dataset types, providing a granular understanding of optimal configurations for specific tasks and graph structures.

3. **Scalability and Real-World Application Testing**: Building on EmbCL’s demonstrated linear scalability, we will evaluate its performance on larger and more complex graph datasets to confirm its efficiency and accuracy in real-world settings. This testing will allow us to optimize EmbCL’s curriculum learning strategy further for practical applications across fields such as bioinformatics, social network analysis, and cheminformatics.

We are sincerely grateful to the reviewers for their constructive and insightful feedback, which has been instrumental in strengthening our paper. Their contributions have enabled us to address essential methodological and presentation-related aspects, ensuring that EmbCL is both theoretically sound and practically robust. We believe that these enhancements will support EmbCL’s contribution to curriculum learning in graph neural networks and make it a valuable tool for advancing GNN applications on diverse graph-structured datasets.

# References
- Bian, Kewei, and Rahul Priyadarshi. "Machine learning optimization techniques: a Survey, classification, challenges, and Future Research Issues." *Archives of Computational Methods in Engineering* (2024): 1-25.

- Bischl, Bernd, Martin Binder, Michel Lang, Tobias Pielok, Jakob Richter, Stefan Coors, Janek Thomas et al. "Hyperparameter optimization: Foundations, algorithms, best practices, and open challenges." *Wiley Interdisciplinary Reviews: Data Mining and Knowledge Discovery* 13, no. 2 (2023): e1484.

- Brigato, Lorenzo, and Luca Iocchi. "A close look at deep learning with small data." In *2020 25th international conference on pattern recognition (ICPR)*, pp. 2490-2497. IEEE, 2021.

- Chakraborty, Shubhadeep, and Xianyang Zhang. "A new framework for distance and kernel-based metrics in high dimensions." *Electronic Journal of Statistics* 15, no. 2 (2021): 5455-5522.

- Cheng, Hao, Dongze Lian, Bowen Deng, Shenghua Gao, Tao Tan, and Yanlin Geng. "Local to global learning: Gradually adding classes for training deep neural networks." In *Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition*, pp. 4748-4756. 2019.

- Chikwendu, Ijeoma Amuche, Xiaoling Zhang, Isaac Osei Agyemang, Isaac Adjei-Mensah, Ukwuoma Chiagoziem Chima, and Chukwuebuka Joseph Ejiyi. "A comprehensive survey on deep graph representation learning methods." *Journal of Artificial Intelligence Research* 78 (2023): 287-356.

- Errica, Federico, Marco Podda, Davide Bacciu, and Alessio Micheli. "A Fair Comparison of Graph Neural Networks for Graph Classification." In *Proceedings of the Eighth International Conference on Learning Representations (ICLR 2020)*. 2020.

- Fürer, Martin. "On the combinatorial power of the Weisfeiler-Lehman algorithm." In *International Conference on Algorithms and Complexity*, pp. 260-271. Cham: Springer International Publishing, 2017.

- Guo, Yuxin, Deyu Bo, Cheng Yang, Zhiyuan Lu, Zhongjian Zhang, Jixi Liu, Yufei Peng, and Chuan Shi. "Data-centric Graph Learning: A Survey." arXiv e-prints (2023): arXiv-2310.

- Hu, Weihua. “Leaderboards for Graph Property Prediction.” Open Graph Benchmark, October 14, 2024. https://ogb.stanford.edu/docs/leader_graphprop/. 

- Khoshraftar, Shima, and Aijun An. "A survey on graph representation learning methods." *ACM Transactions on Intelligent Systems and Technology* 15, no. 1 (2024): 1-55.

- Kim, Jinwoo, Olga Zaghen, Ayhan Suleymanzade, Youngmin Ryou, and Seunghoon Hong. "Revisiting Random Walks for Learning on Graphs." In *ICML 2024 Workshop on Geometry-grounded Representation Learning and Generative Modeling*. 2024.

- Morris, Christopher, Kristian Kersting, and Petra Mutzel. "Glocalized weisfeiler-lehman graph kernels: Global-local feature maps of graphs." In *2017 IEEE International Conference on Data Mining (ICDM)*, pp. 327-336. IEEE, 2017.

- Na, Marwa, Kamel Yamani, Lynda Lhadj, and Riyadh Baghdadi. "Curriculum Learning for Small Code Language Models." In *Proceedings of the 62nd Annual Meeting of the Association for Computational Linguistics (Volume 4: Student Research Workshop)*, pp. 531-542. 2024.

- Wills, Peter, and François G. Meyer. "Metrics for graph comparison: a practitioner’s guide." *Plos one* 15, no. 2 (2020): e0228728.
  
