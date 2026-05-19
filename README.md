Fibrosis Examination

FARD rebuild of the CMFI fibrosis examination stack.

Repository

 [oai_citation:0‡github.com](https://github.com/mauludsadiq/Fibrosis-Examination-.git?utm_source=chatgpt.com)

Overview

This repository reconstructs the CMFI fibrosis pipeline directly in FARD using source fibrosis expression data.

The system derives fibrosis state from raw gene expression rather than consuming precomputed fibrosis scores.

Pipeline

fibrosis_expr.csv
-> panel activity
-> baseline-normalized log2 fold-change
-> latent fibrosis coordinates
-> CMFI scalar
-> mechanics predictions
-> progression trajectory

Implemented Components

* Panel definitions (27 v3 fibrosis fields)
* Active CMFI fibrosis panels
* Latent parameter model
* Panel activity computation
* Baseline-normalized log2 fold-change
* CMFI latent coordinate projection
* CMFI scalar derivation
* Mechanics prediction layer
* Fibrosis progression trajectory
* Cohort-level fibrosis analysis
* Source-derived cohort metrics
* Perturbation testing
* CSV-driven execution path

Source Datasets

data/fibrosis_expr.csv
Raw fibrosis expression matrix.

data/fibrosis_clinical.csv
Clinical fibrosis stage labels.

data/cmfi_panel_v3_from_stage.csv
Derived CMFI cohort outputs.

Scientific Result

The repository now derives fibrosis state directly from raw source expression data inside FARD.

Full Cohort Result

Samples analyzed: 15

Clinical-stage correlation:

Spearman rho:
0.9819805060619657

Pearson r:
0.9963393254261786

Misrankings:
None

Mean CMFI by Clinical Stage

Stage 0:
0.05947

Stage 1:
1.53357

Stage 2:
2.77992

Stage 3:
3.84588

Stage 4:
4.83984

This produces a monotonic fibrosis-stage separation directly from the source expression matrix.

Highest Fibrosis Sample

sample_id:
sample_4_3

Derived panel fold-changes:

collagen        0.86018
elastin         0.85133
lox             0.84557
mmp             0.85952
timp            0.87560
mineral         0.91534
proteoglycan    0.99227
inflammation    0.86028
tgfb            0.91496
tf_ecm          0.90659

Derived latent coordinates:

dphi_res:
2.8168799438241177

dkappa_A:
1.4084399719120588

dkappa_B:
1.4084399719120588

Derived CMFI:

4.878979181525136

Interpretation

The fibrosis signal is now reconstructed directly from the expression matrix inside FARD.

The repository is no longer dependent on:
* hardcoded fibrosis scores
* precomputed CMFI outputs
* scaffolded test vectors

The fibrosis trajectory is source-derived and reproducible from the raw cohort matrix.

Repository Layout

fard_cmfi/

panel_definitions.fard
latent_params.fard
panel_activity.fard
panel_fold_change.fard
cmfi_core.fard
fibrosis_kernel.fard
mechanics.fard
progression.fard
kernel_with_mechanics.fard
expression_csv.fard
cmfi_csv.fard
cohort_analysis.fard
cohort_metrics.fard

tests/

test_*.fard
run_cohort_report.fard

Core Tests

fardrun test --program tests/test_expression_csv_kernel.fard

fardrun test --program tests/test_cohort_analysis.fard

fardrun test --program tests/test_cohort_metrics.fard

Cohort Report

fardrun run --program tests/run_cohort_report.fard --out out/cohort_report

