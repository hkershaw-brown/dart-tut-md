
---

# DART Tutorial Section 25:  
### A Simple 1D Advection Model: Tracer Data Assimilation  

---

### 1D Simple Advection Model: Overview

1. One-dimensional periodic domain.
2. Chaotic/stochastic model for wind.
3. A single passive tracer is advected by the wind.
4. A stochastic model for tracer source can be added.
5. A diurnal cycle for the tracer source can be added.
6. A model for phase offset of the diurnal cycle can also be added.

This model can be found in `models/simple_advection` and configured in the `work` directory.

---

### 1D Simple Advection Model Details

- **Domain**: One-dimensional periodic grid on the domain \([0, 1]\).
- **Grid**: Equally spaced grid points, controlled by `num_grid_points` in the namelist.
- **Time-stepping**: Controlled by `time_step_days` and `time_step_seconds`.

---

### The Wind Model: Burger’s Equation

The wind equation is given by:

$$
\frac{\partial u}{\partial t} = -u \frac{\partial u}{\partial x}
$$

- The continuous solution can form shocks when \( u \) varies with \( x \).
- **Upstream Lagrangian differencing** is used to avoid forming shocks.
- Heavy damping ensures that the model generally avoids shocks.

---

### Wind Model Namelist Controls

1. Random perturbations are applied to the wind field at every timestep:  
   $$
   u_i = u_i + \text{Normal}(0, W \Delta t)
   $$
   - **`wind_random_amp`** controls the magnitude of random perturbations.
   
2. The mean wind field is damped to a spatial mean \( M \):  
   $$
   u(t + \Delta t) = u(t) - WD \Delta t \left(u(t) - M\right)
   $$
   - **`wind_damping_rate`** and **`mean_wind`** control the damping and mean wind values.

---

### Tracer Field and Namelist Controls

- A single passive tracer is advected by the wind.
- The tracer concentration \\( C_i \\) at each grid point evolves with time:
  $$
  C_i = C_i + S_i \Delta t - D \Delta t C_i
  $$
  - \\( S_i \\): Tracer source/sink rate.
  - \\( D \\): Tracer destruction rate, controlled by **`destruction_rate`**.

---

### Example Assimilation Experiment

1. **Observations**:
   - 10 equally spaced observations of wind \\( u \\) and tracer concentration \\( C \\).
   - Located between grid points (e.g., 0.05, 0.15, ..., 0.95).
   - Observation errors: \\( \text{var}(u) = 16.01 \), \( \text{var}(C) = 1000.2 \\).
   
2. **Experiment**:
   - Run `./perfect_model_obs` followed by `./filter`.
   - Analyze behavior using Matlab and track errors in concentration and wind fields.

---

### Experiment Variations

1. Modify the types of observations being assimilated by changing the namelist settings in `&obs_kind_nml`:
   - For example, only assimilate wind observations or only tracer concentration observations.

2. Explore the impact of using fewer observations or no observations, and understand the results.

---

### Tracer Source Model

- The tracer source can evolve as a damped random walk at each grid point:
  $$
  S_i = S_i + \text{Normal}(0, SR) - SD (S_i - \bar{S_i})
  $$
  - **`source_random_amp_frac`** controls the random noise amplitude.
  - **`source_damping_rate`** controls the damping rate.

---

### Diurnal Component for Tracer Source

- The diurnal cycle can be added using the **`source_diurnal_rel_amp`** parameter.
- The amplitude of the diurnal component is set as a fraction of the source value.

---

### Problems to Explore

1. **Observation Costs**:  
   Design an optimal observing/assimilation system with a limited budget for observations. Try different configurations to minimize total error for tracer concentration or source estimation.
   
2. **Sparse Observations**:  
   Investigate the effects of reducing the number of observations or changing observation frequency.

3. **Tracer Creation and Destruction**:  
   Analyze if the assimilation process creates or destroys tracer, and try to minimize this effect.

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
23. Location Module Design
24. Fixed Lag Smoother (not available)
25. **A Simple 1D Advection Model: Tracer Data Assimilation**

---

