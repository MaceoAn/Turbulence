# Turbulent Channel Flow — DNS vs RANS Study

This repository contains the analysis of turbulent flow between two parallel plates using different approaches over two TDs.

---

## TD1 — DNS vs RANS Study

This project analyses the turbulent flow between two parallel plates using three approaches:

- **DNS (Direct Numerical Simulation)** using reference data at $Re_\tau = 5200$  
- **RANS (Reynolds-Averaged Navier–Stokes)** with the **k–ε model** using ANSYS Fluent  
- **Mixing-length model** (Prandtl, 1925) for theoretical comparison

The objective is to compare velocity profiles, turbulent quantities, and stress distributions between the three approaches, and assess the performance and limitations of turbulence models.

### 🎯 Objectives

- Understand the fundamentals of turbulent channel flows  
- Use DNS data as a reference to compute:
  - velocity profile  
  - Reynolds stresses  
  - turbulence production $P$  
  - dissipation rate $\varepsilon$
- Implement the **Prandtl mixing-length model**
- Run a **k–ε RANS simulation** on Fluent
- Compare DNS / RANS / theoretical profiles

### 📘 Scientific Background

#### Turbulent kinetic energy (TKE)

Velocity decomposition:

$$ u_i = \bar{u}_i + u'_i $$

Mean kinetic energy:

$$ \bar{e}_c = \frac{1}{2}(\bar{u}_i^2 + \overline{u'_i u'_i}) $$

#### RANS equations

Incompressible Navier–Stokes:

$$ \frac{\partial u_i}{\partial x_i} = 0 $$

$$ \frac{\partial u_i}{\partial t} + u_j \frac{\partial u_i}{\partial x_j} = -\frac{1}{\rho}\frac{\partial p}{\partial x_i} + \nu \frac{\partial^2 u_i}{\partial x_j^2} $$

Reynolds decomposition yields:

$$ \bar{u}_j \frac{\partial \bar{u}_i}{\partial x_j} = -\frac{1}{\rho} \frac{\partial \bar{p}}{\partial x_i} + \nu \nabla^2 \bar{u}_i - \frac{\partial \overline{u'_i u'_j}}{\partial x_j} $$

#### Closure problem

The Reynolds stress tensor introduces 6 new unknowns → turbulence models required.

#### Mixing-length model

$$ \nu_t = l_m^2 \left|\frac{\partial \bar{u}}{\partial y}\right| $$

$$ l_m = \kappa y $$

#### k–ε model

$$ \nu_t = C_\mu \frac{k^2}{\varepsilon} $$

### 🧪 DNS Analysis

Using the dataset `LM_Channel_5200_prof.txt`, we compute:

- **Friction velocity**: $u_\tau = 0.78 \,\text{m/s}$  
- **Velocity profile**: follows log-law  
  $$ \frac{\bar{u}}{u_\tau} = \frac{1}{\kappa} \ln\left( \frac{y}{l_\tau} \right) + B $$
- **Turbulence production**:  
  $$ P = - \overline{u'_x u'_y} \frac{\partial \bar{u}}{\partial y} $$
- **Dissipation**:  
  $$ \varepsilon = 2\nu S'_{ij} S'_{ij} $$

### 🛠️ RANS Simulation (k–ε)

- 2D incompressible, statistically steady channel  
- Wall BCs, symmetry at mid-plane  
- Normalized using $u_\tau$ and $h$  
- Quantities extracted: mean velocity, Reynolds stresses, turbulent viscosity, $k$, $\varepsilon$, $P$

### 📊 DNS vs RANS Comparison

- RANS matches DNS velocity in log-region  
- Near-wall discrepancies due to k–ε limitations  
- Turbulent viscosity differs at low $y^+$  
- Production/dissipation peaks differ  
- DNS captures near-wall structures that RANS misses

---

## TD2 — Statistical Analysis & Scale Assessment

This part focuses on the **statistical properties of turbulence** and scale-based analysis.

### 🎯 Objectives

- Compute statistical moments of velocity fluctuations: mean, variance, skewness, kurtosis  
- Assess energy spectra and characteristic scales  
- Compare turbulence statistics with theoretical predictions (Kolmogorov scaling)  
- Use DNS dataset `LM_Channel_5200_prof.txt` for analysis  

### 📘 Scientific Background

#### Statistics of turbulent flow

- **Mean velocity**: $\bar{u}(y)$  
- **Fluctuations**: $u' = u - \bar{u}$  
- **Variance**: $\overline{u'^2}$  
- **Skewness**: $S = \overline{u'^3} / \overline{u'^2}^{3/2}$  
- **Kurtosis**: $K = \overline{u'^4} / \overline{u'^2}^{2}$  

#### Energy spectra

- Fourier transform of velocity fluctuations yields $E(k)$  
- Kolmogorov scaling in the inertial range:  
  $$ E(k) \sim \varepsilon^{2/3} k^{-5/3} $$

### 🧪 Analysis Procedure

1. Load DNS data  
2. Compute statistical moments for each velocity component  
3. Calculate Reynolds stresses  
4. Compute one-dimensional energy spectra using FFT  
5. Compare with theoretical inertial-range scaling  

### 📊 Key Observations

- Turbulence intensity peaks near the wall  
- Skewness indicates asymmetry in velocity fluctuations  
- Kurtosis highlights intermittent events  
- Energy spectra follow $k^{-5/3}$ scaling in inertial range  
- Near-wall and outer-layer scales differ significantly  

---

## 🧰 Repository Structure
