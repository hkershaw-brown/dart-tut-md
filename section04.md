
---

# DART Tutorial Section 4:  
### How Should Observations Impact an Unobserved State Variable?  
#### Multivariate Assimilation  

---

### Introduction
- Single observed variable, single unobserved variable.
- Previously, observation likelihood was known for a single variable.
- Now, the prior includes an additional variable.
- This section examines how ensemble methods update the additional variable.
- The basic method generalizes to any number of additional variables.
- Related to the Kalman filter but not applied here.

---

### Ensemble Filters: Updating Additional Prior State Variables

- Assume a prior joint distribution is known, with one variable observed.
- The task is to update the unobserved variable based on the observed one.
- Begin by updating the observed variable using existing methods.

---

### Compute Increments for Prior Ensemble Members
- For the observed variable, compute increments.
- Using these increments, update the unobserved variable.
- If the observation has no impact on the observed variable, the unobserved variable remains unchanged (a highly desirable property).

---

### Linear Regression for Unobserved Variables
- To update the unobserved variable, the first choice is least squares, equivalent to linear regression.
- Begin by finding a least squares fit, which is similar to assuming a binormal prior.
- The next step is to regress the observed variable’s increments onto those of the unobserved variable.
- This is equivalent to finding the image of the increment in joint space and projecting it onto the unobserved priors.

---

### Result: Updated (Posterior) Ensemble
- After the regression process, an updated posterior ensemble for the unobserved variable is obtained.
- Fitting Gaussians to the updated ensemble shows changes in mean and variance.
- Other features of the prior distribution may also have changed.

---

### Key Point: Independent Updates for Multiple Variables
- Since the impact on the unobserved variable is simply a linear regression, this process can be done independently for any number of unobserved variables.
- Alternatively, many variables can be updated at once using matrix algebra, similar to traditional Kalman filtering methods.

---

### Practical Example with the Lorenz 63 Model
1. **Multivariate assimilation in Lorenz 63**:  
   Modify the namelist `input.nml` in `models/lorenz_63/work` to observe specific state variables.
   - Test different combinations (e.g., observe only x and y, observe only x, observe only z).
   - Execute the `filter` program and analyze error statistics and time series using Matlab.

2. **Univariate assimilation**:  
   Set `&assim_tools_nml` parameters like `filter_kind = 1` and `cutoff = 1000000.0` for different assimilation experiments and compare the results with the multivariate case.

---

### Conclusion
- Multivariate assimilation methods allow for updating unobserved state variables based on observations of related variables.
- This process is highly flexible and can be applied to a wide range of models and scenarios using ensemble filtering techniques.

--- 

