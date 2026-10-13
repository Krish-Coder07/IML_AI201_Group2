# IML_AI201_Group2

Breast cancer diagnosis on the Wisconsin Diagnostic (WDBC) dataset using a logistic regression written from scratch in NumPy. This is Part 1 (before midsem) of our AI201 project at IIIT Delhi.

Team: Nikhil Kumar Karn (2025338), Yaman Kumar (2025561), Krish Gupta (2025269), Harshit Singh (2025224)

## What is in this repo

- `AI_Project(Before Midsem).ipynb`: the full Part 1 notebook (EDA, preprocessing, baseline model, validation, cross-validation)
- `data.csv`: the dataset (Kaggle version of Breast Cancer Wisconsin Diagnostic)


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

