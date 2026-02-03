# Learn Probability Density Functions using Roll-Number-Parameterized Non-Linear Model

## Overview
This repository implements a small experiment that transforms a selected numeric feature (NO2) from `data.csv` using a roll-number-parameterized non-linear transform and fits a parametric probability density model of the form:

[ p^​(z)=c * exp(−λ * (z−μ)^2) ]

The transform used is:
\[
z = x + a_r * sin(b_r * x)
\]
where [ a_r = 0.05 * (r % 7) ] and [ b_r = 0.3 * ((r % 5) + 1) ].  
The code provided targets Google Colab and expects the dataset at `data.csv`.

## Steps
1. Read `data.csv` (robustly handle common encodings).  
2. Select the NO2 column if present, otherwise fall back to the first numeric column.  
3. Compute transform parameters \(a_r\) and \(b_r\) using roll number `102316089`.  
4. Transform each sample \(x\) to \(z\) with z = x + a_r * sin(b_r * x).  
5. Estimate the density of \(z\) with a kernel density estimator and fit the parametric model [ p^​(z)=c * exp(−λ * (z−μ)^2) ] (using nonlinear least squares).  
6. Plot the empirical density, fitted model curve, and report learned parameters.

## Results
Learned parameter values (for roll number `102316089` and the provided data):

- μ (mean) = `25.811311026855478`  
- λ (lambda) = `0.001460711615279084`  
- c (constant) = `0.021562906761539043`

## How to run (Google Colab)
1. Upload `data.csv` to the Colab session (left sidebar → Files → Upload).  
2. Paste the provided notebook cells (or run the repository notebook) and execute cells in order.  
3. Required Python packages: `pandas`, `numpy`, `matplotlib`, `scipy`.

Example (local setup)
```bash
pip install pandas numpy matplotlib scipy
python run_notebook_cells.py  # if you've converted the Colab cells to a script
