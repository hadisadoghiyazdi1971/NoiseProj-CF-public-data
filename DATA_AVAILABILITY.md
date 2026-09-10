# Data availability

## Included

This repository provides processed result tables for the frozen core protocol `4.0.2-final` and the targeted extension grid `information-sciences-new-experiments-v2`.

The core tables cover main and secondary effectiveness, dataset-level results, dominance, dimensional efficiency, ranking stability, unseen corruption, observed OCR, cross-corpus transfer, system measurements, bootstrap inference, evaluation-seed sensitivity, calibration-seed stability, leave-one-dataset-out sensitivity, and query/document residual geometry.

The extension tables cover:

- recent-adaptor clean and noisy equal-dataset summaries;
- dataset- and severity-level recent-adaptor results;
- training-seed stability;
- clean, query-only, document-only, and joint corruption-location results;
- NoiseProj-CF comparisons with Full and PCA;
- corruption retention, asymmetry, and joint-corruption interaction;
- the extension completeness audit.

Exact per-file provenance and interpretation constraints are documented in [`metadata/README_RESULTS.md`](metadata/README_RESULTS.md). The claim-to-evidence mapping is provided in [`metadata/CLAIM_EVIDENCE_MATRIX.csv`](metadata/CLAIM_EVIDENCE_MATRIX.csv).

## Not included

- Raw BEIR corpora and qrels
- Pretrained encoder weights
- Raw per-query outputs and complete run directories
- Source implementation and experiment notebooks
- Manuscript or submission files
- Third-party model or dataset licenses

These exclusions avoid redistributing third-party assets and prevent the public processed-results release from being mistaken for the complete private reproducibility archive.

## Statistical interpretation

The core crossed bootstrap resamples query IDs and evaluation-noise seeds within each dataset and resamples the six observed dataset contributions with equal weight. Its intervals quantify sensitivity within the observed benchmark panel and to its composition; they are not unrestricted population inference over all retrieval benchmarks.

The new recent-adaptor and corruption-location comparisons are descriptive. Training-seed and evaluation-seed dispersion is released, but no new paired-query significance claim against NoiseProj-CF is made.

## Pinned encoder revisions

| Encoder | Revision |
|---|---|
| all-MiniLM-L6-v2 | `1110a243fdf4706b3f48f1d95db1a4f5529b4d41` |
| E5-base-v2 | `f52bf8ec8c7124536f0efb74aca902b2995e5bcd` |
| nomic-embed-text-v1.5 | `e9b6763023c676ca8431644204f50c2b100d9aab` |

## Manuscript status

The associated manuscript, **NoiseProj-CF: Noise-Adjusted Low-Rank Projection for Compact and Corruption-Robust Dense Retrieval**, is prepared for submission to *Information Sciences*. No acceptance, DOI, volume, issue, or page assignment is claimed.

## Corresponding author

Hadi Sadoghi Yazdi - `h-sadoghi@um.ac.ir`
Department of Computer Engineering, Faculty of Engineering, Ferdowsi University of Mashhad, Mashhad, Iran
