
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

Test commands

fardrun test –program tests/test_panel_definitions.fard
fardrun test –program tests/test_latent_params.fard
fardrun test –program tests/test_cmfi_core.fard
fardrun test –program tests/test_panel_activity.fard
fardrun test –program tests/test_panel_fold_change.fard
fardrun test –program tests/test_mechanics.fard
fardrun test –program tests/test_progression.fard
fardrun test –program tests/test_kernel_with_mechanics.fard

Kernel path

gene expression
-> panel activity
-> baseline-normalized log2 fold-change
-> latent fibrosis coordinates
-> CMFI scalar
-> mechanics predictions
-> progression trajectory

Core formula

CMFI = sqrt(dphi_res^2 + 4dkappa_A^2 + 4dkappa_B^2)

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

tests/
test_*.fard
