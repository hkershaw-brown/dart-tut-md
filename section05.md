
---

# DART Tutorial Section 5:  
### Comprehensive Filtering Theory: Non-Identity Observations and the Joint Phase Space  

---

### Dynamical System Overview
- The system is governed by a stochastic difference equation:  
  \( dxt = f(xt, t) + G(xt, t)d\beta t, \, t \geq 0 \)

- Observations are made at discrete times:  
  \( yk = h(xk, tk) + vk; \, k = 1,2,...; \, tk+1 > tk \geq t0 \)  
  \( vk \sim N(0, Rk) \)

- The goal is to find the probability distribution for the state at time \( t \):  
  \( p(x,t | Yt) \)

---

### A General Context for Filtering with Geophysical Models

1. **State between observations** is obtained from the difference equation.
2. **Update state** given new observations using Bayes’ rule:
   \[
   p(x, tk | Ytk) = \frac{p(yk | xk, Ytk-1) p(x, tk | Ytk-1)}{p(yk | Ytk-1)}
   \]

3. **Normalizing denominator** involves integrating the numerator:
   \[
   p(yk | Ytk-1) = \int p(yk | x) p(x, tk | Ytk-1) dx
   \]

4. **Extend the state vector** to a joint state-observation vector \( z = [x, y] \), ensuring we have a prior for each observation.

---

### Dealing with Many Observations
- Observations may be split into subsets \( yk = \{yk^1, yk^2, ..., yk^s\} \).
- Observational errors in set \( i \) are independent from those in set \( j \).
- Assimilation can be done sequentially for these subsets:
  \[
  p(yk | z) = \prod_{i=1}^{s} p(yk^i | z)
  \]

#### Options for Non-Scalar Observations:
1. Use matrix algebra to repeat the derivation.
2. Apply singular value decomposition (SVD) to diagonalize the observation error covariance matrix, then assimilate in the rotated space.

Good news: Most geophysical observations have independent errors!

---

### How an Ensemble Filter Works for Geophysical Data Assimilation

1. **Advance ensemble to the next observation time** using the model.
2. **Obtain a prior sample of the observation** by applying the forward operator \( h(x) \) to each ensemble member.
3. **Get observed value and error distribution** from the observing system.
4. **Compute increments** for the prior observation ensemble.
5. **Linearly regress observation increments** onto state variable increments for each state variable.
6. **Update all ensemble members** to get a new analysis, then integrate forward to the next observation time.

---

### Non-Identity Observation Operators in Lorenz 63

- Try observing means of variables \( (x, y) \), \( (y, z) \), and \( (z, x) \) using the input file `obs_seq.out.average`.
- Same error variance and observation frequency as in previous cases.
- Modify `input.nml` in `models/lorenz_63/work`:
  ```fortran
  &filter_nml
  obs_sequence_in_name = "obs_seq.out.z"
  ```
- Execute the `filter` program and compare error statistics and time series to the identity case.
  
Results:  
- Errors are much larger!  
- Identity observations remove all regression error, but this can be misleading.

---

### Tutorial Index
1. Filtering for a One Variable System
2. The DART Directory Tree
3. DART Runtime Control and Documentation
4. How Observations Impact Unobserved State Variables
5. **Comprehensive Filtering Theory: Non-Identity Observations and Joint Phase Space**
6. Other Updates for Observed Variables
7. Additional Low-Order Models
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
18. Challenges of Not Knowing the Truth
19. DART-Compliant Models
20. Model Parameter Estimation
21. Observation Types and System Design
22. Parallel Algorithm Implementation
23. Location Module Design (not available)
24. Fixed Lag Smoother (not available)
25. 1D Advection Model: Tracer Data Assimilation

---

