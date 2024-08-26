
---

# DART Tutorial Section 8:  
### Dealing with Sampling Error  

---

### Updating Additional Prior State Variables

Two primary sources of error:

1. **Sampling error due to noise**:  
   - Even with a linear relationship between variables, sample regression coefficients can be imprecise with finite ensembles.
  
2. **Linear approximation invalid**:  
   - Nonlinearity in the true relationship between variables may require special handling, especially over a large range of prior ensemble.

---

### Regression Sampling Error & Filter Divergence

- **Scenario**: The unobserved state variable is known to be unrelated to the observed variables.
- **Problem**: Even with finite samples, non-zero correlations are observed, leading to incorrect adjustments of the unobserved variable.
  - The unobserved variable mean may follow a random walk as more observations are used.
  - The standard deviation (SD) of the unobserved variable tends to decrease, which leads to overconfidence in the estimates.
  
---

### Filter Divergence

- **Issue**: Overconfidence in unobserved variables results in ignoring meaningful observations.
- **Example**: In the Lorenz 96 experiment, filter spread became small, giving the filter the illusion of a good estimate. However, the error remained large because good observations were ignored.

---

### Dealing with Regression Sampling Error

#### Strategies:
1. **Ignore it**:  
   - If the number of unrelated observations is small and variance is maintained in priors (e.g., in 3 and 9 variable models).

2. **Use larger ensembles**:  
   - Increasing ensemble size reduces sampling error but can become expensive for large problems.
   - Try different ensemble sizes by modifying `ens_size` in `&filter_nml` (e.g., 40, 80, 160).

3. **Use a priori information**:  
   - Incorporate knowledge about the relationships between observations and state variables (e.g., use localization).

4. **Correct for sampling error**:  
   - DART provides several methods to estimate and correct for sampling error.

---

### Localization in DART

- **Localization** refers to weighting regression based on the distance between observations and state variables.
  - DART provides different shapes for the localization function, controlled by `select_localization` in `&cov_cutoff_nml`.
  - The **half-width** of the localization function is set by `cutoff` in `&assim_tools_nml`.

#### Localization Options:
- 1: Gaspari-Cohn
- 2: Boxcar
- 3: Ramped Boxcar

---

### Experimenting with Lorenz 96

- Test different localization half-widths for the Lorenz 96 model using a 40-member ensemble.
  ```bash
  cd models/lorenz_96/work
  ./workshop_setup.sh
  ```
- **Exercise**: Explore different localization settings and assess their impact on the results.

---

### Spread Restoration

- DART implements a **spread restoration** algorithm:
  - After computing increments from an observation, if no correlation is expected, compute the expected decrease in spread and add it back.
  - Enable this algorithm by setting `spread_restoration = .true.` in `&assim_tools_nml`.

---

### Sampling Error Correction

- DART also provides a **sampling error correction** algorithm, which reduces but doesn’t entirely eliminate issues. It often improves results for large models.
  - Enable this algorithm by setting `sampling_error_correction = .true.` in `&assim_tools_nml`.

---

### DART Tutorial Index

1. Filtering for a One Variable System
2. The DART Directory Tree
3. DART Runtime Control and Documentation
4. How Observations Impact Unobserved State Variables
5. Comprehensive Filtering Theory
6. Other Updates for an Observed Variable
7. Some Additional Low-Order Models
8. **Dealing with Sampling Error**
9. Dealing with Error and Inflation
10. Regression and Nonlinear Effects
11. Creating DART Executables
12. Adaptive Inflation
13. Hierarchical Group Filters and Localization
14. Quality Control
15. DART Experiments: Control and Design
16. Diagnostic Output
17. Creating Observation Sequences

---

