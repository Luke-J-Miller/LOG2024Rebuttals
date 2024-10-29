# Introduction and Consolidation Statement
The extended character limit provided by the Learning on Graphs Conference allows us to offer a more thorough response to the reviewers' insightful feedback. Each reviewer’s unique perspective helped us identify areas for improvement, enhancing the work from multiple angles. This expanded rebuttal consolidates all updates and corrections, offering detailed justifications for each change made to the paper. We are sincerely grateful to all reviewers for their constructive input, which has strengthened our paper’s suitability for inclusion in the 2024 Learning on Graphs Conference.

In this rebuttal, we address each major theme raised in the reviews:

1. Expanded Performance Analysis – We provide a comprehensive breakdown of EmbCL’s performance across key datasets (D&D, ENZYMES, and NCI1), with new figures and tables illustrating the model’s adaptability and robustness across varied data conditions.

1. Rationale for Embedding Choices – To clarify the design decisions behind EmbCL, we expand on the rationale for focusing on structure-based embeddings. We discuss the limitations of incorporating node and edge features and present future directions for feature-enhanced embeddings.

1. Curriculum Learning and Adaptive Data Scheduling – We detail our adaptive data release schedule, including the Cumulative Improvement Ratio (CIR), which prevents models from becoming stuck in local minima. This section provides additional insights into our methodology and compares alternative scheduling strategies.

1. Robustness and Sensitivity Analysis – We address reviewer feedback on hyper-parameter sensitivity by expanding our preliminary findings and discussing future studies to further enhance robustness across architectures and datasets.

1. Improved Abstract and Methodological Flow – In response to feedback on the paper’s structure, we clarify the motivation, methodology, and the role of contrastive learning within EmbCL. These improvements ensure a smoother flow and coherence throughout the paper.

1. Enhanced Figures and Presentation – To improve accessibility and readability, we have revised multiple figures and tables, enhancing resolution, layout, and clarity.

Each section provides both the rationale behind updates and the specific changes made, ensuring a comprehensive and transparent response.

# Section 1: Expanded Performance Analysis
## Dataset Performance Overview

- Strong results on D&D.
- Limited gains on ENZYMES.
- Modest improvements on NCI1.
## Metrics and Confidence Intervals

- Updated Figures 8, Tables 2, and 3.
- Discuss variance in confidence intervals.
## Significant Gains on D&D

- Emphasize importance of 5% gain.
- Reference supporting literature on curriculum learning gains.
# Section 2: Rationale for Embedding and Feature Integration
## Structure-Only Embeddings

- Choice of WL graph kernels.
- Exclusion of feature embeddings due to sparsity issues.
- Reference literature on sparsity.
## Challenges with Feature Embeddings

- High-dimensionality issues.
- Distribution instability in initial tests.
## Benefits of Structural Embeddings

- Dataset-agnostic robustness.
- Improved scalability across datasets.
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
