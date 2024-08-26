
---

# DART Tutorial Section 16:  
### Diagnostic Output  

---

### DART Diagnostic Output Categories

1. **State-Space**:  
   - Outputs the values of the model’s state vector and inflation in netCDF format.
   
2. **Observation-Space**:  
   - Stores observation values in the DART-specific `obs_sequence` format.
   
3. **Regression Confidence Factor**:  
   - Outputs values for state vector/observation pairs (ASCII format, transitioning to netCDF).
   
4. **Program Diagnostic Output**:  
   - Includes source code version, namelist values, and error/warning messages.

---

### State-Space Diagnostic Files

DART uses the **netCDF** format for state-space diagnostic files, and you can specify the stages of the filter cycle where outputs are written using the `stages_to_write` entry in `&filter_nml`.

The corresponding files are:
- `forecast.nc`: Ensemble forecasts
- `preassim.nc`: Prior inflation applied
- `postassim.nc`: State updates from assimilation
- `analysis.nc`: Posterior inflation applied

Additional options include:
- `input.nc`: Initial conditions
- `output.nc`: Output file for restarting subsequent filter steps

---

### Viewing State-Space netCDF Files

- DART provides several **Matlab diagnostic functions** available in the `diagnostics/matlab` directory:
  - `plot_bins.m`: Rank histograms
  - `plot_correl.m`: Correlation plots
  - `plot_ens_err_spread.m`: RMS error and spread
  - `plot_ens_mean_time_series.m`: Ensemble mean time series
  - `plot_phase_space.m`: 3D phase space time evolution
  - `plot_sawtooth.m`: Time series of truth, prior, and posterior
  - `plot_total_err.m`: Total error for different fields
  - `plot_var_var_correl.m`: Correlation between variables over time

You can change the diagnostic file used by Matlab functions by entering the filename at the prompt or by setting the `diagn_file` variable in Matlab.

---

### Observation-Space Files

Observation files are named as follows (names specified in namelists):
- `obs_seq.in`: Input to `perfect_model_obs`
- `obs_seq.out`: Output from `perfect_model_obs`, input to the filter
- `obs_seq.final`: Output from the filter, containing prior, posterior, and observed values.

Observation-space diagnostics can be generated using tools like `obs_diag`, which converts the `obs_seq` format to netCDF for easy plotting.

---

### Regression Confidence Factor Output

- Introduced in **Section 13**, the regression confidence factor (α) is used in group filters with multiple ensemble groups.
- Output is controlled by `&reg_factor_nml` and is saved in an ASCII format (e.g., `reg_diagnostics`).
- The output includes time, observation index, state index, and the confidence factor α.

---

### Program Diagnostic Output

- All DART executables append their diagnostic output to `dart_log.out`. This file contains:
  - Program start time
  - Version of the code for each module
  - Namelist values
  - Error, warning, and message logs

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
16. **Diagnostic Output**

---

