
---

# DART Tutorial Section 3:  
### DART Runtime Control and Documentation  

---

### DART Philosophy: Configurable at Run-time
- Uses F90 namelist facility to configure.
- Each F90 module has its own associated namelist file.
- All namelists are combined in a single file (`input.nml`) in the working directory.
- Documentation of modules, including namelists, is available in HTML files.

Example modules:
- **`cov_cutoff_mod`**  
  - Code: `cov_cutoff_mod.f90`
  - Documentation: `cov_cutoff_mod.html`
  - Runtime control: `cov_cutoff_mod.nml`

---

### Example: Changing to a Multivariate Filter

- **Model:** `models/lorenz_63/work/`
- Section 1: Lorenz 63 Example
  - Observed x, y, z components.
  - Observation of x only impacted the ensemble for x, etc.

To switch to a multivariate filter:
- **Modification**: Observations of x will impact ensembles for x, y, and z.
- **Change namelist setting** in `models/lorenz_63/work/input.nml`
  - Modify `&assim_tools_nml`
  - Parameter: `cutoff`

---

### Examining the Assimilation Module

- Open `assimilation_code/modules/assimilation/assim_tools_mod.html` in a browser.
  - Overview
  - List of modules used
  - Public interface (for use in other modules)
  - Details of interfaces and variables
  - **Namelist**: Lists runtime control variables for `assim_tools`

For example:
- **`cutoff`** controls the distance to which an observation has an impact.
  - Small value: Observation of x impacts only x.
  - Large value: All observations impact all state variables.

---

### Example Configuration in `input.nml`
- The `input.nml.xxxxxx_default` files for each program are automatically created by the compilation tool (see Section 11).
- Convenient to have one `input.nml` file containing all settings for commonly-used programs.

Editing `models/lorenz_63/work/input.nml`:
- Modify the `&assim_tools_nml` namelist parameter `cutoff`.  
- When the program filter is run again, the modification is incorporated.

Example `&assim_tools_nml` settings:
```fortran
&assim_tools_nml
filter_kind                     = 1,
cutoff                          = 0.00001,
sort_obs_inc                    = .false.,
spread_restoration              = .false.,
sampling_error_correction       = .false.,
adaptive_localization_threshold = -1,
distribute_mean                 = .false.,
output_localization_diagnostics = .false.,
localization_diagnostics_file   = 'localization_diagnostics',
print_every_nth_obs             = 0
/
```

---

### Tutorial Index
1. Filtering for a One Variable System
2. The DART Directory Tree
3. DART Runtime Control and Documentation
4. Multivariate Assimilation: How should observations of a state variable impact an unobserved state variable?
5. Comprehensive Filtering Theory
6. Other Updates for Observed Variables
7. Additional Low-Order Models
8. Dealing with Sampling Error
9. More on Error Handling and Inflation
10. Regression and Nonlinear Effects
11. Creating DART Executables
12. Adaptive Inflation
13. Hierarchical Group Filters and Localization
14. Quality Control
15. DART Experiments: Control and Design
16. Diagnostic Output
17. Creating Observation Sequences
18. Lost in Phase Space: The Challenge of Not Knowing the Truth
19. DART-Compliant Models and Compliance Guidelines
20. Model Parameter Estimation
21. Observation Types and System Design
22. Parallel Algorithm Implementation
23. Location Module Design (not available)
24. Fixed Lag Smoother (not available)
25. A Simple 1D Advection Model: Tracer Data Assimilation

---

