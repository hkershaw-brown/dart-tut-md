Here is the Markdown conversion of Section 9 from the DART tutorial:

---

# DART Tutorial Section 9:  
### More on Dealing with Error: Inflation  

---

### Some Error Sources in Ensemble Filters

1. **Model Error**  
2. **Observation Errors** (Representativeness)  
3. **Gross Observation Error**  
4. **Sampling Error** (Gaussian Assumption)  
5. **Sampling Error** (Assuming Linear Statistical Relation)

---

### Dealing with Ensemble Filter Errors

Errors can be addressed as follows:

1. **Variance inflation**: Increase prior uncertainty to give observations more impact.
2. **Localization**: Restrict observation impact to a set of nearby state variables and smoothly decrease this impact with distance.

---

### Model/Filter Error: Filter Divergence and Variance Inflation

- **Problem**: Prior distribution has insufficient variance due to sampling or model errors, leading to **filter divergence**.  
  - The filter becomes overconfident, ignoring valuable observations.
  
- **Naïve solution**: Variance inflation to increase spread of the prior.
  - Inflate by applying:  
    \[
    x_i \leftarrow \lambda \cdot (x_i - \bar{x}) + \bar{x}
    \]
  
---

### Physical Space Variance Inflation

- Inflate all state variables by the same amount before assimilation.
- **Capabilities**:  
  - Effective for a variety of models.
  - Can maintain linear balances and stay on flat manifolds.
  - Simple and cost-effective.
  
- **Liabilities**:  
  - Unobserved regions can ‘blow up’ (e.g., in AGCMs).  
  - Magnitude of inflation (λ) is often selected by trial and error.

---

### Physical Space Variance Inflation Example: Lorenz 63

- **Before Inflation**:  
  Observation lies outside the prior, risking filter divergence.
  
- **After Inflation**:  
  The prior ensemble is inflated, and the observation falls within the ensemble cloud, preventing filter divergence.

However, **inflated priors** may lead to transient off-attractor behavior or model blow-up if not handled properly.

---

### Controlling Inflation in DART

In DART, inflation is controlled using parameters in `&filter_nml`:

```fortran
inf_flavor = 0,           0,
inf_initial_from_restart   = .false.,    .false.,
inf_initial                = 1.0,        1.0,
inf_damping                = 1.0,        1.0,
inf_lower_bound            = 1.0,        1.0,
inf_upper_bound            = 1000000.0,  1000000.0,
```

- `inf_flavor`:  
  - 0 = No inflation  
  - 2,3 = Physical space inflation
  
- Set `inf_initial` to values like 1.05, 1.08, or 1.10 for experimentation.

---

### Variance Inflation in Observation Space

- **Concept**: Adjust the variance of the prior based on its consistency with the observation likelihood.
- **Not currently supported** in the Manhattan version of DART.

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
9. **More on Dealing with Error: Inflation**
10. Regression and Nonlinear Effects
11. Creating DART Executables
12. Adaptive Inflation

---

This section provides methods for handling filter divergence and error using variance inflation, particularly in physical space. Let me know if you'd like further refinements or explanations!
