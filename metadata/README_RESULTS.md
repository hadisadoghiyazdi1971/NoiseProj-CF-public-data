# Results index — NoiseProj-CF

The public CSVs in [`../results/`](../results/) are generated from the validated final analysis
record for scientific protocol `4.0.2-final`, with concise manuscript-facing views used where a
smaller table is easier to interpret.

The authoritative numerical direction is:

```text
validated final analysis -> public CSV -> rounded manuscript display
```

The public release does not reconstruct values from rounded PDF tables. This avoids small apparent
percentage discrepancies caused by rounding.

All primary effectiveness values are NDCG@10 unless a column says otherwise.

## Main effectiveness and dataset tables

| CSV | Provenance / meaning |
|---|---|
| `TABLE_MAIN_clean_vs_mean_noisy.csv` | Full-precision clean and equal-dataset mean-noisy NDCG@10 from `01_MAIN/TABLE_MAIN_clean_vs_mean_noisy.csv`, presented as a concise long table. |
| `TABLE_SECONDARY_METRICS.csv` | Full-precision Recall@100, MRR@10, and MAP@100 clean/noisy summaries from `01_MAIN/TABLE_SECONDARY_METRICS.csv`. |
| `TABLE_DATASET_METADATA.csv` | Dataset/document/query/fit-document metadata corresponding to the submitted manuscript dataset table. |
| `TABLE_DATASET_LEVEL.csv` | Full per-dataset, per-encoder, per-method clean/noisy effectiveness from `01_MAIN/TABLE_DATASET_LEVEL.csv`. |

## Robustness and heterogeneity

| CSV | Provenance / meaning |
|---|---|
| `TABLE_NOISEPROJ_DOMINANCE.csv` | Full 108-cell pairwise NoiseProj-CF dominance statistics from `02_ROBUSTNESS/TABLE_NOISEPROJ_DOMINANCE.csv`. |
| `TABLE_COMPACT_WIN_COUNTS.csv` | Which compact method wins each 108-cell comparison, aggregated from `02_ROBUSTNESS/TABLE_COMPACT_WIN_COUNTS.csv`. This is distinct from pairwise dominance. |
| `TABLE_LODO_DELTAS.csv` | Leave-one-dataset-out sensitivity from `03_HETEROGENEITY/TABLE_LODO_DELTAS.csv`. |
| `TABLE_RANKING_STABILITY_MACRO.csv` | Six-condition macro average derived from the 108-row final-analysis ranking-stability table in `04_STABILITY/TABLE_RANKING_STABILITY_MACRO.csv`. |
| `TABLE_REALIZED_CORRUPTION.csv` | Full-precision concise view combining synthetic corruption statistics from `04_STABILITY/TABLE_REALIZED_CORRUPTION.csv` with observed OCR statistics from `06_GENERALIZATION/TABLE_OBSERVED_OCR_NOISE_STATS.csv`. |

## Compression and dimension studies

| CSV | Provenance / meaning |
|---|---|
| `TABLE_CLASSICAL_BASELINES.csv` | Full-precision MiniLM four-dataset comparison combining the Full/NoiseProj rows from the dimension analysis with the additional classical baselines in `05_COMPRESSION/TABLE_CLASSICAL_BASELINES.csv`. |
| `TABLE_DIMENSION_EFFICIENCY.csv` | Direct final-analysis dimension table from `05_COMPRESSION/TABLE_DIMENSION_EFFICIENCY.csv`, including clean/noisy retention and storage reduction. |
| `TABLE_DIMENSION_PARETO.csv` | Direct final-analysis dimension table with the final-analysis Pareto flag from `05_COMPRESSION/TABLE_DIMENSION_PARETO.csv`. |
| `TABLE_NATIVE_MRL.csv` | Full-precision Nomic 128-D Native-MRL versus NoiseProj-CF comparison for both the four-dataset dimension panel and the six-dataset main panel. The six-dataset clean values are Native MRL `0.447143...` and NoiseProj-CF `0.449949...`. |

## Generalization and diagnostics

| CSV | Provenance / meaning |
|---|---|
| `TABLE_OBSERVED_OCR.csv` | Full-precision clean versus observed render/degrade/Tesseract OCR NDCG@10 for Full, PCA-128, and NoiseProj-CF-128, derived from `06_GENERALIZATION/TABLE_OBSERVED_OCR.csv`. |
| `TABLE_UNSEEN_GENERALIZATION.csv` | Full-precision four-generator unseen-corruption comparison derived from `06_GENERALIZATION/TABLE_UNSEEN_GENERALIZATION.csv`. |
| `TABLE_DOCUMENT_QUERY_NOISE_GEOMETRY.csv` | Direct diagnostic from `07_DIAGNOSTICS/TABLE_DOCUMENT_QUERY_NOISE_GEOMETRY.csv`; it measures document/query residual-covariance differences and should not be interpreted as evidence that the two nuisance operators are equal. |
| `TABLE_FIT_SEED_STABILITY.csv` | Direct calibration-seed stability summary from `07_DIAGNOSTICS/TABLE_FIT_SEED_STABILITY.csv`. |
| `TABLE_PAIRED_SEED_SENSITIVITY.csv` | Direct paired evaluation-seed sensitivity table from `10_STATISTICS/TABLE_PAIRED_SEED_SENSITIVITY.csv`. This is different from calibration fit-seed stability. |

## Transfer and system results

| CSV | Provenance / meaning |
|---|---|
| `TABLE_TRANSFER.csv` | Full-precision best-foreign-source noisy-transfer summary from `08_TRANSFER/TABLE_BEST_FOREIGN_SOURCE.csv`. |
| `TABLE_TRANSFER_REGRET.csv` | Derived non-negative regret view of `TABLE_TRANSFER.csv`: `max(0, -delta)`. |
| `TABLE_SYSTEM_FULL.csv` | Full-precision concise view of the 12 Quora/Nomic Flat/PQ/OPQ measurements in `09_SYSTEM/TABLE_SYSTEM_FULL.csv`. |
| `TABLE_SYSTEM_FLAT.csv` | Flat-index-only comparison used for the main storage/throughput/quality discussion. |

## Statistical inference

| CSV | Provenance / meaning |
|---|---|
| `TABLE_CROSSED_QUERY_SEED_BOOTSTRAP.csv` | Direct 10,000-replicate equal-dataset crossed query-seed bootstrap output from `10_STATISTICS/TABLE_CROSSED_QUERY_SEED_BOOTSTRAP.csv`, including raw and Holm-adjusted bootstrap p-values. |
| `TABLE_PAIRED_SEED_SENSITIVITY.csv` | Five paired evaluation-seed sensitivity analysis. It is supplementary to, not a replacement for, the crossed query-seed bootstrap. |

## Important statistical interpretation

The confirmatory crossed bootstrap resamples queries and evaluation-noise seeds as crossed factors
within each dataset and combines the six datasets with equal weight. The six datasets themselves
are not resampled. Therefore its intervals are conditional on the selected benchmark panel.

`TABLE_LODO_DELTAS.csv` is a dataset-composition sensitivity check. It should not be described as
population-level inference over a random sample of retrieval datasets.

## Document/query nuisance geometry

`TABLE_DOCUMENT_QUERY_NOISE_GEOMETRY.csv` shows that document-side and query-side corruption
residual geometry is measurably different. For the Nomic diagnostic at severity 0.15, the mean
principal angles are about 27.6 degrees for typo corruption and 28.9 degrees for OCR-like
corruption, with normalized covariance distances about 0.664 and 0.691, respectively.

Accordingly, the public evidence should not be summarized as showing document/query covariance
equivalence. The operational question is whether the document-calibrated map suppresses query-side
perturbations sufficiently for robust retrieval.

## Protocol reference

Frozen protocol: `4.0.2-final`.

Pinned model revisions:

- all-MiniLM-L6-v2: `1110a243fdf4706b3f48f1d95db1a4f5529b4d41`
- E5-base-v2: `f52bf8ec8c7124536f0efb74aca902b2995e5bcd`
- nomic-embed-text-v1.5: `e9b6763023c676ca8431644204f50c2b100d9aab`

Datasets: ArguAna, FiQA, NFCorpus, SciFact, SciDocs, and Quora.

Calibration is document-only and qrel-free. Evaluation queries and qrels are not used to fit the
projection.
