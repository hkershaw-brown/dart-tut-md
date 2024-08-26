
---

# DART Tutorial Section 13:  
### Hierarchical Group Filters and Localization  

---

### Ways to Deal with Regression Sampling Error

1. **Ignore it**:  
   If there are only a few unrelated observations and there is a way to maintain variance in priors, this can work.
   
2. **Use larger ensembles**:  
   Larger ensemble sizes reduce sampling error, but this can become expensive. Try different ensemble sizes (e.g., 40, 80, 160).

3. **Use additional a priori information**:  
   Ensure that observations only impact state variables that are expected to be related.

4. **Determine and correct for sampling error**:  
   Multiple methods, including using hierarchical Monte Carlo techniques, can help address sampling error.

---

### Localization

- **Localization** refers to weighting the regression based on expected correlation between the observation and state variable. This is useful when distance is a factor, but complex models like satellite radiance and wind component relationships can be harder to localize.
- DART allows for **vertical localization** for more complex models.

---

### Hierarchical Monte Carlo: Ensemble of Ensembles

- Split the ensemble into **M independent groups** of **N members**. For example, 80 ensemble members can be split into 4 groups of 20.
- Compute observation increments for each group, giving **M estimates of the regression coefficient** (β).
- Compute a **regression confidence factor** (α) that minimizes regression error across groups, reducing uncertainty in state variable increments.

```plaintext
M Independent 
N-Member 
Ensembles

β₁   β₂   ...   βₘ
```

---

### Using Hierarchical Monte Carlo in Lorenz 96

1. Set `ens_size = 80` in `&filter_nml` and split into 4 groups of 20.
2. Turn on regression diagnostics.
3. After running the group filter, examine the value of α using the `plot_reg_factor` tool in Matlab. This can provide insights into good localization strategies for a given observation.

---

### Additional Features of Hierarchical Filters

- A more detailed look at group filters can be found in the tutorial directory (`OLD_section_13.pdf`), where pages 10-54 complement the material in this section.

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
13. **Hierarchical Group Filters and Localization**
14. Quality Control
15. DART Experiments: Control and Design

---

