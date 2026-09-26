# Data

The analysis requires two course-provided files. They are intentionally not committed to the repository; copy them into the **repository root**, beside the notebook, before execution.

| File | Contents |
|---|---|
| `single_cell.h5ad` | AnnData object containing 1,499 cells and 4,290 genes |
| `singlecell_train.csv` | Labels for 1,074 annotated cells |

The AnnData object stores cell identifiers in `obs`, gene identifiers and symbols in `var`, and expression values in `X`. The remaining 425 cells have no supplied label.

## Label encoding

The `clusters` column in `singlecell_train.csv` contains arbitrary numerical encodings assigned to the supplied cell types:

| Code | Cell type |
|---:|---|
| 0 | `CMP_broad` |
| 1 | `GMP_broad` |
| 2 | `LMPP_broad` |
| 3 | `LTHSC_broad` |
| 4 | `MEP_broad` |
| 5 | `MPP1_broad` |
| 6 | `MPP2_broad` |
| 7 | `MPP3_broad` |
| 8 | `STHSC_broad` |
| 9 | `other` |

These numbers are effectively random with respect to the biology: code 8 is not “greater” than code 2, neighbouring codes need not represent related populations, and the column is not the output of K-means, Leiden, or another clustering algorithm. It is simply a machine-readable encoding of the textual labels.

## Important notes

- Gene identifiers use the `ENSMUSG` prefix, supporting a murine origin. The precise tissue source is not stored in the supplied files.
- The expression matrix is not raw counts. Its values are strongly compatible with an upstream base-2 logarithmic transformation, but the exact normalisation procedure cannot be reconstructed.
- The notebook therefore preserves the supplied expression scale instead of applying an additional normalisation and logarithm.
- Annotated and unannotated cells have similar label-free expression summaries, but the class composition of the unannotated subset is unknown.

