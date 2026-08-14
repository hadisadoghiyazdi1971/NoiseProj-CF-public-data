# Data availability

## What is included in this repository

- `results/` — 19 generated result tables (CSV), each transcribed or clearly derived from a
  specific LaTeX table shipped in the manuscript/supplementary source of the submitted paper
  (frozen protocol `4.0.2-final`). Exact provenance for every file is documented in
  [`metadata/README_RESULTS.md`](metadata/README_RESULTS.md).
- `metadata/CLAIM_EVIDENCE_MATRIX.csv` — a mapping from the paper's quantitative claims to the
  result table(s) that support them.

## What is explicitly not included, and why

- **Leave-one-dataset-out (LODO) sensitivity deltas.** The manuscript mentions this as a partial
  robustness check but ships no corresponding table in the LaTeX source available for this release.
  No LODO CSV is included; see the "Not included in this release" section of
  `metadata/README_RESULTS.md`.
- **Raw BEIR corpora and qrels.** ArguAna, FiQA, NFCorpus, SciFact, SciDocs, and Quora are
  third-party public benchmark datasets assembled by the BEIR project (Thakur et al., 2021, NeurIPS
  Datasets & Benchmarks). They are not redistributed here; obtain them from the official BEIR
  release under their own license terms.
- **Pretrained encoder weights.** all-MiniLM-L6-v2, E5-base-v2, and nomic-embed-text-v1.5 are
  third-party models with their own licenses; exact pinned revisions are listed in
  `metadata/README_RESULTS.md` / the manuscript's supplementary protocol table.
  They are not redistributed here.
- **Implementation / frozen source code, raw per-query outputs, figures, and the manuscript PDF.**
  The manuscript's own "Reproducibility and artifact availability" section describes a separate
  source artifact (implementation, frozen protocol, cache builder, notebooks, statistical analysis
  workflow) and analysis artifact (per-dataset summaries, per-query and crossed query–seed bootstrap
  outputs, figures, run-completeness audit). Those artifacts are not part of this results-only
  release. Contact the corresponding author for their availability.

## Corresponding author

Hadi Sadoghi Yazdi — h-sadoghi@um.ac.ir
Department of Computer Engineering, Faculty of Engineering, Ferdowsi University of Mashhad, Mashhad, Iran

## Status note

The associated manuscript is submitted to *Data & Knowledge Engineering* and, as of the date of
this release, has not completed peer review. Reported values reflect the frozen protocol at
submission time and may be revised in a later published version.
