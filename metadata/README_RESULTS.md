# Results index — NoiseProj-CF

Every CSV in [`../results/`](../results/) is a direct transcription of a table that ships in the
manuscript or supplementary LaTeX source (frozen scientific protocol `4.0.2-final`), or an
explicitly-labeled re-derivation/subset of one of those tables. No experimental value in this
release was invented, estimated, or back-filled; where a requested table has no corresponding
source data, that is stated below and the file is omitted rather than filled with placeholder
numbers.

All effectiveness figures are NDCG@10 unless a column name says otherwise. "Noisy" always means
the equal-dataset macro average over the frozen evaluation-noise grid (typo-char and OCR-like
corruption at severities 0.05/0.15/0.25, each averaged over five evaluation seeds:
10011/10023/10037/10042/10053), computed with no relevance labels used at fit time.

## Direct transcriptions (one source table each)

| CSV | Source (LaTeX table) | Notes |
|---|---|---|
| `TABLE_MAIN_clean_vs_mean_noisy.csv` | `tables/main_effectiveness.tex` (`tab:main`) | Reshaped from wide (per-encoder columns) to long/tidy format. |
| `TABLE_SECONDARY_METRICS.csv` | `tables/supp_secondary.tex` (`tab:supp-secondary`) | Recall@100, MRR@10, MAP@100. |
| `TABLE_DATASET_LEVEL.csv` | `tables/datasets.tex` (`tab:datasets`) | Corpus sizes and qrel-free fit-document caps; not a retrieval-effectiveness table. |
| `TABLE_RANKING_STABILITY_MACRO.csv` | `tables/supp_ranking.tex` (`tab:suprank`) | Averaged across the six main noisy conditions. |
| `TABLE_CLASSICAL_BASELINES.csv` | `tables/supp_classical.tex` (`tab:supclassical`) | Four-dataset MiniLM subset only, as in the source. |
| `TABLE_OBSERVED_OCR.csv` | `tables/ocr.tex` (`tab:ocr`) | Effectiveness under the observed render→degrade→Tesseract pipeline. |
| `TABLE_UNSEEN_GENERALIZATION.csv` | `tables/unseen.tex` (`tab:unseen`) | Four NLPaug generators never used to calibrate the method. |
| `TABLE_SYSTEM_FULL.csv` | `tables/supp_system.tex` (`tab:supp-system`) | Complete Quora/Nomic Flat/PQ/OPQ benchmark. |
| `TABLE_SYSTEM_PARETO.csv` | `tables/system_flat.tex` (`tab:system`) | Flat-index-only subset used for the main-text storage/throughput/quality trade-off figure. |
| `TABLE_CROSSED_QUERY_SEED_BOOTSTRAP.csv` | `tables/crossed_query_seed_stats.tex` (`tab:crossedstats`) | Confirmatory 10,000-replicate bootstrap, Holm-corrected over 15 comparisons. |
| `TABLE_PAIRED_SEED_SENSITIVITY.csv` | `tables/supp_fitseed.tex` (`tab:supp-fitseed`) | This is **calibration-seed** (fit-seed) sensitivity — the closest available "seed sensitivity" data. It is not a per-evaluation-noise-seed breakdown; no such table is shipped. |

## Merged tables (same measurement, two source tables)

- **`TABLE_REALIZED_CORRUPTION.csv`** combines `tables/supp_realized.tex` (synthetic typo/OCR-like
  corruption statistics, averaged across datasets/encoders) and `tables/supp_ocrstats.tex`
  (observed render→degrade→Tesseract statistics, per dataset). A `corruption_source` column
  distinguishes the two row sets; columns that don't apply to a given source are left blank.

## Derived / re-expressed tables (same underlying numbers, no new measurements)

- **`TABLE_NOISEPROJ_DOMINANCE.csv`** is the full pairwise dominance table from
  `tables/dominance.tex` (`tab:dominance`), including the `Full` reference row.
- **`TABLE_COMPACT_WIN_COUNTS.csv`** is the same table restricted to the four compact baselines
  (PCA/SVD/GaussianRP/DAE), i.e. dominance over compact competitors only, excluding `Full`.
- **`TABLE_DIMENSION_PARETO.csv`** adds a `pareto_optimal_dim_vs_noisy` flag to
  `TABLE_DIMENSION_EFFICIENCY.csv` (source: `tables/dimension_key.tex`, `tab:dimension`). The flag
  marks points not dominated on the two-objective frontier (minimize `dim`, maximize
  `noisy_ndcg10`) **within each encoder**. It intentionally ignores clean NDCG, so a point being
  "Pareto-optimal" here is not a claim that it is best overall — see `TABLE_DIMENSION_EFFICIENCY.csv`
  for the clean-NDCG trade-off the frontier omits.
- **`TABLE_DIMENSION_EFFICIENCY.csv`** additionally reports `pct_of_full_clean_ndgc10` computed as
  `clean_ndcg10 / (Full clean_ndcg10 for the same encoder)`. Values were computed from the rounded
  numbers in `tables/dimension_key.tex`; the manuscript's prose cites 99.3% (MiniLM-256) and ~97.7%
  (Nomic-256) from its own unrounded internal source, so the Nomic figure here (97.8%) differs by
  0.1 point due to rounding — both are transcribed/derived, not independently fabricated.
- **`TABLE_TRANSFER_REGRET.csv`** re-expresses `tables/supp_transfer.tex` (`tab:supp-transfer`) as
  a one-sided "regret" (`max(0, -delta)`), i.e. the noisy-NDCG cost of using the best foreign-fitted
  projection instead of in-domain calibration. The Quora row has zero regret because foreign
  transfer very slightly *helped* there.
- **`TABLE_NATIVE_MRL.csv`** combines one row pair from `tables/dimension_key.tex` (four-dataset
  ArguAna/FiQA/SciFact/Quora panel) with a second row pair whose numbers (0.224→0.274 noisy NDCG,
  0.450 vs 0.447 clean NDCG) appear only in `manuscript.tex` prose (Sec. "RQ2: dimension efficiency
  and native Matryoshka"), not in any shipped LaTeX table. The `source` column marks this explicitly.

## Not included in this release

- **`TABLE_LODO_DELTAS.csv` (leave-one-dataset-out sensitivity) — not available.** The manuscript
  refers to a LODO sensitivity check (`manuscript.tex`, Sec. 5.5: "Leave-one-dataset-out sensitivity
  in the supplement is a partial check") and again in the Sec. 8 "Metrics and statistical inference"
  paragraph, but no LODO numbers appear in any `.tex` table shipped with this submission package.
  Rather than reconstruct plausible-looking numbers, this table is omitted. It may exist in the
  authors' full analysis archive (see `../DATA_AVAILABILITY.md`).
- Deployment-coordinate ablation (`tables/supp_deployment.tex`), the Quora fit-size sweep
  (`tables/supp_fitsize.tex`), and the full 180-row per-query paired bootstrap
  (`tables/supp_queryboot.tex` ships only a 42-row Full/PCA subset) were not requested in this
  release's file list and are not included as separate CSVs. They exist in the LaTeX source and can
  be added on request.

## Protocol reference

Frozen protocol: `4.0.2-final`. Encoders: all-MiniLM-L6-v2 (384-D), E5-base-v2 (768-D),
nomic-embed-text-v1.5 (768-D). Datasets: ArguAna, FiQA, NFCorpus, SciFact, SciDocs, Quora (BEIR).
Calibration is document-only and qrel-free; evaluation queries/qrels are never used to fit the
projection. Full protocol details are in `tables/supp_protocol.tex` and `tables/supp_encoders.tex`
in the manuscript source.
