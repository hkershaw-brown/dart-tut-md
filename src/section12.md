
---

# DART Tutorial Section 12:  
### Adaptive Inflation  

---

### Variance Inflation for Observations: An Adaptive Error Tolerant Filter

1. Estimate the prior-observation inconsistency.
2. Compute the expected difference between prior mean and observation.
3. Apply inflation to increase consistency between prior and observation.

---

### Adaptive Error Correction Using Bayesian Statistics

- **Objective**: Estimate the inflation factor (λ) using Bayesian statistics.
- **Steps**:
  1. Assume the prior is Gaussian.
  2. Compute the likelihood of observation given a specific inflation factor.
  3. Update the inflation factor distribution by multiplying the likelihood and prior distribution.
  
Example:
- Start with a prior distribution for λ.
- After each observation, update the distribution using Bayesian statistics.
  
---

### Observing Inflation in Lorenz 96

- **Experiment**: Use the Lorenz 96 model with different inflation factors to study how inflation affects assimilation results.
- **Steps**:
  - Set `inf_flavor = 3` for spatially constant inflation in `&filter_nml`.
  - Run the filter and examine the time series of inflation mean and standard deviation in the `preassim.nc` file.
  - Final inflation values are stored in `filter_output.nc` for use in future runs.

---

### Adaptive Inflation Algorithmic Variants

1. **Random Gaussian Noise**:  
   Add random noise to prior state variables to increase variance.
   - Set `inf_deterministic = .false.` for this variant.
   
2. **Fixed State Space Inflation**:  
   Use a constant inflation factor across space and time.
   - Set `inf_initial` to a fixed value (e.g., 1.05).

3. **Fixed Standard Deviation for Inflation**:  
   Fix the standard deviation of the inflation factor.
   - This helps prevent inflation from getting too small and can be useful for large models.
   - Set `inf_sd_initial` and `inf_sd_lower_bound` to fixed values (e.g., 0.20).

4. **Inflation Damping**:  
   Dampen the inflation factor towards 1.0 with each assimilation cycle.
   - Set `inf_damping` (e.g., 0.9 for 90% damping).

---

### Simulating Model Error in Lorenz 96

- **Objective**: Simulate model error by changing the forcing in the Lorenz 96 model.
- **Setup**:
  - Use synthetic observations from a model with forcing = 8.0.
  - Introduce model error by using different forcing values (e.g., 7, 6, 5, 3) with and without adaptive inflation.

---

### Posterior Inflation

- DART also supports **posterior inflation**, which inflates the state after assimilation but before model advance.
- **Use case**: Helps to increase forecast variance.

---

### DART Tutorial Index

1. Filtering for a One Variable System
2. The DART Directory Tree
3. DART Runtime Control and Documentation
4. How Observations Impact Unobserved State Variables
5. Comprehensive Filtering Theory
6. Other Updates for an Observed Variable
7. Some Additional Low-Order Models
8. Dealing with Sampling Error
9. More on Dealing with Error: Inflation
10. Regression and Nonlinear Effects
11. Creating DART Executables
12. **Adaptive Inflation**
13. Hierarchical Group Filters and Localization

---

