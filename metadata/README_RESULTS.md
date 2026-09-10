# Results index - NoiseProj-CF

The public CSVs in [`../results/`](../results/) are exported from the validated core and extension analysis records. Values are not reconstructed from rounded PDF tables.

All primary effectiveness values are NDCG@10 unless a column states otherwise.

## Core result tables

The existing `TABLE_MAIN_*`, `TABLE_DATASET_*`, `TABLE_SECONDARY_*`, `TABLE_NOISEPROJ_*`, `TABLE_COMPACT_*`, `TABLE_DIMENSION_*`, `TABLE_NATIVE_*`, `TABLE_CLASSICAL_*`, `TABLE_RANKING_*`, `TABLE_REALIZED_*`, `TABLE_OBSERVED_*`, `TABLE_UNSEEN_*`, `TABLE_TRANSFER*`, `TABLE_SYSTEM_*`, `TABLE_FIT_*`, `TABLE_PAIRED_*`, `TABLE_CROSSED_*`, `TABLE_LODO_*`, and `TABLE_DOCUMENT_QUERY_*` files support the frozen core protocol `4.0.2-final`.

The confirmatory crossed bootstrap resamples queries and evaluation-noise seeds as crossed factors within each dataset. The six observed dataset-level contributions are then resampled with replacement and averaged with equal dataset weight. The uncertainty therefore reflects within-panel resampling and sensitivity to the composition of the observed benchmark panel, not unrestricted population inference over all possible retrieval tasks.

## Recent-adaptor extension

| CSV | Meaning |
|---|---|
| `TABLE_MODERN_ADAPTORS_MACRO.csv` | Equal-dataset clean and overall-noisy metrics for each encoder and baseline. |
| `TABLE_MODERN_ADAPTORS_DATASET.csv` | Dataset-level clean and noisy metrics. |
| `TABLE_MODERN_ADAPTORS_SEVERITY.csv` | Equal-dataset results by corruption family and severity. |
| `TABLE_MODERN_ADAPTORS_SEED_STABILITY.csv` | Mean, SD, range, and extrema across three training seeds. |

The panel covers ArguAna, FiQA, SciFact, and Quora with MiniLM and Nomic at 128 dimensions. `Matryoshka-Adaptor (independent)` is an independent unsupervised implementation. `SMEC-QF` is a qrel-free SMEC-inspired adaptation that excludes the published relevance-based rank loss. Neither result is an official author-code reproduction. The public tables support descriptive mean comparisons only.

## Corruption-location extension

| CSV | Meaning |
|---|---|
| `TABLE_CORRUPTION_LOCATION_MACRO.csv` | Equal-dataset clean and scenario-specific metrics by method and corruption family. |
| `TABLE_CORRUPTION_LOCATION_CELLS.csv` | Dataset/family/scenario cells and NoiseProj-CF deltas versus Full and PCA. |
| `TABLE_CORRUPTION_LOCATION_RETENTION.csv` | Seed-aggregated absolute clean drops and retention fractions. |
| `TABLE_CORRUPTION_LOCATION_WIN_LOSS.csv` | Descriptive NoiseProj-CF win/tie/loss counts versus Full and PCA. |
| `TABLE_CORRUPTION_LOCATION_INTERACTION.csv` | Equal-dataset query/document asymmetry and joint-corruption interaction. |

The panel covers ArguAna, NFCorpus, and SciFact with Nomic at severity 0.15 under five evaluation-noise seeds. The four scenarios are clean, query-only, document-only, and joint query/document corruption. Positive joint-interaction values indicate subadditive degradation on the NDCG scale and should not be interpreted causally.

## Extension audit

[`EXTENSION_AUDIT.json`](EXTENSION_AUDIT.json) records:

- 1488 modern-adaptor result rows;
- 48/48 unique modern-adaptor execution units;
- 360 corruption-location result rows;
- 30/30 unique corruption-location execution units;
- no missing, extra, duplicate, or malformed protocol cells.

## Interpretation guards

- No qrel, relevance label, evaluation query, or retrieval metric is used to fit NoiseProj-CF or either qrel-free extension baseline.
- Recent-adaptor SD values describe variation across training seeds.
- Corruption-location SD values describe variation across evaluation-noise seeds.
- Equal-dataset macros give each dataset equal weight.
- The extension does not provide a new paired-query significance test against NoiseProj-CF.
- Full remains an uncompressed reference and is stronger in several absolute comparisons.
