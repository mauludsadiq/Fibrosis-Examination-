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
* Weighted CMFI variant
* Mechanics prediction layer
* Fibrosis progression trajectory
* Cohort-level fibrosis analysis
* Source-derived cohort metrics
* Perturbation testing
* Panel ranking analysis
* CSV-driven execution path

Source Datasets

data/fibrosis_expr.csv
Raw fibrosis expression matrix.

data/fibrosis_clinical.csv
Clinical fibrosis stage labels.

data/cmfi_panel_v3_from_stage.csv
Derived CMFI cohort outputs.

Scientific Result

The repository derives fibrosis state directly from raw source expression data inside FARD.

Full Cohort Result

Samples analyzed:
15

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

Weighted CMFI Result

A weighted CMFI variant was tested using panel stage-separation deltas.

Weighted CMFI preserved monotonic stage separation:

Stage 0:
~0.006–0.026

Stage 1:
~0.473–0.493

Stage 2:
~0.857–0.912

Stage 3:
~1.210–1.215

Stage 4:
~1.520–1.541

The weighted variant compresses scale while preserving ordering.

Top Biological Separators

Stage-4 minus Stage-0 panel deltas:

1. proteoglycan_fc  0.95410
2. tgfb_fc          0.92503
3. mineral_fc       0.89931
4. collagen_fc      0.87616
5. elastin_fc       0.87443
6. mmp_fc           0.86642
7. tf_ecm_fc        0.85745
8. timp_fc          0.85384
9. lox_fc           0.85313
10. inflammation_fc 0.84933

Key Observation

Proteoglycan signaling is the strongest fibrosis-stage separator in the cohort.

TGFβ and mineralization signaling also strongly increase with fibrosis stage.

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

The fibrosis signal is reconstructed directly from the expression matrix inside FARD.

The repository is no longer dependent on:
* hardcoded fibrosis scores
* precomputed CMFI outputs
* scaffolded test vectors

The fibrosis trajectory is source-derived and reproducible from the raw cohort matrix.

Generated Outputs

out/cohort_flat.csv
Flattened cohort export table with:
* sample_id
* clinical stage
* CMFI
* latent coordinates
* active panel fold-changes

out/cohort_report/result.json
Full cohort metrics report.

out/panel_importance/result.json
Panel stage-separation ranking report.

out/weighted_cmfi/result.json
Weighted CMFI cohort outputs.

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
cohort_export.fard
panel_rankings.fard
weighted_cmfi.fard

tests/

test_*.fard

run_cohort_report.fard
run_panel_importance.fard
run_panel_rankings.fard
run_weighted_cmfi.fard
run_stage_trajectories.fard
run_export_cohort_table.fard

Core Commands

fardrun test --program tests/test_expression_csv_kernel.fard

fardrun test --program tests/test_cohort_analysis.fard

fardrun test --program tests/test_cohort_metrics.fard

fardrun run --program tests/run_cohort_report.fard --out out/cohort_report

fardrun run --program tests/run_panel_importance.fard --out out/panel_importance

fardrun run --program tests/run_weighted_cmfi.fard --out out/weighted_cmfi

