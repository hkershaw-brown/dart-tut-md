
---

# DART Tutorial Section 18:  
### Lost in Phase Space: The Challenge of Not Knowing the Truth  

---

### Reality Strikes

In real-world applications, we do not have access to the truth. Instead, we rely solely on observations, which are functions of state variables and are contaminated by observational errors. While having the truth in earlier exercises was convenient, it was also misleading because much less information is typically available from observations.

---

### Understanding Observation-Space Diagnostics

In DART, whether an observation is assimilated or rejected depends on the settings in the `input.nml`, particularly the thresholds in `&quality_control_nml`:

```fortran
&quality_control_nml
input_qc_threshold = 3.0,
outlier_threshold = -1.0,
/
```

Using the **`obs_diag`** tool, you can post-process `obs_seq.final` to calculate metrics such as RMSE, bias, ensemble spread, total spread, and the number of observations used or rejected.

---

### Observation-Space Diagnostics

The `obs_seq` files used in DART are not in a user-friendly format, so the **`obs_diag`** program must be run to convert them into a netCDF file for easier evaluation. The DART Matlab functions can then be used to visualize the results.

Some available Matlab functions include:
- `plot_rank_histogram.m`
- `plot_evolution.m`
- `plot_rmse_xxx_evolution.m`
- `two_experiments_evolution.m`
- `plot_profile.m`
- `plot_bias_xxx_profile.m`
- `plot_rmse_xxx_profile.m`

These functions can work with any `obs_seq.final` file from any experiment and model.

---

### Lorenz 96 Observation Diagnostic Example

When performing diagnostics on the Lorenz 96 model, you can track the evolution of RMSE and total spread over time. By adjusting parameters such as the outlier threshold, you can explore how different settings impact the rejection of observations and the overall assimilation quality.

---

### Exercises with Lorenz 96

- Pick a case that performs well and analyze the observation-space diagnostics.
- Choose a similar case that is physically different and compare it using physical-space diagnostics.
- Use observation-space diagnostics to detect differences.
- Rerun `obs_diag` with different bin widths and assess the impact.

---

### Rank Histograms and Time-Averaged Profiles

DART's diagnostics provide tools to create rank histograms and time-averaged profiles. These visualizations can give insights into how well the model fits the observations over time and how bias and total spread evolve.

For example:
- `plot_rank_histogram.m`: Displays the rank of observations among ensemble members.
- `plot_profile.m`: Shows bias and total spread across different vertical levels.

---

### Using `obs_seq_to_netcdf`

To convert an `obs_seq` file to netCDF format, use the `obs_seq_to_netcdf` program. This allows you to visualize observation diagnostics more easily using Matlab tools like:
- `plot_obs_netcdf.m`
- `plot_obs_netcdf_diffs.m`
- `plot_coverage.m`

---

### Matlab Hands-On: Exploring Observations

Using `link_obs.m`, you can explore the observations interactively. This tool allows you to rotate, select, and inspect specific observations, helping to identify rejected observations and understand the reasons behind their rejection.

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
12. Adaptive Inflation
13. Hierarchical Group Filters and Localization
14. Quality Control
15. DART Experiments: Control and Design
16. Diagnostic Output
17. Creating Observation Sequences
18. **Lost in Phase Space: The Challenge of Not Knowing the Truth**

---

