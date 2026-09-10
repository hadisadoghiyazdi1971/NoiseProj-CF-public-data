# NoiseProj-CF - Public Results Data

Public processed-results companion to:

> **NoiseProj-CF: Noise-Adjusted Low-Rank Projection for Compact and Corruption-Robust Dense Retrieval**
> Amirreza Taghaddosi and Hadi Sadoghi Yazdi
> Department of Computer Engineering, Faculty of Engineering, Ferdowsi University of Mashhad, Mashhad, Iran
> Manuscript prepared for submission to *Information Sciences*.

This release combines the frozen core protocol `4.0.2-final` with the targeted extension grid `information-sciences-new-experiments-v2`.

## Overview

NoiseProj-CF learns a shared low-rank map from clean corpus embeddings and paired corrupted document views without relevance labels or encoder retraining. The same map is applied to query and document embeddings before normalization and vector search.

The core study evaluates six BEIR datasets and three embedding families. NoiseProj-CF-128 attains the highest mean noisy NDCG@10 among the generic compact baselines for each encoder. A targeted extension evaluates independent qrel-free Matryoshka-Adaptor and SMEC-inspired implementations on four datasets with MiniLM and Nomic. A second extension evaluates clean, query-only, document-only, and joint query/document corruption on three datasets with Nomic.

The extension results show that:

- NoiseProj-CF-128 exceeds both tested recent-adaptor implementations on mean noisy NDCG@10 in the four-dataset MiniLM and Nomic panels;
- its advantage over PCA-128 persists for query-only, document-only, and joint corruption;
- Full remains stronger in several clean and noisy absolute comparisons;
- the recent-adaptor results are descriptive comparisons of independent/adapted qrel-free implementations, not official-code reproductions or paired significance tests.

## Repository contents

```text
NoiseProj-CF-public-data/
|-- README.md
|-- CITATION.cff
|-- DATA_AVAILABILITY.md
|-- LICENSE_NOTICE.md
|-- results/
|   |-- core processed result tables
|   |-- TABLE_MODERN_ADAPTORS_*.csv
|   `-- TABLE_CORRUPTION_LOCATION_*.csv
`-- metadata/
    |-- CLAIM_EVIDENCE_MATRIX.csv
    |-- EXTENSION_AUDIT.json
    `-- README_RESULTS.md
```

Start with [`metadata/README_RESULTS.md`](metadata/README_RESULTS.md) for table definitions and interpretation constraints. [`metadata/CLAIM_EVIDENCE_MATRIX.csv`](metadata/CLAIM_EVIDENCE_MATRIX.csv) maps manuscript claims to public evidence.

## Protocol summary

### Core grid

- Protocol: `4.0.2-final`
- Datasets: ArguAna, FiQA, NFCorpus, SciFact, SciDocs, and Quora
- Encoders: all-MiniLM-L6-v2, E5-base-v2, and nomic-embed-text-v1.5
- Calibration: document-only and qrel-free
- Primary metric: NDCG@10
- Core inference: paired query bootstrap and hierarchical equal-dataset dataset-query-seed bootstrap with 10,000 replicates and Holm correction

### Information Sciences extension

- Protocol: `information-sciences-new-experiments-v2`
- Recent-adaptor panel: four datasets, MiniLM and Nomic, 128 dimensions, three training seeds
- Corruption-location panel: three datasets, Nomic, severity 0.15, five evaluation-noise seeds
- Extension audit: 48/48 recent-adaptor units and 30/30 corruption-location units, with no missing or extra configurations
- Extension comparisons: descriptive; no new paired-query significance claim is made

## Data provenance

Public CSV values are exported from validated analysis records rather than reconstructed from rounded manuscript tables. Full precision is retained where available. Values printed in the manuscript are rounded for presentation.

This repository contains processed evidence tables only. It does not redistribute BEIR corpora, qrels, pretrained weights, raw per-query outputs, implementation archives, notebooks, or the manuscript. See [`DATA_AVAILABILITY.md`](DATA_AVAILABILITY.md).

## Citation and license

See [`CITATION.cff`](CITATION.cff). Public result and metadata files are released under CC BY 4.0 as described in [`LICENSE_NOTICE.md`](LICENSE_NOTICE.md).

Corresponding author: Hadi Sadoghi Yazdi (`h-sadoghi@um.ac.ir`).
