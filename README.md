# Hybrid PINN–Grover Framework for Dark Matter Halo Parameter Inference

## Overview

This project implements a hybrid **Physics-Informed Neural Network (PINN)** and **Grover quantum search** framework to infer **dark matter halo parameters** from galaxy rotation curves.

The goal is to estimate halo parameters by fitting observed rotation curves using the **Navarro–Frenk–White (NFW) model**, while demonstrating the potential advantage of quantum search over classical methods.

---

## Problem Statement

Galaxy rotation curves cannot be explained by visible matter alone, indicating the presence of dark matter halos.

Given observed data:
- Radius: `r`
- Velocity: `v_obs`

We aim to estimate halo parameters:
- `r_s` (scale radius)
- `rho_s` (scale density)

by minimizing:

MSE(v_obs, v_model)

---

## Methodology

The project consists of two main branches:

### 1. Classical Baselines
- Grid Search
- Gradient Descent (Adam)

### 2. Proposed Hybrid Approach
- PINN surrogate model
- Quantum oracle construction
- Grover search

---

## Physics Model (NFW Halo)

Density profile:

rho(r) = rho_s / ((r/rs) * (1 + r/rs)^2)

Velocity model:

v_model(r) = sqrt(G * M(r) / r)

Where:
- `M(r)` is obtained by integrating the density profile
- `G` is the gravitational constant

---

## Dataset

- Galaxy rotation curve data from the **SPARC database**
- 3–5 galaxies used for experiments

---

## Project Pipeline

### Step 1: Data Loading
- Load rotation curve data (r, v_obs)
- Normalize and preprocess

### Step 2: Physics Simulation
- Compute v_model using NFW equations
- Generate synthetic training data

---

## Branch 1 — Classical Methods

### Grid Search
- Discretize parameter space (e.g., 64 × 64 grid)
- Evaluate all candidates
- Select parameters minimizing MSE

### Gradient Descent
- Initialize parameters
- Optimize using Adam optimizer
- Iteratively minimize MSE

---

## Branch 2 — PINN + Grover

### Step 1: PINN Surrogate

Train a neural network to approximate:

(r, rs, rho_s) → v(r)

Loss function:

Loss = DataLoss + PhysicsLoss

Output:
- Fast surrogate model `v_pred`

Purpose:
- Replace expensive physics computation

---

### Step 2: Oracle Construction

For each candidate (rs, rho_s):

1. Predict velocity using PINN
2. Compute error:

   error = MSE(v_obs, v_pred)

3. Mark candidate if error < threshold

This defines the **quantum oracle**.

---

### Step 3: Grover Search

- Define search space of size N
- Run ~ (π/4)√N iterations
- Amplify probability of correct parameters
- Measure to obtain best candidate

Output:
- Estimated parameters (rs, rho_s)

---

## Evaluation

### Metrics

- Parameter accuracy:
  |rs_true - rs_est|, |rho_s_true - rho_s_est|

- Rotation curve fit:
  MSE(v_obs, v_model)

- Search efficiency:
  Number of oracle calls

---

## Scaling Experiment

Test for different search sizes:

- N = 256
- N = 1024
- N = 4096

Compare:

| Method          | Complexity |
|-----------------|-----------|
| Grid Search     | O(N)      |
| Grover Search   | O(√N)     |
| Gradient Descent| Iterative |

Plot:
- Oracle calls vs search space size

---

## Repository Structure

Since this project is implemented in a single Google Colab notebook:
- DMHalo.ipynb
- README.md


Notebook sections:

1. Data Loading
2. Physics Model (NFW)
3. Classical Baselines
4. PINN Training
5. Oracle Construction
6. Grover Search
7. Evaluation & Plots

---

## Technologies Used

- Python
- PyTorch (PINN implementation)
- Qiskit (quantum circuits & Grover search)
- NumPy / SciPy
- Matplotlib
- Google Colab

---

## Key Contributions

- Hybrid quantum-classical framework for parameter inference
- Use of PINN as a surrogate model for quantum oracle
- Demonstration of Grover search scaling in a physics problem
- Comparison with classical optimization methods

---

## Future Work

- Extend to more complex halo models
- Improve PINN accuracy and generalization
- Explore variational quantum algorithms
- Apply to larger astrophysical datasets

---

## References

- Navarro, Frenk, White (1996) — NFW Halo Model

- SPARC Database — Galaxy Rotation Curves

- Raissi et al. (2019) — Physics-Informed Neural Networks

- Grover (1996) — Quantum Search Algorithm

## Author
Rajrupa Das
