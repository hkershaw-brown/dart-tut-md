
---

# DART Tutorial: Section 1  
### Filtering For a One Variable System

---

The National Center for Atmospheric Research is sponsored by the National Science Foundation.  
Any opinions, findings, conclusions, or recommendations expressed in this publication are those of the author(s) and do not necessarily reflect the views of the National Science Foundation.  
© UCAR

---

## Introduction

This series of tutorial presentations introduces basic Ensemble Kalman filter theory and the Data Assimilation Research Testbed (DART) Community Facility for Ensemble Data Assimilation.

There is significant overlap with the DART_LAB tutorial, which is also part of the DART subversion checkout. If you have already studied DART_LAB, feel free to skip the redundant theory slides. However, doing the exercises in all sections of this tutorial is recommended to learn the best ways to use the DART system.

---

## Bayes' Rule

- **Prior Estimate**: Based on all previous information (C).
- **Observation**: An additional observation (B).
- **Posterior Estimate**: Updated estimate based on C and B (p(A|BC)).

```math
p(A|BC) = \frac{p(B | AC) p(A | C)}{p(B | C)} = \frac{p(B | AC) p(A | C)}{\int p(B | x) p(x | C) dx}
```

---

### Color Scheme

- **Green**: Prior
- **Red**: Observation
- **Blue**: Posterior

This color scheme is consistent throughout all tutorial materials.

---

## Product of Two Gaussians

- The product is closed for Gaussian distributions.

```math
N(\mu_1, \Sigma_1) \cdot N(\mu_2, \Sigma_2) = cN(\mu, \Sigma)
```

- **Mean**:  
```math
\mu = (\Sigma_1^{-1} + \Sigma_2^{-1})^{-1} (\Sigma_1^{-1} \mu_1 + \Sigma_2^{-1} \mu_2)
```

- **Covariance**:  
```math
\Sigma = (\Sigma_1^{-1} + \Sigma_2^{-1})^{-1}
```

- **Weight**:  
```math
c = \frac{1}{(2\pi)^{d/2} (\Sigma_1 + \Sigma_2)^{1/2}} \exp \left( -\frac{1}{2} (\mu_2 - \mu_1)^T (\Sigma_1 + \Sigma_2)^{-1} (\mu_2 - \mu_1) \right)
```

---

### Continuous Distributions

- The product of prior Gaussian fit and observation likelihood is also Gaussian.
- Computing the continuous posterior is simple, but you need to have a sample of this PDF.

---

## Ensemble Adjustment (Kalman) Filter

- Use a **deterministic algorithm** to adjust the ensemble:
  1. **Shift** the ensemble to have the exact mean of the posterior.
  2. Use **linear contraction** to have the exact variance of the posterior.

The following transformations are applied:

```math
x_i^u = (x_i^p - \overline{x}^p) \cdot \frac{\sigma^u}{\sigma^p} + \overline{x}^u
```

Where:

- \(x_i^u\): Updated (posterior) value of the \(i\)th ensemble member.
- \(x_i^p\): Prior value of the \(i\)th ensemble member.
- \(\overline{x}^p\): Prior ensemble mean.
- \(\overline{x}^u\): Posterior ensemble mean.
- \(\sigma^p\): Prior standard deviation.
- \(\sigma^u\): Posterior standard deviation.

---

### Diagnostics and Examples

1. **First Look at DART Diagnostics**:
   - Run the following Matlab commands to explore the diagnostics:
     - `plot_total_err`: Plots the total error and spread over time.
     - `plot_ens_mean_time_series`: Plots the ensemble mean time series.

2. **Simple Example: Lorenz 63 3-Variable Chaotic Model**:
   - **Observation**: Shown in red.
   - **Prior Ensemble**: Shown in green.


Sure! Here’s the continuation of the conversion from the PDF into Markdown:

---

### Product of Two Gaussians (Continued)

- For **d-dimensional normals** with means \(\mu_1\) and \(\mu_2\) and covariance matrices \(\Sigma_1\) and \(\Sigma_2\):
  
```math
N(\mu_1, \Sigma_1) \cdot N(\mu_2, \Sigma_2) = cN(\mu, \Sigma)
```

Where:

- **Mean**:  
```math
\mu = (\Sigma_1^{-1} + \Sigma_2^{-1})^{-1} (\Sigma_1^{-1} \mu_1 + \Sigma_2^{-1} \mu_2)
```

- **Covariance**:  
```math
\Sigma = (\Sigma_1^{-1} + \Sigma_2^{-1})^{-1}
```

- **Weight** (ignored unless noted, since products are immediately normalized to be PDFs):

```math
c = \frac{1}{(2\pi)^{d/2} (\Sigma_1 + \Sigma_2)^{1/2}} \exp \left( -\frac{1}{2} (\mu_2 - \mu_1)^T (\Sigma_1 + \Sigma_2)^{-1} (\mu_2 - \mu_1) \right)
```

---

### Properties of the Gaussian Product

- The product of prior Gaussian fit and observation likelihood is Gaussian.
- **Easy to derive for 1-D Gaussians**: Simply compute the products of exponentials.
- For general distributions, there’s no analytical product unless the distribution is Gaussian.

---

## Sampling and Adjustment Techniques

### Ensemble Adjustment (Kalman) Filter

1. Use a **deterministic algorithm** to adjust the ensemble:
    - **Shift** the ensemble to have the exact mean of the posterior.
    - Use **linear contraction** to have the exact variance of the posterior.

2. Transformations for the ensemble members:
    - Posterior update formula for each ensemble member \(x_i\):
  
```math
x_i^u = (x_i^p - \overline{x}^p) \cdot \frac{\sigma^u}{\sigma^p} + \overline{x}^u
```

Where:

- \(x_i^u\) = updated (posterior) value of the \(i\)th ensemble member.
- \(x_i^p\) = prior value of the \(i\)th ensemble member.
- \(\overline{x}^p\) = prior ensemble mean.
- \(\overline{x}^u\) = posterior ensemble mean.
- \(\sigma^p\) = prior standard deviation.
- \(\sigma^u\) = posterior standard deviation.

---

### Example of Application: Lorenz 63 Model

- **Simple Example**: A 3-variable chaotic model.
- **Observations**: Represented in red.
- **Prior Ensemble**: Represented in green.

- **Observation Error Variance**: Set to 4.0.

### Visualization Example

```text
-20
 0
20

-20
 0
20

10
20
30
40
```

- This shows the prior ensemble and observations in the context of the Lorenz 63 model, where the ensemble moves through unpredictable regions.

---

### Using DART Diagnostics

- **Try the following Matlab commands** for diagnostics:
    - `plot_total_err`: Plots the total error and spread over time.
    - `plot_ens_mean_time_series`: Plots the ensemble mean time series.
  
These commands help visualize how the ensemble is performing compared to the truth and its internal consistency.

---

### Key Questions to Analyze Using DART Diagnostics:

- Can you see evidence of enhanced uncertainty?
- Where does this occur?
- Does the ensemble appear consistent with the truth? (Is the truth normally inside the ensemble range?)

---

### Further Sections to Explore

1. **Filtering For a One Variable System**
2. **The DART Directory Tree**
3. **DART Runtime Control and Documentation**
4. **Multivariate Assimilation**: How should observations of a state variable impact an unobserved state variable?
5. **Comprehensive Filtering Theory**: Non-Identity Observations and the Joint Phase Space
6. **Additional Updates for Observed Variables**
7. **Dealing with Sampling Error**
8. **Handling Error Inflation**
9. **Nonlinear Effects and Regression**
10. **Creating DART Executables**
11. **Adaptive Inflation**
12. **Hierarchical Group Filters and Localization**
13. **Quality Control and Experiment Design**

---

Sure! Here’s the next part of the conversion into Markdown:

---

### Ensemble Adjustment (Kalman) Filter (Continued)

- **Mean Shifted**: After applying the Kalman filter, the ensemble's mean shifts to match the posterior mean.
- **Variance Adjusted**: The variance is adjusted to match the posterior variance.
  
```text
-4  -2  0  2  4  0
0.2
0.4
0.6

Prior Ensemble

Posterior PDF
Mean Shifted
Variance Adjusted
```

- **Bimodality**: Bimodality is maintained, but not appropriately positioned or weighted. No issues arise with random outliers.

---

### Deterministic Ensemble Adjustment Algorithms

There are various ways to deterministically adjust the ensemble. The class of algorithms used is often referred to as **deterministic square root filters**.

---

### DART Diagnostics

- **Step 1**: Navigate to your DART sandbox:
  
```bash
cd models/lorenz_63/work
./workshop_setup.sh
matlab -nodesktop
```

- **Step 2**: Run Matlab scripts to explore the DART assimilation results. Examples include:

    - **Trajectory File**: Select the default file by hitting carriage return for all Matlab exercises:
      
      ```text
      <cr> for preassim.nc
      ```

    - **plot_total_err**: Plots the total error and spread of the ensemble.

    - **plot_ens_mean_time_series**: Shows the time series of the ensemble mean.

    - **plot_ens_time_series**: Displays the ensemble members.

---

### Simple Example: Lorenz 63 Model

#### Key Visualization:

- **Observation**: Displayed in red.
- **Prior Ensemble**: Displayed in green.

#### Observation Error Variance:

- **Variance**: Set to 4.0 for this example.

```text
-20  0  20
-20  0  20
10   20  30  40
```

---

### Questions to Ask:

- **Enhanced Uncertainty**: Is there evidence of enhanced uncertainty in the data?
- **Consistency**: Does the ensemble appear to be consistent with the truth? (Is the truth usually inside the ensemble's range?)

---

### DART Tutorial Index

Below is the index of all sections available in the DART tutorial. These sections dive deeper into the theory and practice of data assimilation using DART:

1. **Filtering For a One Variable System**
2. **The DART Directory Tree**
3. **DART Runtime Control and Documentation**
4. **How Should Observations of a State Variable Impact an Unobserved State Variable?**
5. **Comprehensive Filtering Theory**: Non-Identity Observations and the Joint Phase Space
6. **Other Updates for An Observed Variable**
7. **Some Additional Low-Order Models**
8. **Dealing with Sampling Error**
9. **More on Dealing with Error**: Inflation
10. **Regression and Nonlinear Effects**
11. **Creating DART Executables**
12. **Adaptive Inflation**
13. **Hierarchical Group Filters and Localization**
14. **Quality Control**
15. **DART Experiments**: Control and Design
16. **Diagnostic Output**
17. **Creating Observation Sequences**
18. **Lost in Phase Space**: The Challenge of Not Knowing the Truth
19. **DART-Compliant Models and Making Models Compliant**
20. **Model Parameter Estimation**
21. **Observation Types and Observing System Design**
22. **Parallel Algorithm Implementation**
23. **Location Module Design** (Not Available)
24. **Fixed Lag Smoother** (Not Available)
25. **A Simple 1D Advection Model**: Tracer Data Assimilation

---


## DART Tutorial Index to Sections

1. Filtering For a One Variable System
2. The DART Directory Tree
3. DART Runtime Control and Documentation
4. How Observations of a State Variable Impact an Unobserved State Variable
5. Comprehensive Filtering Theory: Non-Identity Observations and the Joint Phase Space
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
23. Location Module Design (Not Available)
24. Fixed Lag Smoother (Not Available)
25. A Simple 1D Advection Model: Tracer Data Assimilation

---


