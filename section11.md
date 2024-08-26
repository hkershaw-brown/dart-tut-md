Here is the Markdown conversion of Section 11 from the DART tutorial:

---

# DART Tutorial Section 11:  
### Creating DART Executables  

---

### Fortran 90 ‘Use’ Trees

- DART requires the use of F90 `module_mod`, and no other mechanisms are used for external routines.
- Programs are viewed as a **Directed Acyclic Graph (DAG)**, where each program can be represented as a tree with shared leaves and no cycles.
- Example: A partial tree for the `filter` program is shown below:

```plaintext
obs_sequence_mod
  |
filter
  |
filter_mod
  |
assim_model_mod
assim_tools_mod
model_mod
location_mod
utilities_mod
```

---

### Generating a Makefile with `mkmf`

1. Use the **`mkmf`** Perl script to generate a Makefile for compiling.
2. **`mkmf`** searches for the main program and modules required, constructing a dependency graph based on the use of `module_mod`.

Steps:
- Run `quickbuild.sh` to generate the necessary list of files.
- **`mkmf`** creates a standard Makefile and generates a default namelist file: `input.nml.filter_default`.
- Use the `make` command to create the desired executable (e.g., `filter`).

---

### Using `mkmf` Templates

- DART provides a variety of **`mkmf` templates** for different machines and compilers, located in the `build_templates` directory.
- These templates specify:
  - The compiler to use.
  - Where to find the **netCDF** libraries.
  - Compiler and linker options for debugging or production.

To modify the template:
1. Copy the appropriate `mkmf.template.xxx` file to `mkmf.template`.
2. Make any necessary changes before running `quickbuild.sh`.

---

### Building with MPI

- DART provides two versions of the MPI module: one for actual MPI calls and one with dummy routines.
- By default, the MPI parallel version is built.

To build with MPI:
```bash
./quickbuild.sh filter
```

To build without MPI:
```bash
./quickbuild.sh nompi filter
```

---

### Exercise: Compiling the Lorenz 63 Filter Program

1. Navigate to `models/lorenz_63/work/`.
2. Remove all files with `.o` and `.mod` extensions.
3. Generate the Makefile and compile the filter program using:
   ```bash
   ./quickbuild.sh nompi filter
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
11. **Creating DART Executables**
12. Adaptive Inflation
13. Hierarchical Group Filters and Localization

---

This section outlines how to compile and create DART executables using `mkmf` and the process of building both MPI and non-MPI versions of programs. Let me know if you need further refinements!
