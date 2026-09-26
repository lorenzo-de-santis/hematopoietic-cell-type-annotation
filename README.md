# Hematopoietic Cell-Type Annotation from scRNA-seq Data

This repository contains an end-to-end analysis of a murine hematopoietic single-cell RNA-sequencing dataset. The project combines biological interpretation, exploratory analysis, dimensionality reduction, unsupervised clustering, representation learning, and supervised cell-type classification.

The central questions are:

1. Do transcriptionally similar cells organise into patterns compatible with continuous hematopoietic differentiation?
2. How reliably can ten supplied cell-type labels be predicted from annotated expression profiles?

## Repository contents

```text
.
├── README.md
├── hematopoietic-cell-type-annotation.ipynb
├── hematopoietic-cell-type-annotation.html
├── data/
│   └── README.md
└── results/
    └── README.md
```

- The **notebook** contains the complete executable analysis and discussion.
- The **HTML file** provides a rendered version that can be read without running Python.
- [`data/README.md`](data/README.md) describes the required input files and label encoding.
- [`results/README.md`](results/README.md) summarises the main biological and modelling results.

## Data setup

The course-provided data are not redistributed in this repository. To run the notebook, place these files in the **same directory as the notebook**:

```text
single_cell.h5ad
singlecell_train.csv
```

The notebook uses `Path.cwd()` and contains no machine-specific paths. Launch Jupyter from the repository directory, then run all cells in order.

## Main workflow

The analysis covers:

- inspection of the AnnData structure and numerical expression scale;
- exploratory analysis and marker-gene interpretation;
- highly variable gene selection and gene-wise scaling;
- PCA, UMAP, t-SNE, nearest-neighbour graphs, K-means, Leiden, Ward clustering, and SOM;
- differential expression analysis;
- PCA, autoencoder, and denoising-autoencoder comparison;
- logistic regression, SVM, random forest, XGBoost, and MLP classification;
- an exploratory Graph Convolutional Network;
- refitting of the selected pipeline on all annotated cells and inference on the unannotated profiles.

## Key result

`MEP_broad` is the most transcriptionally distinct population, whereas the remaining progenitor populations overlap substantially. An RBF SVM on 32 PCA components gives the strongest internal cross-validation result, but fine ten-class annotation remains difficult and many final assignments retain moderate uncertainty.

## Software

The notebook was developed with Python 3.10 and uses NumPy, Pandas, SciPy, Matplotlib, Seaborn, AnnData, Scanpy, UMAP, scikit-learn, PyTorch, and XGBoost. Exact package versions are printed near the beginning of the notebook.

## Interpretation

The numerical class codes are arbitrary identifiers supplied with the annotations. They are not discovered clusters, are not ordinal, and do not represent differentiation time or biological distance. Predicted labels should be treated as model-supported hypotheses rather than experimentally validated identities.

