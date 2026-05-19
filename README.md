Fibrosis Examination

FARD rebuild of the CMFI fibrosis examination stack.

Current status

Implemented in FARD:

* Panel definitions: 27 v3 fields
* Active panel list: 10 CMFI-active fields
* Latent parameters: panel_stage_v3
* Panel activity
* Log2 panel fold-change
* CMFI scalar
* Mechanics prediction layer
* CMFI progression
* Integrated sample kernel
* CSV-derived execution from raw fibrosis expression data

Scientific result

The repository now derives CMFI directly from the raw fibrosis expression dataset:

data/fibrosis_expr.csv
-> panel activity
-> baseline-normalized log2 fold-change
-> latent fibrosis coordinates
-> CMFI scalar
-> mechanics predictions
-> progression trajectory

For the highest-stage fibrosis sample:

sample_id: sample_4_3

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

dphi_res  ≈ 2.865
dkappa_A  ≈ 1.4325
dkappa_B  ≈ 1.4325

Derived CMFI:

CMFI ≈ 4.963

Meaning:

The fibrosis signal is now reproduced directly from source expression data inside FARD rather than from hardcoded or precomputed CMFI values.

Test commands

fardrun test --program tests/test_panel_definitions.fard
fardrun test --program tests/test_latent_params.fard
fardrun test --program tests/test_cmfi_core.fard
fardrun test --program tests/test_panel_activity.fard
fardrun test --program tests/test_panel_fold_change.fard
fardrun test --program tests/test_mechanics.fard
fardrun test --program tests/test_progression.fard
fardrun test --program tests/test_kernel_with_mechanics.fard
fardrun test --program tests/test_expression_csv_kernel.fard

Repository layout

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

tests/
test_*.fard

data/
fibrosis_expr.csv
fibrosis_clinical.csv
cmfi_panel_v3_from_stage.csv
