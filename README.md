# Fibrosis Examination

FARD-native pipeline for the Collapse-Mechanical Fibrosis Index (CMFI).

## Cohort Results (synthetic, n=15, stages 0-4)

Pearson r: 0.9963
Spearman rho: 0.9820
Misrankings: 0

Stage summary (original CMFI, mean +/- SEM):

   Stage 0   0.0595 +/- 0.0108
   Stage 1   1.5336 +/- 0.0136
   Stage 2   2.7799 +/- 0.0471
   Stage 3   3.8459 +/- 0.0027
   Stage 4   4.8398 +/- 0.0160

Top panel drivers by delta stage 4 minus stage 0:

   proteoglycan_fc   0.9541
   tgfb_fc           0.9250
   mineral_fc        0.8993
   collagen_fc       0.8762
   elastin_fc        0.8744

Early vs late activation:

   tf_ecm_fc        66.0 pct achieved by stage 2   Strongly Early
   proteoglycan_fc  60.5 pct achieved by stage 2   Moderately Early
   timp_fc          59.2 pct achieved by stage 2   Moderately Early
   mineral_fc       58.3 pct achieved by stage 2   Moderately Early
   elastin_fc       57.7 pct achieved by stage 2   Moderately Early
   mmp_fc           56.8 pct achieved by stage 2   Balanced
   inflammation_fc  56.6 pct achieved by stage 2   Balanced
   collagen_fc      54.7 pct achieved by stage 2   Balanced
   lox_fc           52.9 pct achieved by stage 2   Balanced
   tgfb_fc          51.7 pct achieved by stage 2   Most Progressive

Kappa conservation: dkappa_A + dkappa_B = 0 enforced for all samples.
CMFI metric: sqrt(dphi_res^2 + 4*dkappa_A^2 + 4*dkappa_B^2)

## Layout

   fard_cmfi/   core library modules
   tests/       test and run programs
   data/        expression and clinical CSVs
   out/         generated outputs

## Running

   fardrun test --program tests/test_cohort_analysis.fard
   fardrun run --program tests/run_summary_export.fard --out out/summary_export
