# Data availability

## What is included in this repository

This repository is a **processed-results release** for the frozen scientific protocol
`4.0.2-final`.

The `results/` directory includes manuscript-facing result summaries and selected validated
sensitivity/diagnostic outputs, including:

- main and secondary retrieval effectiveness;
- per-dataset retrieval effectiveness;
- 128-D dominance and compact-method win counts;
- dimension-efficiency and native-MRL comparisons;
- ranking-stability diagnostics;
- unseen corruption and observed render/degrade/Tesseract OCR results;
- cross-corpus transfer;
- Quora/Nomic Flat/PQ/OPQ system measurements;
- crossed query-seed bootstrap inference;
- paired evaluation-seed sensitivity;
- calibration fit-seed stability;
- leave-one-dataset-out (LODO) sensitivity;
- document-side versus query-side residual-covariance geometry.

Exact per-file provenance is documented in
[`metadata/README_RESULTS.md`](metadata/README_RESULTS.md).

`metadata/CLAIM_EVIDENCE_MATRIX.csv` maps manuscript claims to the public evidence tables that
support them.

## Numerical precision

The public CSVs are generated from the validated final analysis record rather than reconstructed
from rounded PDF/LaTeX displays. Full precision is retained where available. Manuscript tables may
show rounded values.

## What is not included

- **Raw BEIR corpora and qrels.** ArguAna, FiQA, NFCorpus, SciFact, SciDocs, and Quora are
  third-party benchmark datasets distributed through BEIR and are not redistributed here.
- **Pretrained encoder weights.** The models are third-party assets and remain under their own
  licenses.
- **Implementation, notebooks, raw per-query outputs, complete run artifacts, figures, and the
  manuscript PDF.** These are not part of this public processed-results repository.
- **Third-party model or dataset licenses.** This repository's CC BY 4.0 notice does not override
  the licenses of external datasets or pretrained models.

## Pinned encoder revisions

The validated analysis record uses the following model revisions:

| Encoder | Revision |
|---|---|
| all-MiniLM-L6-v2 | `1110a243fdf4706b3f48f1d95db1a4f5529b4d41` |
| E5-base-v2 | `f52bf8ec8c7124536f0efb74aca902b2995e5bcd` |
| nomic-embed-text-v1.5 | `e9b6763023c676ca8431644204f50c2b100d9aab` |

## Manuscript status

The associated manuscript was submitted to *Data & Knowledge Engineering* on 14 August 2026.
This repository does not infer external peer-review status from submission alone. The public
record should be updated when the journal status or bibliographic information changes.

## Corresponding author

Hadi Sadoghi Yazdi — `h-sadoghi@um.ac.ir`
Department of Computer Engineering, Faculty of Engineering, Ferdowsi University of Mashhad,
Mashhad, Iran
