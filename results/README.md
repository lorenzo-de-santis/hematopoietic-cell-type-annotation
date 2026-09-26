# Main Results

## Biological structure

- The dataset contains **1,499 cells**, **4,290 genes**, ten annotated populations, and marked class imbalance.
- `MEP_broad` is the clearest transcriptionally distinct population. PCA, UMAP, K-means, Leiden, Ward clustering, SOM, and differential expression all recover a compatible erythroid structure.
- Label-free K-means favours a coarse **two-cluster** solution, while the selected Leiden resolution produces **four communities**. Neither method naturally recovers ten sharply separated groups.
- The remaining stem and progenitor populations overlap strongly. `CMP_broad`, `GMP_broad`, and `MPP3_broad` share part of a myeloid axis, while early stem/MPP populations occupy neighbouring regions.
- This organisation is compatible with continuous, branching hematopoietic differentiation, but broad labels, technical variation, dropout, and small class sizes remain alternative explanations.

## Representations and models

- **1,000 highly variable genes** were retained, followed by a conservative **50-component PCA** working space.
- At 32 dimensions, PCA reconstructed held-out profiles slightly better than the autoencoder and denoising autoencoder. The nonlinear representations offered no clear downstream advantage.
- The best inductive classifier was an **RBF SVM on PCA-32**:

| Metric | Value |
|---|---:|
| Out-of-fold accuracy | 0.599 |
| Macro-F1 | 0.430 |
| Balanced accuracy | 0.440 |
| Fold macro-F1 SD | 0.019 |

- An SVM on PCA-50 was slightly weaker in macro-F1 (**0.420**) but more stable across folds (**SD 0.004**).
- The MLP did not outperform the classical models under the selected protocol.
- The exploratory transductive GCN was competitive but not superior: accuracy **0.562**, macro-F1 **0.414**, and balanced accuracy **0.437**. Its rare-class improvements are based on very small supports and should be interpreted cautiously.

## Error structure and final refit

- The largest confusion block occurs between `CMP_broad` and `GMP_broad`; `MPP3_broad` also overlaps with the myeloid/LMPP region.
- `other` and `MPP2_broad` are too sparsely represented for reliable class-specific estimates.
- After refitting the selected SVM on all 1,074 annotated cells, the largest predicted groups among the 425 unannotated profiles were `MEP_broad` (**96**), `LMPP_broad` (**77**), and `CMP_broad` (**75**).
- Prediction uncertainty remains meaningful: median assigned-class probability **0.596**, **49.6%** of assignments at or above 0.60, and median normalised entropy **0.462**.

These final labels are analytical hypotheses, not ground truth. Independent annotations, larger rare-class samples, and trajectory-oriented methods would be the most useful next steps.

