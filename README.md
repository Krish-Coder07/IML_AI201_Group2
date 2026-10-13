# IML_AI201_Group2

Breast cancer diagnosis on the Wisconsin Diagnostic (WDBC) dataset using a logistic regression written from scratch in NumPy. This is Part 1 (before midsem) of our AI201 project at IIIT Delhi.

Team: Nikhil Kumar Karn (2025338), Yaman Kumar (2025561), Krish Gupta (2025269), Harshit Singh (2025224)

## What is in this repo

- `AI_Project(Before Midsem).ipynb`: the full Part 1 notebook (EDA, preprocessing, baseline model, validation, cross-validation)
- `data.csv`: the dataset (Kaggle version of Breast Cancer Wisconsin Diagnostic)

## Requirements

- Python 3.8 or newer
- numpy, pandas, matplotlib, jupyter
- Install with `pip install numpy pandas matplotlib jupyter`
- Last tested with Python 3.13, numpy 2.5.3, pandas 3.0.5, matplotlib 3.11.2
- No scikit-learn. The model, split, k-fold, metrics and AUC are all hand-written

## How to run

- Clone the repo and keep `data.csv` in the same folder as the notebook (the notebook reads `data.csv` by relative path)
- Open the notebook and use Kernel > Restart & Run All (Colab: Runtime > Restart session and run all)
- A full run took about 40 seconds on our test machine

## Why the results are repeatable

- One fixed seed (42) for the 70/15/15 stratified split
- Cross-validation uses seeds 42, 43 and 44 for its 3 repeats
- Training is deterministic: weights start at zero and we use full-batch gradient descent, so there is no random initialisation or mini-batch shuffling
- The hold-out set is created but not evaluated anywhere in Part 1

## Things to watch out for

- Run cells top to bottom, once. The random generator is stateful, so re-running only the split cell gives a different split. If you re-run anything, restart and run all again
- Do not edit or re-save `data.csv`. It should have 569 rows and 33 columns (`id`, `diagnosis`, 30 features, and an empty `Unnamed: 32`). The raw UCI `wdbc.data` has no header and will not work
- Do not change the seed, learning rate (0.5), tolerance (1e-6), iteration limit (20000) or the lambda grid
- Known cell-order issue: the cell starting with `etas_to_compare = [5, 1.5, 1.0, 0.5]` in Section 4.2 calls `lambda_sweep`, which is defined in the cell right after it. On a fresh run it stops with `NameError: name 'lambda_sweep' is not defined`. Run the next cell (`def lambda_sweep(eta):`), then continue from the failed cell. Results do not change. Moving the `def` cell above it fixes this
- The eta = 10 row in the learning rate table is an unstable run that oscillates, so its last digits depend on the machine and library versions. On our re-run it gave final objective 0.100056 with 11095 loss increases, while our original run gave 0.101293 and 11106. The conclusion is the same (it never converges). All other rows matched exactly

## Expected results

If your numbers match these, the run is reproduced.

| Notebook section | Expected output |
|---|---|
| 1.3 Class distribution | Benign 357 (62.74%), Malignant 212 (37.26%) |
| 1.4 Missing values and duplicates | 0 and 0 |
| 3. Split sizes (benign / malignant) | fit 249 / 148, validation 53 / 31, hold-out 55 / 33 |
| 4.0 Tolerance check, iterations | 1e-2: 125, 1e-4: 1949, 1e-6: 4708, 1e-8: 7633 |
| 4.1 Learning rate (lambda = 0.01) | converged for 0.1, 0.5, 1, 1.5, 5 (7374, 1476, 743, 500, 156 iterations); 0.01 and 10 do not converge; final objective 0.099961; selected eta = 0.5 |
| 4.2 L2 strength | best lambda = 0.003, validation BCE 0.080624, weight norm 3.2696; lambda = 0 and 1e-4 do not converge at eta = 0.5 |
| eta = 5 vs eta = 0.5 | at eta = 5, lambda = 0.1 gives BCE 0.9487 (not converged) and lambda = 1 gives NaN; at eta = 0.5 every lambda from 0.001 up converges |
| 4.3 Validation, threshold 0.5 | accuracy 0.9762, confusion matrix [[53, 0], [2, 29]], recall 0.9355, specificity 1.0, precision 1.0, F1 0.9667, AUC 0.9957 |
| 4.4 Best threshold (5 FN + FP) | 0.15 (0 FN, 4 FP) |
| 5. Single 5-fold CV | recall 0.9440, specificity 0.9901, F1 0.9622, AUC 0.9928 |
| 6. Repeated CV (5-fold x 3) | recall 0.9404, specificity 0.9879, F1 0.9586, AUC 0.9918 |
| 6.1 Out-of-fold threshold, 5:1 cost | 0.25 (FN 7.3, FP 15.3; at 0.5 it is FN 10.7, FP 3.7) |
| 6.1 Best threshold by cost ratio | 1:1: 0.60, 2:1: 0.50, 5:1: 0.25, 10:1: 0.05 |

## Limitations

- Learning rate, lambda and threshold were tuned on the validation set, which is also part of the CV data, so the CV numbers are slightly optimistic. Nested CV is planned after midsem
- The 5:1 FN to FP cost ratio is our assumption, not a measured clinical value
- Feature selection, calibration, other models and noise robustness are part of Part 2
