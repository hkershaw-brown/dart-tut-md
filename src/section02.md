
---

# DART Tutorial: Section 2  
### The DART Directory Tree

---

The National Center for Atmospheric Research is sponsored by the National Science Foundation.  
Any opinions, findings, conclusions, or recommendations expressed in this publication are those of the author(s) and do not necessarily reflect the views of the National Science Foundation.  
© UCAR

---

## The DART Code Tree

Much of DART is implemented as Fortran-90 modules and programs. In addition, DART contains:

- Documentation
- Namelist control files
- Compilation tools
- Shell scripts for managing large applications
- Diagnostic tools

---

## DART Top-Level Directory Structure

```plaintext
DART/
    ├── models/
    ├── observations/
    ├── assimilation_code/
    ├── documentation/
    ├── diagnostics/
    ├── build_templates/
    ├── CHANGELOG/
    └── README/
```

Explore the DART subdirectories to get familiar with the structure.

---

## DART Models Directory

```plaintext
DART/models/
            ├── lorenz_63/
            ├── lorenz_96/
            ├── wrf/
            ├── POP/
            ├── cam-fv/
            ├── utilities/
            └── model_mod_tools/
```

- The **`models`** directory contains various models like Lorenz 63, Lorenz 96, WRF, etc. It also includes utility directories and a code template for adding new models.

---

### Example: DART Model Directory

```plaintext
lorenz_96/
        ├── work/
        ├── matlab/
        ├── tests/
        └── shell_scripts/
```

- The `work` directory is where executables are built and run.
- `matlab/`, `tests/`, and `shell_scripts/` directories are model-specific, but they are not required for every model.

---

### DART Model/Work Directory Details

- **`work/`**: Where executables are built, and input/output files reside.
- **Makefiles and compiler output files**: Found in the `work` directory.
- **Input/Output files**: Including the `input.nml` file used by all DART programs.
- **Scripts**:
  - `workshop_setup.sh`: Used for running set experiments in workshops.
  - `quickbuild.sh`: Used to compile all applicable DART programs for the model. You can run `./quickbuild.sh help` to learn more.

---

## DART Module Files

For instance, the directory `assimilation_code/modules/assimilation/` contains the following three files that implement localization:

- `cov_cutoff_mod.f90`: Code for the module
- `cov_cutoff_mod.html`: Documentation for the module
- `cov_cutoff_mod.nml`: Run-time control for the module

DART Fortran-90 code comes with code, documentation, and run-time control files.

---

## DART Observations Directory

```plaintext
DART/observations/
                ├── utilities/
                ├── forward_operators/
                └── obs_converters/
```

- **Utilities**: Tools for manipulating observation sequence files.
- **Forward Operators**: Code for computing forward operators for various instruments and models.
- **Obs Converters**: Programs for creating observation sequence files from various data sources.

---

## DART Documentation Directory

```plaintext
DART/documentation/
                  ├── DART_LAB/
                  ├── tutorial/
                  └── html/
```

- **`DART_LAB/`**: Interactive Matlab introduction to ensemble assimilation.
- **`tutorial/`**: The current tutorial.
- **`html/`**: Header for HTML documentation.

---

## DART Assimilation Code Directory

```plaintext
DART/assimilation_code/
                      ├── programs/
                      ├── scripts/
                      └── modules/
```

- **`programs/`**: Contains all DART programs, including the filter for ensemble assimilation.
- **`scripts/`**: Scripts for specialized tasks.
- **`modules/`**: Defines geometries for assimilation (e.g., `threed_sphere/` for large problems, `oned/` for simple models).

---

## DART Assimilation Code/Modules Directory

```plaintext
assimilation_code/modules/
                          ├── assimilation/
                          ├── io/
                          ├── utilities/
                          └── observations/
```

- **`assimilation/`**: Contains modules for ensemble solver algorithms, like `filter_mod.f90`.
- **`io/`**: Modules for input/output operations in DART filters.
- **`utilities/`**: Manages data structures, parallel processing, time, and calendars.

---

### DART Tutorial Index to Sections

1. Filtering For a One Variable System
2. The DART Directory Tree
3. DART Runtime Control and Documentation
4. How Observations of a State Variable Impact an Unobserved State Variable
5. Comprehensive Filtering Theory: Non-Identity Observations and the Joint Phase Space
6. Other Updates for An Observed Variable
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
18. Lost in Phase Space: The Challenge of Not Knowing the Truth
19. DART-Compliant Models and Making Models Compliant
20. Model Parameter Estimation
21. Observation Types and Observing System Design
22. Parallel Algorithm Implementation
23. Location Module Design (Not Available)
24. Fixed Lag Smoother (Not Available)
25. A Simple 1D Advection Model: Tracer Data Assimilation

---

