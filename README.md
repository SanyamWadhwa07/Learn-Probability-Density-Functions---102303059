# Learn Probability Density Functions — 102303059

**Assignment 1 | Roll Number:** 102303059

## Overview

This project fits a parameterized Gaussian-style Probability Density Function (PDF) to India Air Quality data (NO2 readings), using a roll-number-derived non-linear transformation of the input.

**Dataset:** [India Air Quality Data — Kaggle](https://www.kaggle.com/datasets/shrutibhargava94/india-air-quality-data)  
**Feature used:** `no2` (Nitrogen Dioxide concentration)  
**Data points:** 27,447 (after dropping NaN)

---

## Methodology

### Step 1 — Non-linear Transformation

Each NO2 value `x` is transformed to `z` using:

$$z = T_r(x) = x + a_r \sin(b_r x)$$

Parameters derived from roll number `r = 102303059`:

| Parameter | Formula | Value |
|-----------|---------|-------|
| `a_r` | `0.05 × (r mod 7)` | 0.25 |
| `b_r` | `0.3 × (r mod 5 + 1)` | 1.5 |

### Step 2 — PDF Fitting

The target PDF is:

$$\hat{p}(z) = c \cdot e^{-\lambda(z - \mu)^2}$$

Parameters are estimated via two methods:

**Maximum Likelihood Estimation (MLE)** — optimized using L-BFGS-B:

| Parameter | Value |
|-----------|-------|
| λ (lambda) | 0.000001 |
| μ (mu) | 21.077877 |
| c | 87680.290592 |

**Analytical (Moment Matching)**:

| Parameter | Value |
|-----------|-------|
| λ (lambda) | 0.003419 |
| μ (mu) | 21.484590 |
| c | 0.032988 |

### Step 3 — Goodness of Fit

Kolmogorov-Smirnov test against the fitted distribution:
- **KS Statistic:** 0.4913
- **p-value:** 0.0000

---

## Summary Statistics

| Metric | Original (x) | Transformed (z) |
|--------|-------------|-----------------|
| Count | 27447 | 27447 |
| Mean | 21.47 | 21.48 |
| Std Dev | 12.12 | 12.09 |
| Min | 0.50 | 0.67 |
| Max | 334.90 | 334.82 |
| Median | 19.00 | 18.94 |
| Skewness | 3.22 | 3.25 |
| Kurtosis | 39.16 | 39.47 |

---

## Files

| File | Description |
|------|-------------|
| `Assignment1_102303059 (1).ipynb` | Main Jupyter notebook with all analysis |
| `data.csv` | India Air Quality dataset |

## Dependencies

```
numpy
pandas
matplotlib
seaborn
scipy
```

## Usage

1. Clone the repository
2. Place `data.csv` in the working directory (or update the path in the notebook)
3. Run all cells in `Assignment1_102303059 (1).ipynb`
