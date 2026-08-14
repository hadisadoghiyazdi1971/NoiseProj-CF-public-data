# NoiseProj-CF — Public Results Data

Public results/data companion to:


> **NoiseProj-CF: Noise-Adjusted Low-Rank Indexing for Compact and Corruption-Robust Dense Retrieval**
> Amirreza Taghaddosi, Hadi Sadoghi Yazdi
> Department of Computer Engineering, Faculty of Engineering, Ferdowsi University of Mashhad, Mashhad, Iran
> Submitted to *Data & Knowledge Engineering* (Elsevier), 14 August 2026 — **currently under review, not yet published.**

> If you are reading this before the manuscript is accepted: the numbers below are the frozen
> results of protocol `4.0.2-final` as submitted. They may be revised during peer review. This
> repository will be updated with the DOI, volume/issue, and a permanent journal link once the
> paper is published — **TBD, to be filled in after publication.**

## What this is

Dense retrieval represents queries and documents as fixed-dimensional vectors, but high-dimensional
indexes are costly and frozen embeddings can be brittle to misspellings and OCR-like corruption.
NoiseProj-CF learns one shared low-rank map from clean corpus embeddings and paired corrupted
document views — no relevance labels, no encoder retraining — by solving a regularized
noise-adjusted generalized eigenproblem, and applies it symmetrically to queries and documents
before indexing. Across six BEIR datasets and three embedding families, NoiseProj-CF-128 has the
highest mean noisy NDCG@10 among the evaluated compact (128-D) methods for every encoder, and a
128-D Nomic/Quora Flat index cuts vector/index storage by 83.3% while raising measured throughput
4.7x relative to the full 768-D representation.

This repository contains the **generated result tables** (CSV) that support the manuscript's
tables and claims, plus a claim→evidence cross-reference. It does **not** contain the manuscript
text/figures, the implementation, or the raw BEIR corpora — see [`DATA_AVAILABILITY.md`](DATA_AVAILABILITY.md).

## Repository structure

```
NoiseProj-CF-public-data/
├── README.md                    this file
├── CITATION.cff                 machine-readable citation metadata
├── DATA_AVAILABILITY.md         what is / isn't included, and where the rest lives
├── LICENSE_NOTICE.md            license for the contents of this repository
├── results/                     20 result tables in CSV, one per manuscript/supplementary table
└── metadata/
    ├── CLAIM_EVIDENCE_MATRIX.csv   paper claims mapped to the CSV(s) that support each one
    └── README_RESULTS.md           per-table provenance: exact LaTeX source, merges, derivations, gaps
```

Start with [`metadata/README_RESULTS.md`](metadata/README_RESULTS.md) — it documents, table by
table, exactly which LaTeX source each CSV was transcribed from, which tables are re-derived views
of the same numbers (clearly marked as such), and the one requested table
(leave-one-dataset-out deltas) that is **not** included because no such data is shipped anywhere in
the submitted manuscript/supplementary source.

## Protocol summary

- Frozen protocol version: `4.0.2-final` (no changes after the confirmatory runs)
- Datasets: ArguAna, FiQA, NFCorpus, SciFact, SciDocs, Quora (BEIR)
- Encoders: all-MiniLM-L6-v2 (384-D), E5-base-v2 (768-D), nomic-embed-text-v1.5 (768-D)
- Calibration: document-only, qrel-free; evaluation queries/qrels never used to fit the projection
- Primary metric: NDCG@10; secondary: Recall@100, MRR@10, MAP@100
- Inference: paired query bootstrap (10,000 replicates) and equal-dataset crossed query–seed
  bootstrap, Holm-corrected over confirmatory comparisons

## How to cite

See [`CITATION.cff`](CITATION.cff). Until the manuscript is published, please contact the
corresponding author (Hadi Sadoghi Yazdi, h-sadoghi@um.ac.ir) for citation guidance.

## License

The contents of `results/` and `metadata/` are released under **CC-BY 4.0** — see
[`LICENSE_NOTICE.md`](LICENSE_NOTICE.md). The manuscript text and figures are **not** covered by
this license; they remain under the authors' copyright pending the journal's editorial decision.
