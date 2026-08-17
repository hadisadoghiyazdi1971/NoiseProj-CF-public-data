# NoiseProj-CF — Public Results Data

Public processed-results companion to:

> **NoiseProj-CF: Noise-Adjusted Low-Rank Indexing for Compact and Corruption-Robust Dense Retrieval**
> Amirreza Taghaddosi, Hadi Sadoghi Yazdi
> Department of Computer Engineering, Faculty of Engineering, Ferdowsi University of Mashhad, Mashhad, Iran
> Submitted to *Data & Knowledge Engineering* (Elsevier) on 14 August 2026; not yet accepted or published.

The values in this repository correspond to the frozen scientific protocol `4.0.2-final`.
The manuscript may be revised during the editorial process, and this repository will be updated
with the DOI, volume/issue, pages, and permanent journal link if the paper is published.

## What this is

Dense retrieval represents queries and documents as fixed-dimensional vectors, but high-dimensional
indexes are costly and frozen embeddings can be brittle to misspellings and OCR-like corruption.
NoiseProj-CF learns one shared low-rank map from clean corpus embeddings and paired corrupted
document views — no relevance labels and no encoder retraining — by solving a regularized
noise-adjusted generalized eigenproblem. The same map is applied to query and document embeddings
before normalization and vector search.

Across six BEIR datasets and three embedding families, NoiseProj-CF-128 has the highest mean noisy
NDCG@10 among the evaluated compact 128-D methods for every encoder. In the Quora/Nomic system
benchmark, a 128-D Flat representation reduces vector/index storage by 83.3% and increases measured
throughput by about 4.7x relative to the full 768-D representation.

This repository contains **processed result tables** supporting the manuscript and selected
sensitivity/diagnostic analyses. It does **not** contain the manuscript, implementation, notebooks,
raw per-query outputs, raw BEIR corpora, or pretrained model weights. See
[`DATA_AVAILABILITY.md`](DATA_AVAILABILITY.md).

## Data precision and provenance

CSV values are generated from the validated final analysis record for protocol `4.0.2-final`.
Full numerical precision is retained where available. Values printed in the manuscript are rounded
for presentation, so recomputing a percentage from a rounded PDF table can differ slightly from
recomputing it from the CSV values here.

The repository also includes:

- leave-one-dataset-out (LODO) sensitivity results;
- document-side versus query-side corruption-residual geometry diagnostics;
- calibration fit-seed stability;
- paired evaluation-seed sensitivity;
- exact crossed query-seed bootstrap outputs.

## Repository structure

```text
NoiseProj-CF-public-data/
├── README.md
├── CITATION.cff
├── DATA_AVAILABILITY.md
├── LICENSE_NOTICE.md
├── results/
│   └── processed CSV result and diagnostic tables
└── metadata/
    ├── CLAIM_EVIDENCE_MATRIX.csv
    └── README_RESULTS.md
```

Start with [`metadata/README_RESULTS.md`](metadata/README_RESULTS.md). It documents the meaning and
provenance of each public CSV and distinguishes direct final-analysis outputs from concise derived
views.

## Protocol summary

- Frozen protocol version: `4.0.2-final`
- Datasets: ArguAna, FiQA, NFCorpus, SciFact, SciDocs, Quora (BEIR)
- Encoders: all-MiniLM-L6-v2 (384-D), E5-base-v2 (768-D), nomic-embed-text-v1.5 (768-D)
- Calibration: document-only and qrel-free; evaluation queries/qrels are not used to fit the projection
- Primary metric: NDCG@10
- Secondary metrics: Recall@100, MRR@10, MAP@100
- Confirmatory inference: equal-dataset crossed query-seed bootstrap with 10,000 replicates and
  Holm correction over the prespecified comparisons
- Dataset-composition sensitivity: leave-one-dataset-out analysis

## How to cite

See [`CITATION.cff`](CITATION.cff). Until publication, cite this dataset directly or contact the
corresponding author, Hadi Sadoghi Yazdi (`h-sadoghi@um.ac.ir`), for citation guidance.

## License

The repository's public result and metadata files are released under **CC BY 4.0** as described in
[`LICENSE_NOTICE.md`](LICENSE_NOTICE.md). The manuscript and figures are not included in this
repository and are not licensed by this repository notice.
