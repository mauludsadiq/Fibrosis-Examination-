# Fibrosis Examination

A FARD-native pipeline for computing the Collapse-Mechanical Fibrosis Index (CMFI) from gene expression data.

## What it does

Takes a gene expression matrix and clinical staging CSV as input and produces per-sample CMFI scores, organ mechanics predictions, progression trajectories, and cohort summaries.

The pipeline runs entirely in FARD with no external dependencies beyond the fardrun runtime.

## Pipeline

   expression CSV + clinical CSV
       -> panel fold-changes (27 gene panels)
       -> latent embedding (ridge-fitted weights)
       -> CMFI scalar (sqrt of weighted latent norm)
       -> organ mechanics predictions (cartilage, vessel)
       -> progression trajectories
       -> cohort summary with Spearman rank correlation

## Performance on synthetic fibrosis cohort

   Samples: 15 (stages 0-4, 3 replicates each)
   Pearson r: 0.996
   Spearman rho: 0.982
   Misrankings: 0

## Layout

   fard_cmfi/                  core library modules
     panel_definitions.fard    27 gene panels and active set
     latent_params.fard        fitted weight vector and intercept
     panel_activity.fard       mean expression per panel
     panel_fold_change.fard    log2 fold-change vs baseline
     cmfi_core.fard            dot product, latent embedding, CMFI metric
     fibrosis_kernel.fard      single-sample fold-change to CMFI
     kernel_with_mechanics.fard  adds mechanics and progression
     expression_csv.fard       CSV loader and baseline detection
     cohort_analysis.fard      full cohort CMFI and Spearman rank
     cohort_metrics.fard       stage summary, misrankings, report
     cohort_export.fard        CSV writer for cohort results
     mechanics.fard            linear organ mechanics predictions
     progression.fard          time-stepped CMFI trajectory
     weighted_cmfi.fard        data-driven panel weight variant
     activation_analysis.fard  early vs late panel activation
     panel_trajectories.fard   per-panel fold-change by stage
     summary_export.fard       markdown and CSV summary writer
     viz_export.fard           visualization-ready CSV exports

   tests/                      test and run programs
   data/                       expression and clinical CSVs
   out/                        generated outputs

## Running

   fardrun test --program tests/test_cohort_analysis.fard
   fardrun run --program tests/run_summary_export.fard --out out/summary_export
   fardrun run --program tests/run_viz_export.fard --out out/viz_export

## Key invariants

   dkappa_A + dkappa_B = 0 (kappa conservation enforced in cmfi_core)
   CMFI = sqrt(dphi_res^2 + 4*dkappa_A^2 + 4*dkappa_B^2)
   Baseline samples identified by sample_id prefix sample_0_

## Data

   data/fibrosis_expr.csv       gene expression matrix, genes x samples
   data/fibrosis_clinical.csv   sample_id and fibrosis_stage columns
