
---

# DART Tutorial Section 23:  
### Location Module Design  

---

### DART Location Modules

The location of model states and observations in DART is specified by selecting one of the available location modules. These modules define how location coordinates are handled for different types of models. Some commonly used location modules include:

| Module Name       | Location Specification                                               |
|-------------------|----------------------------------------------------------------------|
| **threed_sphere**  | lat, lon, vertical (e.g., surface, height, pressure, level, none)    |
| **oned**           | x (periodic)                                                        |
| **annulus**        | azimuth, radius, vertical (e.g., surface, level, height)            |
| **channel**        | x (periodic), y (limited domain), z (infinite)                      |
| **column**         | vertical (e.g., surface, level, pressure, height, none)             |
| **twod**           | x, y (both periodic)                                                |
| **twod_annulus**   | azimuth, radius (with azimuth boundary options)                     |
| **twod_sphere**    | lat, lon                                                            |
| **threed**         | x, y, z (all periodic)                                              |
| **threed_cartesian**| x, y, z (Cartesian coordinates)                                    |

(Note: Modules marked with * are the most commonly used.)

---

### Location Module Design

In DART, the **Location Derived Type** is used to handle different location modules without exposing the internal values of these modules. This design allows the main DART routines to pass locations through the system, regardless of the internal structure of the module.

All location modules share a standard set of routine interfaces, enabling them to be compiled and used interchangeably within DART.

---

### Required Interfaces for Location Modules

Each location module must implement a set of required interfaces to ensure compatibility with DART. These interfaces include:

- **public location functions**:
  - `location_type`, `get_location`, `set_location`, `set_location_missing`
  - `is_location_in_region`, `query_location`
  - `write_location`, `read_location`, `interactive_location`
  - Comparison operators: `operator(==)`, `operator(/=)`
  
- **localization and distance-related functions**:
  - `get_close_type`, `get_close_init`, `get_close_obs`
  - `get_close_state`, `get_close_destroy`, `get_dist`
  
- **vertical location-related functions**:
  - `has_vertical_choice`, `vertical_localization_on`
  - `set_vertical`, `is_vertical`, `convert_vertical_obs`, `convert_vertical_state`
  - `get_vertical_localization_coord`, `set_vertical_localization_coord`

Note: Even if a model (e.g., a low-order model) does not use vertical coordinates, the module must still include these entry points as dummy routines.

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
19. DART-Compliant Models and Making Models Compliant
20. Model Parameter Estimation
21. Observation Types and Observing System Design
22. Parallel Algorithm Implementation
23. **Location Module Design**
24. Fixed Lag Smoother (not available)
25. A Simple 1D Advection Model: Tracer Data Assimilation

---

