## Reproducibility

Running this notebook from top to bottom gives the numbers in our report and slides.

### Setup
- Python 3.8 or newer with numpy, pandas, matplotlib and jupyter (`pip install numpy pandas matplotlib jupyter`)
- Last tested on our machines with Python 3.13, numpy 2.5.3, pandas 3.0.5, matplotlib 3.11.2
- Dataset: Kaggle "Breast Cancer Wisconsin (Diagnostic) Data Set", saved as `data.csv` next to this notebook.
- The raw UCI `wdbc.data` has no header and will not work as it has the Unnames: 32 and 'id','diagnosis' coloumns. After removing those we will be left with 30 features in total which are in data.csv

### Essential checklist for reproducability 
- Seed 42 for the stratified 70/15/15 split and ofcourse throughout all the random generators we have used the same seed onl difference is in seeds 42, 43, 44 for the 3 cross-validation repeats
- Weights start at zero and training is full-batch gradient descent

### How to run
- Use Restart & Run All 
- Seed,lambda grid,tolerance of 1^-6, learning rate of 0.5 and iteration limit of 20000 should not be changed. Here learning should not be changed as from the naive method of the table it will always choose eta=5 which is not feasable to our model. Whole reason is stated in the report and colab file also.
- We should always run the cells in order. It may happen that a function is defined in above cells as helper and is used many times below so it will need that cell to be executed first. 

### Known Issues
- The eta=10 may crash on some variants on some pc as it is shown just for the referance that higher etas misbalance and jump along the target. 
### Hold out data is set to be used for our last comparision with 2 more models to compare which is best. 
