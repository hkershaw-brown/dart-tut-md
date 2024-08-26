
---

# DART Tutorial Section 20:  
### Model Parameter Estimation  

---

### Introduction to Model Parameter Estimation

Suppose a model is governed by a stochastic difference equation:

$$
dxt = f(xt, t; u) + G(xt, t; w) d\beta t, \quad t \geq 0
$$

Where:
- \( u \) and \( w \) are vectors of parameters.
- We may not know the parameter values accurately.

We can use observations along with data assimilation to help constrain these parameter values. By augmenting the state vector to include \( xt \), \( u \), and \( w \), the model is modified so that assimilation can adjust these parameters.

---

### Parameter Estimation in an Ensemble Filter

In the ensemble filter approach:
- Add the parameters of interest to the model state vector.
- Proceed to assimilate as usual.

**Challenges**:
1. Localization: Where are the parameters located?
2. No time evolution for parameters (unless added), which may lead to filter divergence.
3. Parameters may not correlate strongly with any observations.

---

### Example: Forced Lorenz 96 Model

The forced Lorenz 96 model is provided in DART, where each state variable has a corresponding forcing variable, \( F_i \):

$$
\frac{dX_i}{dt} = (X_{i+1} - X_{i-2}) X_{i-1} - X_i + F_i
$$

$$
\frac{dF_i}{dt} = N(0, \sigma_{\text{noise}})
$$

In this case, we ask whether observations of state variables can help constrain \( F \), the forcing parameter.

---

### Control via Namelist Parameters

In the `forced_lorenz_96` model, you can adjust the parameters using the following namelist:

```fortran
&model_nml
num_state_vars = 40,
forcing = 8.0,
delta_t = 0.05,
time_step_days = 0,
time_step_seconds = 3600,
reset_forcing = .false.,
random_forcing_amplitude = 0.10,
/
```

- If `reset_forcing = .true.`, \( F_i \) will be set to the global forcing value for all \( i \) and \( t \).
- Adding random noise helps prevent filter divergence.

---

### Assimilation in the Forced Lorenz 96 Model

To run the forced Lorenz 96 model:
1. Navigate to the `models/forced_lorenz_96/work` directory.
2. Run the `workshop_setup.sh` script to prepare the experiment.
3. Use Matlab to analyze the output.

In the perfect model run, forcing was fixed at \\( F = 8.0 \\), but during assimilation, \\( F_i \\) is modified based on observations. Interestingly, the best state estimates often occur when \\( F_i \\) varies, even outperforming cases where \\( F_i \\) is fixed at the known value of 8.0.

---

### Contest: Estimating the Forcing Value

Question: Given an observation set, can you estimate the value of \\( F \\)?

- Try different setups in `input.nml` and analyze the output.
- The truth is unknown, so results will vary based on the chosen parameters and settings.

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
20. **Model Parameter Estimation**

---

