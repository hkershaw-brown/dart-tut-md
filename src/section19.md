
---

# DART Tutorial Section 19:  
### Making DART-Compliant Models  

---

### DART Compliant Models Overview

DART uses identical assimilation code across a variety of models. The same namelists used for low-order models apply to more complex models as well.

To work with DART, models must implement a subset of **18 interfaces**. This can be done by:
1. **Wrapping the model**: Embedding the model itself within the DART filter.
2. **Interfacing the model**: Running the model outside of the filter, while using a `model_mod` to connect it with DART.

---

### Large Models Compliant with DART

DART supports a wide range of models, including:
- **Low-order models** for data assimilation research
- **Geophysical models**: Atmosphere, ocean, land, solar, space weather, hydrology
- **Non-geophysical applications**: Economics, target-tracking

Some examples include:
- **Global Atmosphere Models**: CAM, WACCM, AM2, MPAS
- **Regional Atmosphere Models**: WRF, COSMO, NCOMMAS
- **Ocean Models**: POP, ROMS, MIT OGCM
- **Upper Atmosphere/Space Weather Models**: ROSE, GITM
- **Land/Hydrology Models**: CLM, NOAH, WRF Hydro

---

### Creating a DART-Compliant Model

For full compliance, models must implement the following interfaces:
1. **get_model_size**: Returns the size of the model.
2. **get_state_meta_data**: Provides location and type of each state variable.
3. **static_init_model**: Initializes the model (allocating memory, reading namelist).
4. **get_model_time_step**: Specifies the model's time step.
5. **model_interpolate**: Interpolates a state value at a given location.
6. **adv_1step**: Advances the model by one time step.

Additional interfaces may include:
- **pert_model_state**: Perturbs the control state to generate ensemble members.
- **nc_write_model_atts and nc_write_model_vars**: Write netCDF diagnostic output.
- **get_close_obs**: Performs efficient observation searches.

---

### Steps for Creating a DART-Compliant Model

1. **Start with the DART template**: Copy the `models/template` directory and modify it incrementally.
2. **Decide on model interaction**:
   - Embed the model inside the DART filter (subroutine-callable).
   - Drive the model externally using scripts.
   - For parallel models, use complex scripting to advance the model separately from DART.
3. **Test incrementally**: Implement one interface at a time and use the provided tests to ensure each is working correctly.

---

### Assimilating Observations in Your Model

To assimilate observations, you need to implement the `model_interpolate` subroutine. This involves:
1. **Direct interpolation**: If the observation type exists in the model state.
2. **Vertical transformations**: For observations that require transformations (e.g., temperature, moisture, pressure).
3. **Forward operators**: Implement custom operators in `obs_def_xxx_mod.f90` for observations that cannot be directly interpolated.

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
18. Lost in Phase Space: The Challenge of Not Knowing the Truth
19. **DART-Compliant Models and Making Models Compliant**

---

