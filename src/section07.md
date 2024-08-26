
---

# DART Tutorial Section 7:  
### Some Additional Low-Order Models  

---

### Low Order Models in DART

| Model              | Size             | Features                                                   |
|--------------------|------------------|-------------------------------------------------------------|
| **lorenz_63**       | 3                | Chaotic, nearly integral attractor, bifurcations            |
| **lorenz_84**       | 3                | More complex attractor, less periodic                       |
| **9var**            | 9                | Transient off-attractor dynamics                            |
| **lorenz_96**       | 40 (variable)    | Higher dimensional system; attractor dimension 13           |
| **forced_lorenz_96**| 80 (variable)    | Allows assimilation of model parameters (see Section 20)    |
| **lorenz_96_2scale**| 396 (variable)   | Two interacting spatial/temporal scales                     |
| **lorenz_04**       | Variable         | Multiscale dynamics                                         |

---

### Lorenz 84 Model

- The attractor is not sheet-like, and there are rare significant deviations.
- Trajectories along deviations don’t mesh back with the rest of the attractor, posing a challenge for certain filter variants.

```bash
cd models/lorenz_84/work
./workshop_setup.sh
```

- State variables are observed once every hour with observational error variance of 1.
- **Exercise**: Examine the output in Matlab and identify the new type of filter challenge.

---

### 9 Variable Model

- Variables are divided into three groups:
  - Variables 1-3: Divergence
  - Variables 4-6: Vorticity
  - Variables 7-9: Height

- Mimics ‘gravity waves’ when perturbed off the attractor, with transient, high-frequency oscillations dominating divergence variables.
  
```bash
cd models/9var/work
./workshop_setup.sh
```

- Observations of Y1, Y2, Y3 (vorticity variables) every 6 hours with observational error variance of 0.4.

---

### Lorenz 96 (40-variable) Model

- This model has an attractor dimension of 13 with 40 variables and standard forcing of 8.0 in `&model_nml`.
- Issues with sample covariance and small ensemble size can lead to divergence.
  
```bash
cd models/lorenz_96/work
./workshop_setup.sh
```

- Observations are randomly located in space and made once an hour with an observational error variance of 1.0.
- **Exercise**: Use Matlab to examine the output and explore techniques to address the issues identified.

---

### DART Tutorial Index
1. Filtering For a One Variable System
2. The DART Directory Tree
3. DART Runtime Control and Documentation
4. How Observations Impact Unobserved State Variables
5. Comprehensive Filtering Theory
6. Other Updates for an Observed Variable
7. **Some Additional Low-Order Models**
8. Dealing with Sampling Error
9. Dealing with Error and Inflation
10. Regression and Nonlinear Effects
11. Creating DART Executables
12. Adaptive Inflation
13. Hierarchical Group Filters and Localization
14. Quality Control
15. DART Experiments: Control and Design
16. Diagnostic Output
17. Creating Observation Sequences
18. Lost in Phase Space
19. DART-Compliant Models
20. Model Parameter Estimation
21. Observation Types and Design
22. Parallel Algorithm Implementation

---

