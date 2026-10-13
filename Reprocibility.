## Reproducibility

Running this notebook from top to bottom gives the numbers in our report and slides. All values below were checked by a fresh run.

### Setup
- Python 3.8 or newer with numpy, pandas, matplotlib and jupyter (`pip install numpy pandas matplotlib jupyter`)
- Last tested with Python 3.13, numpy 2.5.3, pandas 3.0.5, matplotlib 3.11.2
- Dataset: Kaggle "Breast Cancer Wisconsin (Diagnostic) Data Set", saved as `data.csv` next to this notebook. Do not edit it. It should have 569 rows and 33 columns (`id`, `diagnosis`, 30 features, empty `Unnamed: 32`). The raw UCI `wdbc.data` has no header and will not work
- A full run takes about a minute

### Why it is repeatable
- Seed 42 for the stratified 70/15/15 split, and seeds 42, 43, 44 for the 3 cross-validation repeats
- Weights start at zero and training is full-batch gradient descent, so there is no random initialisation or shuffling
- Only numpy, pandas and matplotlib are used, with no scikit-learn
- The hold-out set is created but not evaluated in Part 1

### How to run
- Use Restart & Run All (Jupyter: Kernel menu, Colab: Runtime menu)
- Run the cells in order and only once. The random generator keeps its state, so re-running just the split cell gives a different split. If you re-run anything, restart and run all again
- Do not change the seed, learning rate (0.5), tolerance (1e-6), iteration limit (20000) or the lambda grid

### Known issues
- The cell starting with `etas_to_compare = [5, 1.5, 1.0, 0.5]` in Section 4.2 uses `lambda_sweep`, which is defined in the next cell. On a fresh run it raises `NameError: name 'lambda_sweep' is not defined`. Run the next cell, then continue from the failed one. Results do not change
- The eta = 10 row in the learning rate table oscillates, so its last digits depend on the machine and library versions (we saw final objective 0.101293 with 11106 loss increases on one run and 0.100056 with 11095 on another). It never converges either way. Every other value below matched exactly

### Expected values

| Section | Expected output |
|---|---|
| 1.3 Class distribution | Benign 357 (62.74%), Malignant 212 (37.26%) |
| 1.4 Missing values, duplicates | 0 and 0 |
| 3. Split (benign / malignant) | fit 249 / 148, validation 53 / 31, hold-out 55 / 33 |
| 4.0 Tolerance, iterations | 1e-2: 125, 1e-4: 1949, 1e-6: 4708, 1e-8: 7633 |
| 4.1 Learning rate | converged for 0.1, 0.5, 1, 1.5, 5 (7374, 1476, 743, 500, 156 iterations); 0.01 and 10 do not converge; final objective 0.099961; selected eta = 0.5 |
| 4.2 L2 strength | best lambda = 0.003, validation BCE 0.080624, weight norm 3.2696; lambda = 0 and 1e-4 do not converge at eta = 0.5 |
| eta = 5 vs 0.5 | at eta = 5: lambda = 0.1 gives BCE 0.9487 (not converged), lambda = 1 gives NaN; at eta = 0.5 every lambda from 0.001 up converges |
| 4.3 Validation, threshold 0.5 | accuracy 0.9762, confusion matrix [[53, 0], [2, 29]], recall 0.9355, specificity 1.0, precision 1.0, F1 0.9667, AUC 0.9957 |
| 4.4 Best threshold (5 FN + FP) | 0.15 (0 FN, 4 FP) |
| 5. Single 5-fold CV | recall 0.9440, specificity 0.9901, F1 0.9622, AUC 0.9928 |
| 6. Repeated CV (5-fold x 3) | recall 0.9404, specificity 0.9879, F1 0.9586, AUC 0.9918 |
| 6.1 Out-of-fold threshold, 5:1 | 0.25 (FN 7.3, FP 15.3; at 0.5 it is FN 10.7, FP 3.7) |
| 6.1 Threshold by cost ratio | 1:1: 0.60, 2:1: 0.50, 5:1: 0.25, 10:1: 0.05 |
