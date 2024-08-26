
---

# DART Tutorial Section 17:  
### Creating Observation Sequences  

---

### Types of Observations Used in DART

DART supports a wide range of geophysical observations, including:

- Atmospheric observations
- Ocean observations
- Solar, space weather, extraterrestrial observations
- Land observations
- Sea ice observations

---

### Building Real Observation Sequences

In the DART distribution, `observations/obs_converters` contains various programs to convert data into DART `obs_seq` format. These converters are available for several file formats:

- **netCDF**: Start with `MADIS/convert_madis_profiler.f90`
- **Comma-separated text**: Start with `Ameriflux`
- **Generic text**: Start with `text`
- **HDF-EOS**: Start with `AIRS`
- **BUFR or prepBUFR**: Start with `NCEP`
- **Dense data (satellite swaths)**: Start with `quikscat`
- **Ray-path integrated data**: Start with `gps`
- **World Ocean Database packed ASCII**: Start with `WOD`

To create new converters for custom data formats, use the above files as starting points.

---

### Observation Sequence Tools

Several tools are provided for managing and processing observation sequences:

- **`obs_diag`**: Primary tool for evaluating observation space performance.
- **`obs_seq_to_netcdf`**: Converts an `obs_seq` file to netCDF format.
- **`obs_sequence_tool`**: A general-purpose tool for handling observation sequences.
- **`obs_common_subset`**: Selects common observations from multiple files.
- **`obs_seq_coverage`**: Identifies observation locations through time.
- **`obs_seq_verify`**: Generates a netCDF file for verification studies.
- **`obs_selection`**: Selects a subset of observations from another `obs_seq` file.
- **`obs_loop`**: A template to help create custom `obs_seq` modifying programs.

---

### Structure of an Observation Sequence File

Observation sequence files contain multiple data values per observation and can store metadata for each observation type (e.g., radar, GPS). The file does not need to be time-ordered; DART automatically reads observations in time sequence during assimilation.

For more details, refer to the [DART documentation on observation sequences](https://docs.dart.ucar.edu/en/latest/guide/detailed-structure-obs-seq.html).

---

### Building Real Observation Sequences

1. **Interactive creation**:  
   Use the `create_obs_sequence` program to input observation details interactively.
   
2. **Use a converter**:  
   Use an existing converter for your data format.
   
3. **Custom program**:  
   Write a custom program using the `obs_sequence` module in Fortran 90 to create, read, and modify observation sequences.

---

### Creating Synthetic Observation Sequences

Synthetic observation sequences are used in Observing System Simulation Experiments (OSSEs).

**Steps**:
1. **Create the sequence**:  
   Use `create_obs_sequence` or `create_fixed_network_seq` to generate the observation network.
   
2. **Generate observations**:  
   Run `perfect_model_obs` to simulate observations based on the model.
   
3. **Run the filter**:  
   The filter will add ensemble mean, spread, and individual ensemble member values to the observation sequence.

---

### Example: Localized Observation Set for Lorenz 96

1. Run `create_obs_sequence` and specify 5 observations (group them close to location 0.5).
2. Use `create_fixed_network_seq` to observe these 5 observations repeatedly over 1000 hours.
3. Generate synthetic observations using `perfect_model_obs`.
4. Run the filter with adaptive inflation and analyze results using Matlab diagnostics.

---

### Selecting Observation Types to Process

To specify which types of observations to assimilate or evaluate (but not assimilate), use the `&obs_kind_nml` in the namelist:

```fortran
&obs_kind_nml
  assimilate_these_obs_types = 'RAW_STATE_VARIABLE'
  evaluate_these_obs_types   = 'RAW_STATE_1D_INTEGRAL'
/
```

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
17. **Creating Observation Sequences**

---

